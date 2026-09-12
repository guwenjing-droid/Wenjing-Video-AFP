# P0 恢复与输入门禁

通过 Runtime Adapter 读取 manifest/state 的必要字段和当前 scope。验证 Storyboard 为 LOCKED、version/integrity 合法；Visual Bible 若被 Storyboard 选择则验证其 manifest/资产引用；从 state 的 `current_preflight_report_ref` 读取当前有效的 `preflight_report_v{n}`。只有不存在版本化报告且项目明确为 v1.0 兼容模式时，才回退旧 `06_qa/preflight_report.md`，不得覆盖或伪造历史报告。

真实模式只有 `decision: GREEN` 且 `producer_eligible: true`、报告输入 hash 与当前上游一致时可继续。DRY_RUN 可接受 `decision: DRY_RUN_GREEN` 且 `producer_eligible_for: DRY_RUN`。DRY_RUN_GREEN 不得升级到 PILOT/SHOT/BATCH。YELLOW、RED、PENDING、过期 hash、STALE 或缺失均 BLOCK；不得在 Producer 内修复或重审。

## 输出 schema

```json
{"input_status":"PASS|BLOCKED","selected_shots":[],"hashes":{},"preflight":{"decision":"","producer_eligible":false},"next_station":"P1|BLOCKED"}
```

更新 `{project_path}/00_project_state.md` 的输入快照与 P0 checkpoint。

╭─ Gate ─────────────────────────────────────╮
│ HARD：锁、完整性、当前模式对应 decision/eligible 全真。 │
╰────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P0 后加载 P1；BLOCKED 时只路由上游责任站。*
