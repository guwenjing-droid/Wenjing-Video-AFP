# Integration Guide

- 类型：Pattern 5 Independent；partner `wenjing`；契约 v0.1.0。
- PREFLIGHT 输入：Script LOCKED + Storyboard LOCKED + 条件性 Visual Bible；输出版本化 `06_qa/preflight_report_v{n}.md`，state 登记 current report ref 与 supersession 关系。
- POSTGEN 另需 generation manifest 与实际媒体证据；输出 `postgen_{id}.md`。
- 只有 `mode=PREFLIGHT, decision=GREEN, producer_eligible=true` 可接棒 Producer。
- YELLOW/RED 路由到 issue.owner_stage；Reviewer 不修改、不生成。
- 状态只写本件报告、evidence、decision、issues、rerun_scope 与 next_station。
