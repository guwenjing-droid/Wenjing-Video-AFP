# P3 · Narrative Nodes

> wenjing-video-narrative-designer · Stage 03  
> 目的：把已选策略展开为模型无关的叙事功能节点，并建立钩子兑现链。

## 一、本阶段做什么

本阶段只规定每个叙事节点承担什么功能、状态如何变化、依据什么事实；不写最终场景、对白、镜头、运镜、画风或模型 Prompt。

前置条件：P2 `strategy_selection=APPROVED|APPROVED_BY_POLICY` 且 selected_strategy_id 存在。生成前 Read `modules/narrative-strategy-library.md`、`modules/exemplars.md` 的结构正反例和 `modules/truth-lock-read-policy.md`。

## 二、引导逻辑

1. 依据已选策略选择节点功能，不机械套固定三段式。可用功能包括：建立情境、提出张力、显示取舍、升级后果、发现/转折、兑现、反思/余韵。
2. 为每个节点分配稳定 `NOD_01` 起的 ID。
3. 每个节点写清 `entry_state`、`narrative_function`、`content_summary`、`exit_state`。
4. `content_summary` 只能概括事实、解释或允许戏剧化功能；不得出现未经锚定的新事件。
5. 每个节点至少绑定 fact_id、knowledge_id 或明确的 ALLOWED boundary；若是 CONDITIONAL，必须引用已批准 decision_id。
6. 把 Hook Promise 绑定到一个或多个 Payoff Node；检查承诺强度与兑现内容等价。
7. 写给 Script Studio 的只是“下游写作任务”，不是替它写最终内容。
8. 若节点采用 transfer rule，记录 `transfer_rule_refs` 和 `adaptation_summary`；节点内容仍必须由本项目 Truth Lock 与教学目标独立成立。

## 三、方案型决策点

若同一策略存在两种合理次序，提供最多 2 个节点序列：

- 方案 A：信息先行——优势/代价/适用受众。
- 方案 B：体验先行——优势/代价/适用受众。

用户选择后登记 `node_sequence_decision_id`。结构差异不实质时不要为凑数制造伪方案。

## 四、输出 schema 与落盘

更新 `{project_path}/stage-outputs/02_narrative_plan_DRAFT.md`：

| 字段 | 含义 |
|---|---|
| node_id | 稳定节点 ID |
| narrative_function | 节点功能 |
| entry_state / exit_state | 观众认知或情绪状态变化 |
| content_summary | 非台词、非镜头的内容摘要 |
| fact_refs / knowledge_refs | 上游锚点 |
| boundary_class | FACT / ALLOWED / CONDITIONAL |
| conditional_decision_id | 条件批准记录，若适用 |
| hook_payoff_role | SETUP / DEVELOP / PAYOFF / NONE |
| downstream_writing_task | 给 Script Studio 的任务边界 |
| transfer_rule_refs | 可选；已采用的稳定规则 ID |
| adaptation_summary | 可选；说明如何去除来源专有内容并迁移到本项目 |

同时写 Hook Promise & Payoff Map，确保每个 hook_id 至少有一个有效 PAYOFF。

同步 state：`current_station=P3`、`next_station=P4`、node_count、hook_payoff_status、last_checkpoint。

## 五、Hard Stop · 交付确认单

```text
╭─ 管理案例视频叙事设计器 · P3 完成 ─────╮
│ 🧱 Narrative Nodes：{count}
│ 🪝 Hook 兑现：{COVERED|GAP}
│ 🔗 无锚节点：{count}
│ ✅ 产出：{draft_absolute_path}
│ 💾 状态：已写入 00_project_state.md
│ 📍 下一步：{P4 情绪与知识映射|留在 P3 修复}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

hook_payoff_status=GAP 或存在无锚核心节点时不得 `Next`。即使结构顺畅，也不允许自动进入 P4。

## 六、反模式

- 不把节点写成“镜头 1/场景 1”或逐字台词。
- 不机械要求每个案例都有反派、反转或高潮。
- 不让后果节点暗示材料未证明的因果。
- 不用抽象空话替代 entry/exit 状态变化。
- 不让 Hook 在结构中失踪。
- 不写角色外观、机位、光影或模型参数。
- 不因参考视频使用某一顺序就机械复制其段落或事件排列。

---

*P3 完成后，主控加载 `stages/04-emotion-and-knowledge-map.md`。*
