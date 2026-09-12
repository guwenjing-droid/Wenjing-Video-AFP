# P4 Pilot 与成本 Gate

按风险选择一个能覆盖主要角色、场景、对白/动作和参考资产的代表镜头作为 Pilot。记录已选 provider/model、分镜预算档、预计请求数、最大生成轮次、成本模式和停止条件。运行者必须看到当前选择的能力与成本证据；价格未知时写 `COST_UNKNOWN`，不把它排序成最便宜。FAST 可使用事先登记的低风险授权；GUIDED/STRICT 或高连续性、高成本请求必须显式确认。

在质量底线全部 PASS 时可推荐 `ECONOMY`；若低成本 profile 无法满足创作时长、画幅、Dialogue、参考资产、连续性或输出契约，必须从候选中排除，不能以低价绕过能力 Gate。成本估算使用映射后的实际生成档位与请求数，不用 creative duration 冒充计费参数；可裁切余量必须透明。

DRY_RUN 不发起外部调用，授权记录为 `NOT_REQUIRED`，外部成本固定记录为 0；v0.1 不等待 provider/model 可用性。BATCH 只能覆盖已逐镜 READY 且在授权 scope 内的请求。

## 输出 schema

```json
{"backend_selection":{"provider":"","model_id":"","cost_mode":"","cost_evidence":"KNOWN|COST_UNKNOWN","shot_budget_mode":"","selection_source":"USER|PREAUTHORIZED_POLICY"},"execution_plan":{"mode":"","pilot_shot_id":"","authorized_shots":[],"estimated_requests":0,"max_generation_rounds":null},"authorization":{"status":"NOT_REQUIRED|AUTHORIZED|DENIED|MISSING","evidence":""},"next_station":"P5|BLOCKED"}
```

落盘到 generation manifest 的 `cost_authorization` 与 execution plan，并更新 `{project_path}/00_project_state.md`。

╭─ Gate ─────────────────────────────────────╮
│ HARD：所有有成本外部调用必须在授权范围内。│
╰────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P4 后加载 P5。*
