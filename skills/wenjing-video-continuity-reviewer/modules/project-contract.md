# Project Contract

- 直接触发先读 manifest/state；缺失可建最小壳，只写 Reviewer 字段。
- LOCKED 输入只读；变更走 CR。报告按 mode/id/version 独立落盘，不覆盖历史。
- Continue 从最近合法 checkpoint 按需恢复；旧报告仅在所有 input/evidence hash 未变时复用。
- 局部变更只重审 affected shots/batch 与 continuity neighbors。
- FAST/GUIDED/STRICT 不改变 required checks；任何“忽略检查强制继续”均非法。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
