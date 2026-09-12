# P3 · 教学目标锁定

> wenjing-video-case-planner · Stage 03  
> 目的：把经过审核的事实转成 1–3 个可教学、可映射的核心知识点，并由用户确认教学方向。

## 一、本阶段边界

本阶段只确定受众、教学目标和知识点映射，不设计最终钩子、情绪曲线、剧情、对白或镜头。

前置条件：Truth Audit 不是 BLOCKED；核心 Fact Table 已形成。

## 二、教学目标构造

先确认三件事：

1. **谁学**：受众的角色、已有知识和使用场景。
2. **学什么**：从案例事实中理解的 1–3 个管理/经济知识点。
3. **学完能做什么**：使用可观察动词，如识别、比较、判断、解释、选择；避免“有所启发”。

每个知识点分配 `KP_01` 起的 ID，并至少关联一个 `fact_id`。区分：

- 案例材料明确支持的知识点。
- 教师基于案例引入的理论解释；此类必须标 `TEACHING_INTERPRETATION`，不能伪装成案例事实。

## 三、方案型决策

当材料允许多种教学角度时，输出 2–3 个方案，每个包含：

- 教学焦点与一句话目标
- 选用的 knowledge points
- 依赖的 fact_id
- 优势、可能损失和适合受众
- 是否会弱化案例中的其他重要矛盾

示例格式：

```text
方案 A：决策与激励——优势：冲突清楚；代价：弱化组织文化线。
方案 B：组织文化——优势：适合课堂讨论；代价：需要更多背景解释。
请选择 A / B，或提出组合与修改。
```

系统可以推荐，但必须说明理由；用户确认前不得把某方案写成 LOCKED 教学方向。

## 四、完成标准

- knowledge point 为 1–3 个。
- 每个 knowledge point 有 fact_id 映射；理论补充有单独标识。
- 目标受众具体。
- 教学结果可观察、可评价。
- 不以“故事更精彩”为选择教学方向的主要理由。

## 五、输出 schema 与落盘

落盘目标：`{project_path}/stage-outputs/01_case_truth_lock_DRAFT.md`。

更新该 Draft：

- Target Audience
- Teaching Goal
- Core Knowledge Points
- Fact–Knowledge Mapping
- Rejected/Deferred Teaching Angles
- User Decision Record

同步 state：`current_station=P3`、`next_station=P4`、`teaching_direction=APPROVED`、decision_id 和时间戳。

## 六、Hard Stop

教学方向属于人工高代价决策，必须 HARD。即使某个方案明显更优，也不允许自动进入 P4。

```text
╭─ 管理案例视频化事实规划器 · P3 完成 ─────╮
│ 👥 受众：{audience}
│ 🎓 教学目标：{goal_summary}
│ 🧠 知识点：{count}/3
│ 🔗 事实映射：{mapped_count}/{count}
│ ✅ 产出：{draft_absolute_path}
│ 📍 下一步：P4 · 视频化边界
│ 👉 Next 确认 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 七、反模式

- 不把知识点数量当信息量竞赛。
- 不使用无法从事实或明确理论解释支持的概念。
- 不替用户选择价值立场或案例解释方向。
- 不把抽象口号写成教学目标。
- 不提前决定传播钩子。

---

*P3 完成后，主控加载 `stages/04-dramatization-boundary.md`。*
