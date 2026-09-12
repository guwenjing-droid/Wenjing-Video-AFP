# P1 · Narrative Brief

> wenjing-video-narrative-designer · Stage 01  
> 目的：从 Truth Lock 与 manifest 提取本件所需的最小叙事简报，不重新解释案例事实。

## 一、本阶段做什么

本阶段只建立 Audience–Teaching–Emotion–Platform–Duration 简报与上游继承表；不设计正式钩子、结构节点、台词、场次或镜头。

前置条件：P0 `input_integrity=PASS`。Read `modules/truth-lock-read-policy.md` 与 `templates/narrative-plan-template.md`。

## 二、引导逻辑

1. 从 Truth Lock 复制 project/version、Teaching Goal、1–3 个 knowledge_id、核心 fact_id 与 Boundary 摘要。
2. 从 manifest/state 读取 content_route、control_mode、目标受众、发布平台、目标时长或其他形式约束。
3. 区分三种字段来源：`INHERITED_LOCKED`、`USER_DECISION`、`PENDING`；不得把推测写成继承值。
4. 将目标情绪定义成观众完成观看后的可描述状态，如“理解取舍”“产生共鸣”“愿意复盘”，避免写成“必须爆”。
5. 若目标情绪缺失，给 2–3 个与 Teaching Goal 相容的候选，并说明收益、代价和事实风险。
6. 对平台/时长缺失：若不影响策略，可标 PENDING；若会改变叙事容量，列为 blocker 等待补齐。
7. 若 P0 有 `AVAILABLE` Reference Analysis，只把其 Contract Header 登记为可选来源，并列出当前 analysis_scope；本阶段不采纳 transfer rule、不导入原视频内容。

## 三、方案型决策点

仅在目标情绪或传播任务未锁定时提供候选：

```text
方案 A：{目标情绪/传播任务}
依据：{teaching_goal / knowledge_id / fact_id}
优势：{...}
代价：{...}
事实风险：{LOW|MEDIUM|HIGH + 原因}
```

用户明确选择后写入 `decision_id`；未选择时不得把推荐项当已确认。

## 四、输出 schema 与落盘

创建或更新：

`{project_path}/stage-outputs/02_narrative_plan_DRAFT.md`

本阶段写入：

- Contract Header：project_id、status=DRAFT、version、upstream path/version/hash。
- Narrative Brief：audience、teaching_goal、knowledge_ids、content_route、control_mode、platform、duration_constraint、target_emotion。
- Truth & Boundary Inheritance：事实、知识和边界的只读 ID 清单。
- Reference Analysis Availability（可选）：`reference_analysis_refs`、input_modality、analysis_scope、adoption_intent；未提供时为空数组。
- Decision Log：候选、用户选择、时间和依据。
- Pending Fields / Blockers。

同步 state：`current_station=P1`、`next_station=P2|P1`、brief_status、draft_path、last_checkpoint、last_user_decision。

## 五、Hard Stop · 交付确认单

```text
╭─ 管理案例视频叙事设计器 · P1 完成 ─────╮
│ 👥 受众：{audience}
│ 🎓 教学目标：{teaching_goal_summary}
│ 🧠 知识点：{count}/3
│ 💓 目标情绪：{confirmed|PENDING}
│ 🎞️ Reference：{available_count|0}
│ ✅ 产出：{draft_absolute_path}
│ 💾 状态：已写入 00_project_state.md
│ 📍 下一步：{P2 钩子与参与策略|留在 P1}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

即使系统有推荐，也不允许自动替用户锁定缺失的方向性字段或自动进入 P2。

## 六、反模式

- 不重做 Truth Audit 或改写 Teaching Goal。
- 不把“爆款”当目标情绪或可保证结果。
- 不因平台常见做法硬编码 3 秒、60 秒或镜头数。
- 不在 Brief 阶段提前写钩子、对白或镜头。
- 不把 PENDING 字段静默补成模型猜测。
- 不把 Reference Analysis 中的观点当成本项目事实或教学目标。

---

*P1 完成后，主控加载 `stages/02-hook-and-participation.md`。*
