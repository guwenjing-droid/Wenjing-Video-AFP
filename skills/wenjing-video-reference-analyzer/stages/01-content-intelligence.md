# P1 · Content Intelligence

> 只回答讲了什么、面向谁、用什么信息支撑；不分析镜头或设计新故事。

## 执行

1. Read `modules/evidence-and-claim-policy.md` 与 `modules/content-intelligence-method.md`。
2. 提炼目标受众，并给出语言、知识门槛、问题意识等 Evidence Anchors。
3. 用 1–2 句提炼核心观点，区分主论点、铺垫和例证。
4. 构建信息逻辑链；每个分论点绑定数据、案例、政策或其他论据。
5. 标记 claim_type：`VIDEO_CLAIM | OBSERVATION | ANALYTIC_INFERENCE | EXTERNALLY_VERIFIED`。
6. 登记细分领域与视频自身明示的行业关联。外部知识不得混入本节。

## 完成标准

- 受众、核心观点、逻辑链、论据四项齐全或明确 NOT_OBSERVABLE。
- 每个事实性条目有锚；无法定位则 `ANCHOR_LIMITED` + 降低 confidence。
- 没有把视频主张冒充外部已核验事实。

## 输出 schema 与落盘

更新 `<reference_id>_DRAFT.md` 的 Content Intelligence 与 Evidence Anchors，更新 state。

## Hard Stop

```text
╭─ Reference Analyzer · P1 完成 ─╮
│ 受众 / 核心观点 / 逻辑链 / 论据
│ Evidence：PASS | REVIEW | BLOCK
│ 下一步：P2 Narrative Reverse Engineering
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────────╯
```

不自动进入 P2。

## 反模式

- 逐句摘要代替层级；把作者动机当事实；自动补企业/政策；无锚写“观众一定是”。

---
*P1 确认后加载 `stages/02-narrative-reverse-engineering.md`。*
