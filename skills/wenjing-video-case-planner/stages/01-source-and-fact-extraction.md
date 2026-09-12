# P1 · 来源登记与事实抽取

> wenjing-video-case-planner · Stage 01  
> 目的：建立 Source Registry，并从材料中抽取带锚点的事实候选。

## 一、本阶段边界

本阶段只登记来源并抽取候选 claim，不裁决矛盾，不锁定教学目标，不写叙事、剧本或镜头。

开始前 Read：

- `modules/evidence-classification.md`
- `modules/source-anchor-rules.md`
- `templates/case-truth-lock-template.md`

## 二、来源登记

为每份材料分配稳定 `source_id`：`SRC_001` 起顺序编号。记录：

- source_id、标题/描述、文件绝对路径或来源说明
- source_type：USER_FILE / USER_TEXT / PUBLIC_SOURCE / INTERNAL_NOTE
- 版本、日期或文件修改时间（可获得时）
- 是否为原始材料、二手解释或用户补充
- 可读状态与限制

用户口述内容必须标记 `USER_STATEMENT`，不能伪装成原文件内容。

## 三、事实候选抽取

1. 按来源顺序阅读；长材料分段处理，保留段落/页码/标题锚点。
2. 一条记录只表达一个可检验 claim。
3. 为候选分配 `FACT_001` 起的稳定 ID。
4. 记录原始措辞的忠实释义，不增加原文没有的因果、动机或评价。
5. 初分为 FACT / INTERPRETATION / INFERENCE / UNKNOWN；最终分类留给 P2。
6. 人物、组织、时间、地点、行为、结果、数量、制度条件分别抽取。

事实候选字段：

| 字段 | 要求 |
|---|---|
| fact_id | 稳定且唯一 |
| claim | 单一、清楚、可核对 |
| source_id | 必填 |
| source_anchor | 必填；格式见 module |
| provisional_class | 四类之一 |
| confidence | HIGH / MEDIUM / LOW |
| notes | 歧义、上下文或待核点 |

## 四、Evidence Chain 检查

- 没有 `source_id + source_anchor` 的候选不得进入核心 Fact Table。
- 同一 claim 有多来源时逐项列出，不用“多方资料显示”等模糊话。
- 外部常识或模型记忆不属于用户案例来源；需要时放入 `Proposed External Check`，不混入候选事实。
- 无法定位的内容进入 `Unanchored Claims`，等待 P2 处理。

## 五、输出 schema 与落盘

基于模板创建或增量更新：

`{project_path}/stage-outputs/01_case_truth_lock_DRAFT.md`

本阶段只填：Document Metadata、Source Registry、Candidate Fact Table、Unanchored Claims。未到阶段的章节保留 `PENDING`，不得提前补写。

同步更新 state：`current_station=P1`、`next_station=P2`、source_count、candidate_fact_count、unanchored_count。

## 六、Hard Stop

展示来源数量、事实候选数量、低置信/无锚点数量和 Draft 绝对路径。即使候选全部清楚，也不允许自动进入 P2。

```text
╭─ 管理案例视频化事实规划器 · P1 完成 ─────╮
│ 📚 来源：{source_count}
│ 🧾 事实候选：{fact_count}
│ ⚠️ 无锚点/低置信：{risk_count}
│ ✅ 产出：{draft_absolute_path}
│ 💾 状态：已写入 00_project_state.md
│ 📍 下一步：P2 · Truth Audit
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 七、反模式

- 不把全文摘要当作事实表。
- 不把作者观点自动升级为客观事实。
- 不删除与预期结论不一致的材料。
- 不因找不到页码就编造页码。
- 不在抽取阶段替用户选择教学方向。

---

*P1 完成后，主控加载 `stages/02-truth-audit.md`。*
