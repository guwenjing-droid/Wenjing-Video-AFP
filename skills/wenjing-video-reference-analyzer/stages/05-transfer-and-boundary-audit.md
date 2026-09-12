# P5 · Transfer Engine & Boundary Audit

> 只把分析抽象为候选迁移规则并完成边界审计；不把规则应用成最终 Narrative 或剧本。

## 执行

1. Read `modules/transfer-originality-and-limitations.md`。
2. 从 P1–P4 提议候选 Transfer Rules。每条含稳定 ID、mechanism、source_layer、anchors、confidence、transferable_to、source-specific、do-not-copy、originality risk、conditions。
3. 给出 2–3 种迁移强度：A 只取抽象原则；B 重组结构功能；C 若接近原组合则标高风险并阻断。用户选择不等于通过 Gate。
4. 分离不可迁移的原视频事实、独特表达、角色、事件顺序、段落与镜头组合。
5. 完成 Objectivity & Limitations：偏向、信息完整性、数据时效、样本、论证跳跃、未观察模态、适用场景。
6. External Supplements 默认 `NONE`；若用户提供或明确要求补充，必须单独列来源、日期、核验状态，不能写成原视频内容。
7. 运行 G-RA-01 Input Modality、G-RA-02 Observability、G-RA-03 Original Transfer 全审计；任何 BLOCK 规则设为 EXCLUDED，不进入可采用清单。

## 完成标准

- 规则能脱离原主题表达并保留功能原理。
- source_specific_elements 和 do_not_copy 非空时均有对应隔离动作。
- HIGH risk 不得以 Review 放行；MEDIUM 必须人工确认改造程度。
- DRAFT 九区完整，缺失内容有明确状态。

## 输出 schema 与落盘

完成 `<reference_id>_DRAFT.md`，更新 reference manifest/state 和 Gate 记录。

## Hard Stop

```text
╭─ Reference Analyzer · P5 完成 ─╮
│ 候选规则 / EXCLUDED / limitations
│ G-RA-01/02/03：PASS | REVIEW | BLOCK
│ 下一步：P6 Lock & Handoff
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────────╯
```

不自动进入 P6。不得 Skip。

## 反模式

- 换词仿写；把独特顺序称为模板；省略禁复制项；外部资料污染观察；用用户同意覆盖 HIGH risk。

---
*P5 确认后加载 `stages/06-lock-and-handoff.md`。*
