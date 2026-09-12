# Module · Boundary Audit

> 供 P5 按需读取。逐项验证 Narrative Draft 的事实忠实、职责边界、Hook 兑现、Reference 可观察性与原创迁移。

## 1. 审计输入

1. 当前 `02_narrative_plan_DRAFT.md`
2. 当前 `01_case_truth_lock_LOCKED.md`
3. manifest/state 与开放 Change Request
4. Draft 实际引用的 Reference Analysis LOCKED Artifacts（若有）

审计前重新校验所有实际依赖的路径、版本、状态和完整性登记。依赖变化则先标 STALE，不继续内容审计。

## 2. 审计顺序

### A. Truth Integrity

逐个 Hook、Node、Payoff、Emotion Trigger、Knowledge Map 检查：

- fact_id / knowledge_id 是否存在。
- 主体、数字、时间、因果、结果与限定词是否保持一致。
- INTERPRETATION 是否被伪装成 FACT。
- 新增内容是否落在 ALLOWED；CONDITIONAL 是否有批准 decision_id。
- FORBIDDEN 命中必须为 0。

### B. Promise–Payoff

- 每个 hook_id 有至少一个有效 Payoff Node。
- Promise 强度不高于 Payoff 能证明的内容。
- Payoff 没有靠新增事实或下游镜头技巧补洞。
- 延迟信息没有隐去理解案例所必需的前提。

### C. Teaching & Audience

- 1–3 个 knowledge_id 全覆盖。
- 每个知识点有可观察的学习动作：看懂、区分、判断或反思。
- 解释深度、术语密度与已登记受众相容。
- Ending 同时兑现 Teaching Goal 与 target_emotion。

### D. Narrative Boundary

Draft 不得出现：

- 最终逐字台词、旁白成稿
- 场次级拍摄脚本
- 景别、机位、构图、运镜、光影
- 角色视觉定稿或资产 Prompt
- Seedance 或其他模型参数/调用

允许写“下游功能任务”，不允许替相邻 Skill 交付成品。

### E. Reference Adoption（仅非空时）

#### G-RA-01 Input Modality

- Artifact 的 input_modality、observed_materials、missing_modalities、analysis_scope 相互一致。
- 失败：`BLOCK`，移除规则；若 adoption_intent=REQUIRED，回用户 Review。

#### G-RA-02 Observability

- 每个采用规则的 observable_basis 可定位且属于已提供模态。
- transcript-only 不得支持镜头、运镜、表演、字幕、BGM、音效、转场、色彩或光影结论。
- `ANCHOR_LIMITED` 必须降低置信度并进入 REVIEW。

#### G-RA-03 Original Transfer

- 机制已脱离原视频专名、角色、事件、措辞、段落和独特镜头组合。
- source_specific_elements 与 do_not_copy 无命中。
- originality risk=MEDIUM 转人工 REVIEW；HIGH 或实质复制为 BLOCK。

#### G-ND-RA Adoption

每条 `adopted_transfer_rule_id` 必须有：

- 对应 LOCKED reference artifact
- `applied_to`
- `adaptation_summary`
- `truth_lock_check=PASS`
- `project_constraint_check=PASS`
- `originality_check=PASS`

任一缺失，该规则不得进入 LOCKED Narrative Plan。

## 3. Issue 分级

| Severity | 定义 | 处理 |
|---|---|---|
| BLOCKER | 上游无效、FORBIDDEN、事实无锚、视听幻觉、实质复制 | 阻断 P6 |
| MAJOR | Hook 未兑现、知识缺失、职责越界、必填 provenance 缺失 | 修复后重审 |
| REVIEW | CONDITIONAL、ANCHOR_LIMITED、MEDIUM 原创风险、方向性歧义 | 用户裁决 |
| MINOR | 表述、编号或非核心格式问题 | 修复并记录 |

每个 issue：`issue_id`、severity、section、object_id、upstream/reference evidence、required_action、owner、status。

## 4. PASS 判据

`READY_FOR_APPROVAL` 必须同时满足：

- Truth Lock 仍 READY。
- FORBIDDEN=0；未决阻断 CONDITIONAL=0。
- 无锚核心节点=0；未兑现 Hook=0。
- knowledge coverage=100%；结尾与 Brief 对齐。
- 职责越界=0。
- Reference 未使用时相关 Gate=`N/A`；使用时四个 Gate 全部 PASS。
- 12 节 schema、Decision/Approval Log、Downstream Handoff 完整。

不允许用总分抵消 BLOCKER；一个 BLOCKER 即不得进入 P6。

## 5. 审计输出

写入 Draft 的 Boundary Audit / Reference Adoption Audit / Review Summary：

```yaml
review_status: "READY_FOR_APPROVAL | REVIEW_REQUIRED | BLOCKED"
truth_integrity: "PASS | BLOCK"
forbidden_hits: 0
unanchored_core_nodes: 0
unpaid_hooks: 0
knowledge_coverage: "100%"
role_boundary: "PASS | BLOCK"
reference_gates:
  input_modality: "PASS | REVIEW | BLOCK | N/A"
  observability: "PASS | REVIEW | BLOCK | N/A"
  originality: "PASS | REVIEW | BLOCK | N/A"
  adoption: "PASS | REVIEW | BLOCK | N/A"
issues: []
```

## 6. 审计反模式

- 不只看文风顺不顺而忽略锚点。
- 不把 Reference 的流行度当有效证据。
- 不因“只是借鉴”跳过逐规则原创检查。
- 不在审计阶段偷偷重写 Truth Lock。
- 不把 REVIEW_REQUIRED 写成 PASS。
