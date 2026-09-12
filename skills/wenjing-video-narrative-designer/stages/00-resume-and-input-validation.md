# P0 · 恢复与输入校验

> wenjing-video-narrative-designer · Stage 00  
> 目的：从项目磁盘恢复状态，验证必需的 Truth Lock，并校验已登记的可选 Reference Analysis。

## 一、本阶段做什么

本阶段只扫描项目、恢复状态、校验必需与可选输入并建立最小项目壳；不设计钩子、结构或情绪，不创建 Narrative Draft。

开始前 Read `modules/project-contract.md` 与 `modules/truth-lock-read-policy.md`。

## 二、引导逻辑

### 已有项目

1. 读取用户给出的绝对项目路径。
2. 读取 `00_project_manifest.yaml`、`00_project_state.md` 和开放 Change Request。
3. 定位 `stage-outputs/01_case_truth_lock_LOCKED.md`。
4. 验证文件存在、内部 status 为 LOCKED、必填区完整、版本与 manifest/state 一致。
5. 通过 Runtime Adapter 解析 `content_ref`，核对 `status=LOCKED`、artifact version 与 manifest/state 一致；本地文件系统且 hash 可用时，重新计算冻结文件整文件 SHA-256，并与 manifest/state 的 expected hash 比较。任一不一致必须 `BLOCKED`，不得静默修正。无 hash 能力时保留空 `sha256` 并标 `integrity_status=NOT_OBSERVABLE`；仅非 STRICT 的 Dry Run 可按 Gate policy 继续，STRICT/真实生产可要求 `VERIFIED`。LOCKED 文件本体不应内嵌自身整文件 hash。
6. 检查上游是否被标 STALE、是否有影响 FACT/KP/Boundary 的开放 CR。
7. 列出 READY、MISSING、STALE、BLOCKED 资产与下一安全动作。

### 可选 Reference Analysis

8. 从 manifest 的 `optional_reference_analysis` 读取 `adoption_intent` 与 selected refs；没有登记时写 `NOT_PROVIDED`，不得阻断标准 CASE 主链。
9. 对每个 selected ref 校验 `Reference_Analysis_Artifact_Contract_v0.1`：LOCKED、版本兼容、路径/完整性信息一致、input_modality 与 observed_materials 一致。
10. 根据 analysis_scope 冻结可读取维度。`TRANSCRIPT_ONLY` 只允许 Content、Narrative 和部分 Engagement；Audiovisual 必须为 `NOT_OBSERVABLE`。
11. 可选 ref 无效时标 `EXCLUDED` 并继续；只有 `adoption_intent=REQUIRED` 时标 `REQUIRED_BUT_INVALID` 并阻断 P1。
12. 不读取 source-specific 或 do-not-copy 内容作为候选机制；P0 只登记可用性，不在本阶段采纳 transfer rule。

### Direct Use 无项目壳

若 manifest/state 不存在，先 Read `templates/project-manifest-minimum.yaml` 和 `templates/project-state-template.md` 建最小项目壳。不得自行制造 Truth Lock；上游正式输入缺失时保持 BLOCKED，并提示先运行 `wenjing-video-case-planner`。

### 恢复既有 Narrative

若 Narrative Draft/LOCKED 已存在，核对其 upstream version/hash 与当前 Truth Lock：

- 一致且无 CR：READY，定位 state 的实际 current_stage。
- 上游版本变化或 hash 不一致：Narrative 及依赖物标 STALE。
- 已有 LOCKED 且用户要求修改：创建 Change Request，不原地覆盖。

## 三、判断标准

只有以下条件全部满足，`input_integrity=PASS`：

- manifest/state 可读且 project_id 一致。
- Truth Lock 文件存在、status=LOCKED、schema 可读。
- `status=LOCKED` 且 version 一致；本地 hash 可用时 expected/actual/manifest/state 一致，否则按当前档位合法处理 `NOT_OBSERVABLE`。
- Truth Lock 不是 STALE，且没有阻断级开放 CR。
- FACT、Core Knowledge Points、Teaching Goal、ALLOWED/CONDITIONAL/FORBIDDEN 可读取。

Reference Analysis 不属于 `input_integrity` 的必需条件，但若被登记则必须得到以下单独结论：

- `reference_input_modality=PASS|REVIEW|BLOCK|N/A`
- `reference_observability=PASS|REVIEW|BLOCK|N/A`
- `reference_analysis_status=AVAILABLE|NOT_PROVIDED|EXCLUDED|REQUIRED_BUT_INVALID`

任一失败，`next_station` 保持 P0，不允许 `Next` 解锁 P1。

## 四、输出 schema 与落盘

更新 `{project_path}/00_project_manifest.yaml` 与 `{project_path}/00_project_state.md`：

```text
current_station: P0
next_station: P1 | P0
input_integrity: PASS | BLOCKED
upstream_truth_lock: {path, version, sha256, status}
optional_reference_analysis:
  adoption_intent: NONE | OPTIONAL | REQUIRED
  selected_refs: [{reference_id, path, version, sha256, input_modality, analysis_scope}]
  status: AVAILABLE | NOT_PROVIDED | EXCLUDED | REQUIRED_BUT_INVALID
reference_gates: {input_modality, observability, originality, adoption: PENDING|N/A}
assets: [{path, status: READY|MISSING|STALE|BLOCKED, reason}]
open_change_requests: [...]
current_blocker: ...
updated_at: ...
```

P0 的实质产物是状态盘和资产表；不创建 `02_narrative_plan_DRAFT.md`。

## 五、Hard Stop · 交付确认单

```text
╭─ 管理案例视频叙事设计器 · P0 完成 ─────╮
│ 📊 项目：{project_id}
│ 📥 Truth Lock：{READY|MISSING|STALE|BLOCKED}
│ #️⃣ Hash：{MATCH|MISMATCH|MISSING}
│ 🎞️ Reference：{AVAILABLE|NOT_PROVIDED|EXCLUDED|REQUIRED_BUT_INVALID}
│ 👁️ 可观察范围：{scope|N/A}
│ 💾 状态：{state_absolute_path}
│ 🚦 input_integrity={PASS|BLOCKED}
│ 📍 下一步：{P1 Narrative Brief|留在 P0 修复}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

即使输入看似完整，也必须写盘并等待用户 `Next`；BLOCKED 时不得接受越阶请求。

即使校验结果明确，也不允许自动推进到 P1。

## 六、反模式

- 不凭对话摘要假设 Truth Lock 已存在。
- 不跳过 hash、STALE 或 Change Request 检查。
- 不把 DRAFT 当 LOCKED 输入。
- 不在上游缺失时自己重做 Case Planner。
- 不因可选 Reference Analysis 缺失而阻断标准 CASE 主链。
- 不相信 Artifact 对未提供模态的自我声明；以实际 observed_materials 为准。
- 不重问磁盘已保存且仍有效的用户决定。

---

*P0 完成后，主控加载 `stages/01-narrative-brief.md`。*
