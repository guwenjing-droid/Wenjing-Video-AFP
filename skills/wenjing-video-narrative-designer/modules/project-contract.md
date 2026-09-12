# Module · Project Contract

> 供 P0–P6、Continue 与 Change Request 按需读取。只管理工作空间、资产状态、Gate 和跨 Skill 交接，不执行叙事设计。

## 1. 公共工作空间

项目根必须包含：

```text
00_project_manifest.yaml
00_project_state.md
change-requests/
stage-outputs/
  00_reference_analysis/                 # 可选
  01_case_truth_lock_LOCKED.md            # Narrative 必需
  02_narrative_plan_DRAFT.md
  02_narrative_plan_LOCKED.md
```

所有 Artifact 在 manifest/state 中使用逻辑 `content_ref`；Local File Adapter 可回报解析后的本地位置，Document/Board Adapter 回报 document/object ref。Skill 源码目录和运行项目存储不得混用。

## 2. 资产四态

| 状态 | 定义 | 能否正式消费 |
|---|---|---|
| READY | 文件存在、schema/版本/完整性登记一致、无阻断 CR | 可以 |
| MISSING | 契约要求的文件不存在 | 不可以 |
| STALE | 其依赖的 LOCKED 上游已升版、重开或改变 | 不可以 |
| BLOCKED | 文件存在但状态、schema、Gate 或 CR 不允许消费 | 不可以 |

可选 Reference Analysis 另有路由状态：

- `NOT_PROVIDED`：没有提供；正常继续 CASE 主链。
- `AVAILABLE`：LOCKED、契约兼容且可观察范围有效，可作为候选机制来源。
- `EXCLUDED`：不满足采用条件；从本轮候选中排除，不污染 Narrative。
- `REQUIRED_BUT_INVALID`：用户/manifest 明确要求采用但 Artifact 无效；阻断并回到 Review。

## 3. Manifest 最小字段

```yaml
pipeline_version: "0.3"
project_id: ""
content_route: "CASE"
control_mode: "FAST | GUIDED | STRICT"
artifacts:
  case_truth_lock: {path: "", version: "", status: "LOCKED", sha256: ""}
  narrative_plan: {draft_path: "", locked_path: "", version: "", status: ""}
optional_reference_analysis:
  adoption_intent: "NONE | OPTIONAL | REQUIRED"
  selected:
    - {reference_id: "", path: "", version: "", status: "LOCKED", sha256: "", input_modality: "", analysis_scope: []}
preauthorizations:
  narrative_strategy: false
  narrative_lock: false
```

不得为了让流程通过而补造上游路径、版本、完整性值或用户授权。

## 4. State 最小字段

`00_project_state.md` 必须保留可读 HUD 与变更历史：

```json
{
  "pipeline_version": "0.3",
  "project_id": "",
  "current_station": "P0",
  "next_station": "P1",
  "stage_status": {},
  "gate_status": {},
  "locked_artifacts": [],
  "stale_artifacts": [],
  "optional_reference_analysis": {"adoption_intent": "NONE", "selected": [], "status": "NOT_PROVIDED"},
  "user_decisions": [],
  "open_change_requests": [],
  "current_blocker": "",
  "resume_prompt": "",
  "updated_at": ""
}
```

状态盘用于恢复，Narrative Draft/LOCKED 用于交接；两者不能互相替代。

## 5. Reference Analysis 读取契约

冻结规范：项目编排附件 `Reference_Analysis_Artifact_Contract_v0.1.md`。

P0 对每个 selected ref 执行：

1. 文件存在且 `status=LOCKED`。
2. contract version 与 `reference-analysis/0.1` 兼容。
3. manifest/state 的 path、version、sha256 一致，并对文件重新计算完整性值。
4. `input_modality` 与实际 `observed_materials` 一致。
5. `analysis_scope` 没有覆盖 missing modalities。
6. transcript-only 的 Audiovisual section 为 `NOT_OBSERVABLE`。
7. Artifact 没有开放的阻断 CR，也未被标 STALE。

只有通过检查的 Transfer Engine 规则可进入 P2 候选池。采用顺序固定为：

```text
Case Truth Lock > 用户/项目约束 > Reference Analysis
```

任何冲突都淘汰 reference rule，而不是修改 Truth Lock 或用户约束。

## 6. Gate 与审批语义

- HARD：必须有用户明确批准记录，才能进入下一站或 LOCK。
- REVIEW：必须展示；只有 manifest 已存在对应预授权，才可记 `APPROVED_BY_POLICY`。
- AUTO：机器规则全绿即可通过；YELLOW/歧义升级为 REVIEW，RED/BLOCK 不得绕过。

Reference 采用还需：

- G-RA-01 Input Modality
- G-RA-02 Observability
- G-RA-03 Original Transfer
- G-ND-RA Adoption

未提供 Reference 时四项均为 `N/A`，不是失败。

## 7. Lock、完整性与 STALE 传播

- 正式继承物走 `DRAFT → APPROVED → LOCKED`。
- LOCKED 文件本体不写入自身整文件 SHA-256；冻结后计算并只登记到 manifest/state。
- 上游 Truth Lock 重开或变更：Narrative Draft/LOCKED 及其下游全部标 STALE。
- 被实际采用的 Reference Analysis 重开或变更：Narrative Draft/LOCKED 标 STALE；未采用的 Reference 变化不污染 Narrative。
- Reference 被 `EXCLUDED` 后不得残留在 `adopted_transfer_rule_ids`。

## 8. Change Request

禁止原地覆盖 LOCKED。CR 至少记录：

`cr_id`、target path/version/sha256、原因、影响的 fact/knowledge/node/transfer_rule、申请时间、决策、需重跑站点、STALE 传播范围。

批准后创建新 Draft 版本并重过相应 Gate；旧 LOCKED 保留审计链。

## 9. Continue 协议

`Continue {project_path}`：

1. 读取 manifest/state/开放 CR。
2. 复核所有实际依赖的 LOCKED 文件及完整性登记。
3. 列出 READY/MISSING/STALE/BLOCKED，以及 Reference 的 NOT_PROVIDED/AVAILABLE/EXCLUDED/REQUIRED_BUT_INVALID。
4. 以 `next_station` 和最近 checkpoint 定位恢复点。
5. 展示恢复清单并 Hard Stop；不得重问磁盘中仍有效的决定。

## 10. 项目契约反模式

- 不把可选 Reference 缺失当主链失败。
- 不把 REQUIRED 的无效 Reference 静默降级。
- 不让 Reference Analysis 覆盖 Truth Lock。
- 不把对话里的批准当成未落盘授权。
- 不修改 LOCKED 文件后沿用旧完整性登记。
- 不在上游 STALE 后继续消费下游成本。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
