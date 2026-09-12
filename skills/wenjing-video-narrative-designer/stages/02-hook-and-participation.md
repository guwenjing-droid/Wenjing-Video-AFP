# P2 · 钩子与参与策略

> wenjing-video-narrative-designer · Stage 02  
> 目的：生成可比较、可追溯的钩子与观众参与组合，由用户或已登记策略完成选择。

## 一、本阶段做什么

本阶段只选 Narrative Strategy、Hook Promise 和 Participation Mechanism；不展开完整节点，不写最终台词、场次、镜头或标题文案。

前置条件：P1 brief_status=READY。生成前 Read `modules/narrative-strategy-library.md`、`modules/participation-mechanisms.md`、`modules/exemplars.md` 的钩子/共鸣正反例，以及 `modules/truth-lock-read-policy.md`。

## 二、引导逻辑

1. 根据 Teaching Goal、目标情绪、事实强度和 Boundary，筛选适配的策略族：冲突、悬念、反差、决策—后果、共鸣、观察/治愈。
2. 至少提供 2 个、最多 3 个差异显著的组合；不把强刺激路线设为默认唯一答案。
3. 每个 Hook Promise 必须绑定 `fact_id`/`knowledge_id`，说明后续应在哪类 Payoff Node 兑现。
4. 每个 Participation Mechanism 必须回答“观众做什么认知动作”：预测、选择、代入、比较、反思或贡献案例。
5. 检查互动是否服务教学目标，是否泄露隐私、诱导错误答案或沦为无关互动诱饵。
6. 给出系统推荐及理由，但保留用户选择权。
7. 若有 AVAILABLE Reference Analysis，只从 Transfer Engine 读取适用 `narrative` 的规则；逐条先过 Truth Lock、项目约束、可观察范围和原创迁移预检，再作为候选机制，而不是模板答案。

## 三、方案型决策点

```text
方案 {A|B|C}：{strategy_name}
Hook Promise：{只描述承诺，不写成终稿台词}
事实/知识锚点：{fact_ids / knowledge_ids}
Participation：{mechanism + audience_action}
预期情绪路径：{start → shift → end}
兑现要求：{payoff_function}
优势：{...}
代价：{...}
越界风险：{LOW|MEDIUM|HIGH + 原因}
Reference 规则：{transfer_rule_ids|NONE}；迁移说明：{如何改变语境和表达}
适配度：{score/criteria，不伪装成客观概率}
```

写入 `selected_strategy_id` 才算完成。GUIDED/STRICT 必须由用户选择；FAST 只有在 manifest 明确登记 narrative_strategy 预授权时，才可把展示后的推荐项记为 `APPROVED_BY_POLICY`。无论哪种模式，本阶段仍输出 Hard Stop，等待 `Next` 才进入 P3。

## 四、输出 schema 与落盘

更新 `{project_path}/stage-outputs/02_narrative_plan_DRAFT.md`：

- Strategy Options：A/B/C 全量比较。
- Selected Narrative Strategy：selected_strategy_id、decision_source、decision_id。
- Hook Promise & Payoff Requirement：hook_id、promise、fact_refs、knowledge_refs、required_payoff_function、risk。
- Participation Mechanism：participation_id、type、audience_action、teaching_link、safety_notes。
- `reference_analysis_refs`：实际读取的 LOCKED Artifact path/version/sha256/modality/scope。
- `adopted_transfer_rule_ids`：候选或已采纳规则、applied_to、adaptation_summary、truth/project/originality checks；不采用时为空数组。
- Decision Log 与被拒方案理由。

同步 state：`current_station=P2`、`next_station=P3|P2`、`strategy_selection=APPROVED|APPROVED_BY_POLICY|PENDING`、selected_strategy_id。

## 五、Hard Stop · 交付确认单

```text
╭─ 管理案例视频叙事设计器 · P2 完成 ─────╮
│ 🧭 候选策略：{count}
│ ✅ 已选：{selected_strategy_id|PENDING}
│ 🪝 Hook：{hook_id}
│ 🙋 参与机制：{participation_id}
│ 🔁 迁移规则：{adopted_count|0}
│ 🚦 strategy_selection={status}
│ ✅ 产出：{draft_absolute_path}
│ 📍 下一步：{P3 Narrative Nodes|留在 P2 选择}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

没有 `selected_strategy_id` 时，`Next` 不得越过本阶段。即使策略明显，也不允许省略方案比较或自动连跳 P3。

## 六、反模式

- 不使用与“案例视频”无关的泛化爆款公式。
- 不为强钩子发明对立者、数字、因果或结局。
- 不让 Hook Promise 没有事实锚点和兑现要求。
- 不把“评论区扣 1”当默认参与机制。
- 不把方案写成逐字开场台词或具体镜头。
- 不把适配评分描述成传播成功概率。
- 不复制参考视频原句、专有角色、段落顺序或独特镜头组合，不用换词伪装原创。
- 不采用超出 Artifact analysis_scope 的视听规则。

---

*P2 完成后，主控加载 `stages/03-narrative-nodes.md`。*
