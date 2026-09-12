# P6 Manifest 日志与接棒

写 `08_generation/generation_manifest.json` 和 append-only `generation_log.md`；记录输入/Prompt hash、reference 顺序、模型参数、授权、请求、输出、重试与局部恢复范围。更新 `00_project_state.md` 的 checkpoint 和 next station。

实际输出存在且可定位时，按 shot/batch 请求 Reviewer POSTGEN；普通 DRY_RUN 标记接口验证完成。含 Mock 成败的 v0.1 DRY_RUN 可接 Reviewer MOCK_POSTGEN 验证状态、局部重跑与恢复，但不生成视觉 PASS。

## 输出 schema

```json
{"manifest_status":"DRY_RUN_VALIDATED|MOCK_VALIDATED|PARTIAL|COMPLETE|BLOCKED","generated_shots":[],"postgen_ready_shots":[],"mock_qa_ready_shots":[],"next_station":"WAITING_FOR_REAL_PILOT|wenjing-video-continuity-reviewer:MOCK_POSTGEN|wenjing-video-continuity-reviewer:POSTGEN|BLOCKED"}
```

最终落盘路径为 `{project_path}/stage-outputs/08_generation/generation_manifest.json`、`generation_log.md` 与更新后的 `{project_path}/00_project_state.md`。

╭─ Gate ───────────────────────────────────────╮
│ HARD：manifest 与 log 一致；无实际输出不得冒 │
│ 充生成或 POSTGEN 证据。                       │
╰──────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P6 是最后一个阶段；完成后仅接棒或等待授权。*
