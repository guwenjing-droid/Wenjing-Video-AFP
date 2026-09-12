# P4 · 视频化边界

> wenjing-video-case-planner · Stage 04  
> 目的：界定下游可以怎样戏剧化、哪些内容需要条件确认、哪些绝对不能改。

## 一、本阶段边界

本阶段只建立改编边界和初步叙事模式建议，不写最终钩子、剧情、台词、角色造型、分镜或模型 Prompt。

## 二、改编边界分类

依据 Fact Table 和教学方向，把可能的改编动作分为：

### ALLOWED

通常可做但必须记录：压缩重复信息、合并非关键时间段、用视觉隐喻表达抽象概念、调整讲述顺序但不改变因果。

### CONDITIONAL

必须逐项说明条件并由用户确认：合成人物、匿名化、对话重构、时间压缩、场景替换、把隐含动机外化为动作或旁白。

### FORBIDDEN

不得改变或发明：核心人物身份与关系、关键行为、关键时间顺序、因果、数量、制度条件、结果，以及影响教学结论的事实。

不能机械套用上述类别；必须结合本案例逐条写成可检查规则，并引用相关 fact_id。

## 三、初步叙事模式建议

只输出 2–3 个“路线建议”，供下游 Narrative Designer 使用：

- SCQA 案例冲突型
- 问题—决策—后果型
- 共鸣观察/日常困境型
- 对比或复盘型

每个建议包含：适配的教学目标、可用事实、风险、禁止跨越的边界。不得产出最终开头、情绪曲线或台词。

## 四、边界完整性检查

- 每条 FORBIDDEN 对应 fact_id 或明确的教学约束。
- 每条 CONDITIONAL 有批准者、条件和记录位置。
- ALLOWED 不得隐含改变事实强度或因果。
- 知识点植入位置只做上游建议，不替 Narrative 决定节奏。
- 若材料是真实人物/组织案例，明确匿名、声誉和敏感信息风险。

## 五、输出 schema 与落盘

落盘目标：`{project_path}/stage-outputs/01_case_truth_lock_DRAFT.md`。

更新该 Draft：

- Dramatization Space：ALLOWED / CONDITIONAL / FORBIDDEN
- Forbidden Fabrication List
- Sensitivity and Anonymization Notes
- Initial Narrative Mode Suggestions
- Downstream Guardrails

同步 state：`current_station=P4`、`next_station=P5`、conditional_decision_count、boundary_status。

## 六、Hard Stop

展示最重要的允许项、条件项和禁止项；要求用户确认条件项。即使没有条件项，也不允许自动进入 P5。

```text
╭─ 管理案例视频化事实规划器 · P4 完成 ─────╮
│ ✅ ALLOWED：{allowed_count}
│ 🟡 CONDITIONAL：{conditional_count}
│ ⛔ FORBIDDEN：{forbidden_count}
│ 🧭 叙事路线建议：{mode_count}
│ ✅ 产出：{draft_absolute_path}
│ 📍 下一步：P5 · Draft 审阅
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 七、反模式

- 不把“可戏剧化”理解为可以补写关键事实。
- 不用合成人物掩盖因果变化。
- 不把路线建议写成成品叙事。
- 不只写“忠于原文”而缺少可检查的禁止项。
- 不忽略真实人物、组织和未成年人等敏感风险。

---

*P4 完成后，主控加载 `stages/05-draft-review.md`。*
