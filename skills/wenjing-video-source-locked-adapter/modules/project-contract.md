# Project Contract

使用既有 manifest/state 状态：MISSING、DRAFT、READY、APPROVED、LOCKED、STALE、BLOCKED。每次写盘登记 path、version、SHA-256；LOCKED 不回写 hash。变更写 CR，生成新版本并只把依赖后代标 STALE。恢复从最近合法检查点开始。

最短路径只读取本 Stage 必需依赖。Source/Adaptation/Script 三个正式锁依次位于 `stage-outputs/01_source_lock_LOCKED.md`、`02_adaptation_plan_LOCKED.md`、`03_script_LOCKED.md`。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
