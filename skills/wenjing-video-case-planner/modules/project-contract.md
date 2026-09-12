# 项目契约

> 仅在 P0、P6、Continue 或 Change Request 时加载。  
> 本模块定义工作空间、状态、锁、变更和跨 Skill 交接；不包含案例分析方法。

## 1. 工作空间边界

历史资产库与运行项目必须分离：

- 历史资产库：只读方法来源，不写运行产物。
- 运行项目：`{runtime_root}/{project_slug}/`，一个项目一套状态与产物。
- Skill 安装目录：只放 Skill 说明、模板与测试，不保存用户案例或生成内容。

运行项目结构：

```text
{project_path}/
├─ 00_project_manifest.yaml
├─ 00_project_state.md
├─ change-requests/
├─ stage-outputs/
│  ├─ 01_case_truth_lock_DRAFT.md
│  └─ 01_case_truth_lock_LOCKED.md
├─ conversation-log/
└─ assets-local/
```

任何写入前先解析并回显绝对路径。不得把磁盘根、用户主目录、历史资产库根或不明确的通配路径作为递归写入目标。

## 2. Manifest 最小契约

`00_project_manifest.yaml` 是项目静态身份与路由配置，至少包含：

```yaml
schema_version: video-project-manifest/v0.2
project_id:
project_slug:
title:
content_route: CASE
control_mode: FAST|GUIDED|STRICT
source_policy: FREE|GUIDED|SOURCE_LOCKED
continuity_level: LOW|MEDIUM|HIGH
target_audience:
teaching_goal:
duration:
aspect_ratio:
platforms: []
model_backend: seedance
cost_risk: LOW|MEDIUM|HIGH
artifacts: {}
status: ACTIVE|BLOCKED|COMPLETE
```

Case Planner 只可补全与本件相关的字段。不得替后续 Skill 决定视觉风格、镜头或模型参数。

## 3. State 最小契约

`00_project_state.md` 内嵌唯一 HUD JSON：

```json
{
  "pipeline_version": "0.2",
  "project_id": "",
  "content_route": "CASE",
  "control_mode": "GUIDED",
  "current_station": "P0",
  "next_station": "P1",
  "stage_status": {},
  "gate_status": {},
  "locked_artifacts": [],
  "stale_artifacts": [],
  "user_decisions": [],
  "open_change_requests": [],
  "current_blocker": "",
  "resume_prompt": "",
  "updated_at": ""
}
```

允许的 stage 状态：`LOCKED / ACTIVE / COMPLETE / BLOCKED / STALE / SKIPPED_OPTIONAL`。必经 Gate 不得标 `SKIPPED_OPTIONAL`。

允许的 Gate 状态：`PENDING / APPROVED / PASS / REVIEW_REQUIRED / BLOCKED`。

### v1.1 Artifact Registry（规范字段）

manifest/state 中每个 Artifact 条目至少包含：`artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧版 `path/locked_path` 可作为兼容别名保留，但不得替代 `content_ref`。

`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`。能访问本地文件且具备 SHA-256 能力时必须复算并匹配后写 `VERIFIED`；无 hash 能力的平台保留 `sha256` 字段为空并写 `NOT_OBSERVABLE`，禁止伪造。`DEFERRED` 表示尚未到验证时点，`FAIL` 表示预期值与可观察实际值不符。

`content_ref` 是逻辑引用，不保证是绝对路径；由 Runtime Adapter 按 `storage_backend=LOCAL_FILE | DOCUMENT_BOARD` 解析。业务 Skill 不拼接 Windows/Unix 分隔符，不把本地绝对路径当跨平台协议。

## 4. Artifact Contract

### Draft

- 路径：`stage-outputs/01_case_truth_lock_DRAFT.md`
- 状态：`DRAFT` 或 `APPROVED`
- 可编辑，但每次用户决策必须追加 Approval/Decision Log。
- 不得作为下游正式输入。

### Locked

- 路径：`stage-outputs/01_case_truth_lock_LOCKED.md`
- 状态：`LOCKED`
- 由已获用户批准的 Draft 生成；保留 Draft。
- manifest/state 必须登记版本、content_ref、storage_backend、完整性状态与批准时间；本地 hash 可用时另登记最终整文件 SHA-256。
- SHA-256 在 LOCKED 文件冻结后计算，只存入 manifest/state；不得写回 LOCKED 文件自身，避免 hash 自引用。
- 下游只读，不得原地修改。

正式继承物唯一判据：Artifact 可由 Adapter 解析、status=LOCKED、version 一致、必填字段完整；本地 hash 可用时 expected/actual/manifest/state 全部一致。无法观察 hash 时必须显式 `NOT_OBSERVABLE`，并由运行档位决定是否允许继续；不得静默修正。

## 5. Lock 状态机

```text
DRAFT → APPROVED → LOCKED
  ↑         │         │
  └─────────┴─ CHANGE_REQUEST → STALE → 新版本 DRAFT
```

- HARD：用户明确确认后才能从 APPROVED 进入 LOCKED。
- 锁定后发现问题必须创建 Change Request。
- 已被下游消费的上游版本变为 STALE 时，下游依赖产物也标 STALE；不得继续高成本生成。
- 新版本使用递增版本号；旧 LOCKED 文件保留审计记录，不静默覆盖。

## 6. Change Request

文件：`change-requests/CR-{YYYYMMDD}-{NNN}.md`。

必填：request_id、target_artifact/version、提出时间、原因、证据、拟改字段、影响的 fact/knowledge/boundary、受影响下游、风险、用户决策、status、需重跑阶段。

状态：`OPEN / APPROVED / REJECTED / APPLIED / CLOSED`。

## 7. Continue 协议

收到 `Continue {project_path}` 后严格按序执行：

1. 读 manifest 与 state。
2. 扫描 state 登记的产物，不以对话摘要替代磁盘检查。
3. 对 LOCKED 文件核对路径、状态和 hash。
4. 检查开放 Change Request 和 STALE 传播。
5. 输出 `READY / MISSING / STALE / BLOCKED` 资产表。
6. 定位 current/next station 和未决 Gate。
7. 等待用户确认恢复位置；不得自动跨过 Hard Stop。

若 state 缺失但产物存在：从文件重建“候选状态”，列出推断依据并让用户确认后才写回。

## 8. 跨 Skill 交接

Case Planner 完成时：

- `stage_status.case_planner=COMPLETE`
- `next_station=wenjing-video-narrative-designer`
- `resume_prompt` 写明需读取 manifest/state/LOCKED 路径
- 不在 state 中粘贴完整 Truth Lock 内容

下游不存在或未安装时，只登记下一站和直击口令，不伪装已运行。
