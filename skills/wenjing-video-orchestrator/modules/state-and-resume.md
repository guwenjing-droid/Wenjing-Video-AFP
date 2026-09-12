# State and Resume

固定状态文件为 `{project_path}/00_project_state.md`，固定项目清单为 `00_project_manifest.yaml`。

Continue 顺序：读取两文件 → 只验证当前站的依赖闭包 → 比较登记与实际文件 → 定位首个 MISSING/STALE/BLOCKED → 写唯一 next_skill 和 resume prompt。有效 LOCKED 文件不得重算。

局部失败只写 `rerun_scope.from_checkpoint/affected_artifacts/unaffected_locked_artifacts`。只有根依赖变化才传播到全部后代；总控不替 owner 修复。

项目目录比聊天记忆优先。状态冲突时保留证据、标 BLOCKED 并点将责任 Skill。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`。

`content_ref` 由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。Local File 在 SHA-256 可用时必须复算；Document/Board 无 hash 能力时保留空 `sha256` 并写 `NOT_OBSERVABLE`。业务 Skill 不假设绝对路径、固定分隔符或 shell。状态比较以逻辑 Artifact 身份、版本、锁与完整性语义为准。
