# P6 · 报告锁定与接棒

## 边界
只冻结 QA 报告并更新路由；不调用 Producer 或执行返工。

## 执行
验证 P0–P5、evidence refs 和 issue 完整性。PREFLIGHT 写新的 `06_qa/preflight_report_v{n}.md`；RECHECK 必须递增 `{n}`，不得覆盖历史报告。POSTGEN 写 `06_qa/postgen_{shot_or_batch_id}_v{n}.md`；MOCK_POSTGEN 写 `06_qa/mock_postgen_{shot_or_batch_id}_v{n}.md`。每份报告记录 `supersedes`、`superseded_by`、`review_scope`、`affected_artifacts`；旧报告的 `superseded_by` 通过报告索引或 state 关系登记，不原地改写已锁定报告。计算报告 hash 并登记 state，另更新当前有效报告指针。GREEN PREFLIGHT 可接真实 Producer；DRY_RUN_GREEN 只接 Producer DRY_RUN；YELLOW/RED 或 POSTGEN issues 路由 owner_stage/人工。

## 输出 schema
报告必须含 mode、report_version、supersedes、superseded_by、review_scope、affected_artifacts、input integrity、observability、checks、issues、decision、producer_eligible、rerun_scope、created_at、report hash。

## Gate
```
╭─ Continuity Reviewer · P6 完成 ───────────╮
│ mode/decision：{mode}/{GREEN|DRY_RUN_GREEN|MOCK_PASS|MOCK_FAIL|YELLOW|RED}
│ report：{path} · hash：{值}
│ next：{Producer|人工|责任站复测}
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不覆盖旧报告；不让非 GREEN 进入 Producer；不在 POSTGEN 自动生成重试；不伪造 hash。

---
*P6 是最后一个阶段，完成后输出全流程交付确认单。*
