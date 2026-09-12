# P2 · Truth Audit

> wenjing-video-case-planner · Stage 02  
> 目的：把事实候选审成可继承的事实集，并显式保留矛盾、缺口和未知。

## 一、本阶段边界

本阶段只审核事实与证据关系，不确定教学目标，不做戏剧化设计，不写最终叙事。

开始前 Read `modules/evidence-classification.md`、`modules/source-anchor-rules.md`；用户要求外部核实时再 Read `modules/external-verification-boundary.md`。

## 二、逐项审核

对每个候选执行：

1. **可溯源性**：anchor 是否真的支持该 claim，而非只提到相同主题。
2. **分类**：确定为 FACT / INTERPRETATION / INFERENCE / UNKNOWN。
3. **粒度**：一个事实是否混入多个判断；必要时拆分并保留 ID 关联。
4. **一致性**：检查人物、时间、地点、数量、行为、结果和因果是否互相冲突。
5. **措辞强度**：原文只说“可能”时不得改成确定结论。
6. **核心性**：标记 CORE / SUPPORTING / CONTEXT，不因非核心就删除证据链。

## 三、矛盾与缺口

每个问题分配 `ISSUE_001` 起的 ID，记录涉及 fact/source、问题、风险和可选处理：

- 方案 A：保留为 UNKNOWN，禁止下游当事实使用——最稳妥，但叙事可用信息减少。
- 方案 B：请用户提供补充来源或裁决——证据更完整，但当前流程暂停。
- 方案 C：从核心事实集中排除，仅保留在争议记录——可继续，但不能围绕它设计关键情节。

只有用户能裁决材料无法自行解决的关键冲突。系统应给建议和代价，不代替用户拍板。

## 四、外部核验边界

- 默认只审核用户给定材料内部的一致性。
- 用户明确要求核实，或核心事实影响现实人物/组织声誉、法律/医疗/财务判断时，必须另行核验。
- 外部核验结果使用新的 source_id，并明确与原案例材料的关系。
- 核验失败写 `UNVERIFIED`，不得伪装为 PASS。

## 五、输出 schema 与落盘

落盘目标：`{project_path}/stage-outputs/01_case_truth_lock_DRAFT.md`。

更新该 Draft：

- Final Fact Table
- Interpretations
- Inferences
- Unknowns
- Unresolved Issues
- Excluded Claims
- Truth Audit Summary

同步更新 state：`current_station=P2`、`next_station=P3`、`truth_audit=PASS|REVIEW_REQUIRED|BLOCKED`、未决 issue 数。

有核心问题未裁决时，`next_station` 保持 P2，状态为 BLOCKED。

## 六、Hard Stop

若存在 issue，先展示选项与影响；无论是否存在 issue，本阶段都必须停止等待确认。

```text
╭─ 管理案例视频化事实规划器 · P2 完成 ─────╮
│ ✅ 核心事实：{core_count}
│ 📝 解释/推断：{nonfact_count}
│ ⚠️ 未决问题：{issue_count}
│ 🚦 Truth Audit：{status}
│ ✅ 产出：{draft_absolute_path}
│ 📍 下一步：{P2 继续裁决 | P3 教学目标锁定}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 七、反模式

- 不通过“最合理解释”静默解决矛盾。
- 不把多个弱来源相加当成强证据。
- 不用外部常识覆盖用户材料。
- 不为保持故事顺畅删除 UNKNOWN。
- 不把 Truth Audit PASS 等同于“现实世界绝对真实”。

---

*P2 放行后，主控加载 `stages/03-teaching-lock.md`。*
