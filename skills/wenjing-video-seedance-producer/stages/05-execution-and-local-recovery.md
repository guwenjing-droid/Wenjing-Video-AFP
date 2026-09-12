# P5 执行与局部恢复

DRY_RUN 序列化最终请求并记录 `NOT_SUBMITTED`。为 v0.1 验收可额外执行无外部调用的 Mock 成败场景，状态只允许 `MOCK_SUCCEEDED|MOCK_FAILED`，并强制记录 `is_mock=true`、`media_generated=false`、`external_cost=0`。真实模式使用当前可用的 Seedance backend，提交前再次核对 request hash、能力档和授权；将 provider request id、状态、时间、输出路径/链接和错误码写入 manifest/log。

失败时只重试受影响 shot，且不超过 `max_generation_rounds`。身份/内容/连续性问题不在本阶段重写 Prompt，而是保留证据并路由 POSTGEN/上游；瞬时传输错误可按策略局部重试。

## 输出 schema

```json
{"results":[{"shot_id":"","request_id":"","status":"NOT_SUBMITTED|MOCK_SUCCEEDED|MOCK_FAILED|SUBMITTED|SUCCEEDED|FAILED","is_mock":false,"media_generated":false,"external_cost":0,"output_refs":[],"retries":0,"error":null}],"rerun_scope":{"from_checkpoint":"P3|P5","affected_artifacts":[],"unaffected_locked_artifacts":[]},"next_station":"P6"}
```

逐 attempt 追加写入 `{project_path}/stage-outputs/08_generation/generation_manifest.json` 与 `generation_log.md`。

╭─ Gate ─────────────────────────────────────────╮
│ HARD：禁止越权调用、无限重试或扩大重跑范围。  │
╰────────────────────────────────────────────────╯

Mock 返回不得写真实 provider request id、媒体 output refs 或 POSTGEN 视觉结论。Hard Gate 未满足也不允许自动推进。

*P5 后加载 P6。*
