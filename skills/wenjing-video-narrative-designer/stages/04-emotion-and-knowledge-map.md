# P4 · 情绪与知识映射

> wenjing-video-narrative-designer · Stage 04  
> 目的：把情绪、反应/呼吸、参与动作和知识点逐项映射到已确认 Narrative Nodes。

## 一、本阶段做什么

本阶段只为现有节点增加情绪与教学层；不改事实、不新增主事件、不写最终旁白、对白、场次或镜头。

前置条件：P3 hook_payoff_status=COVERED 且核心节点均有锚。生成前 Read `modules/participation-mechanisms.md`、`modules/exemplars.md` 的日常共鸣/反面例和 `modules/truth-lock-read-policy.md`。

## 二、引导逻辑

1. 为每个关键节点定义观众情绪词和相对强度 1–10；数字只用于比较变化，不声称心理测量精度。
2. 解释强度变化由哪个事实、取舍、发现或认知变化产生，不靠新编事件硬拉曲线。
3. 至少检查一个 Reaction/Reflection Beat 是否必要：让观众处理信息、代入或完成概念迁移；只写功能，不规定反应镜头。
4. 把每个 knowledge_id 映射到一个或多个 node_id，并选择叙事载体：问题、比较、决策、后果、发现、反思。
5. 说明观众在该点应“看懂/区分/判断/反思”什么，避免把理论原句硬塞进故事。
6. 将 P2 Participation Mechanism 放到合适节点，验证其不提前泄露 Payoff、不制造错误事实。
7. 检查结尾状态是否兑现 P1 target_emotion 与 Teaching Goal。
8. 若情绪或参与机制继承了 transfer rule，记录规则 ID 与本项目适配说明；不得据 transcript-only 规则写入实际音乐、表演或镜头节奏判断。

## 三、判断标准

- 情绪曲线至少有可解释的变化，但不强制大起大落。
- 每个强度变化都绑定 node_id 和触发依据。
- 1–3 个 knowledge_id 全覆盖，且每个至少关联一个 fact_id。
- Participation 有 node_id、audience_action、teaching_link 和安全边界。
- 结尾情绪与 Brief 一致；若不一致，回 P1/P3 修正，不在本阶段编新事实。

## 四、输出 schema 与落盘

更新 `{project_path}/stage-outputs/02_narrative_plan_DRAFT.md`：

### Emotion / Reaction / Reflection Beats

`beat_id`、`node_id`、`emotion_label`、`relative_intensity`、`change_trigger`、`beat_function`、`boundary_notes`、可选 `transfer_rule_refs`。

### Knowledge Embedding Map

`knowledge_id`、`fact_refs`、`node_id`、`narrative_vehicle`、`audience_learning_action`、`do_not_say_as_fact`。

### Participation Placement

`participation_id`、`node_id`、`audience_action`、`teaching_link`、`payoff_visibility`、`safety_notes`、可选 `transfer_rule_refs`。

同步 state：`current_station=P4`、`next_station=P5|P4`、knowledge_coverage、emotion_alignment、participation_status、last_checkpoint。

## 五、Hard Stop · 交付确认单

```text
╭─ 管理案例视频叙事设计器 · P4 完成 ─────╮
│ 💓 情绪节点：{count}
│ 🧠 知识覆盖：{covered}/{total}
│ 🙋 参与机制：{PLACED|PENDING|N/A}
│ 🎯 结尾情绪：{ALIGNED|MISALIGNED}
│ ✅ 产出：{draft_absolute_path}
│ 📍 下一步：{P5 边界审计|留在 P4 修复}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

知识未全覆盖或结尾情绪不一致时不得 `Next`。即使曲线好看，也不允许自动推进。

## 六、反模式

- 不把任意强度数字当科学测量。
- 不强迫低强度共鸣案例制造 10/10 高潮。
- 不把知识点写成脱离情节的讲义插播。
- 不把“反应/呼吸”越界写成摄影指令。
- 不让参与机制与教学目标无关。
- 不为补曲线新增上游没有的事实或因果。

---

*P4 完成后，主控加载 `stages/05-boundary-audit-and-review.md`。*
