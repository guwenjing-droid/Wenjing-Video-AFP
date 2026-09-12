# Project Contract

固定文件：`00_project_manifest.yaml`、`00_project_state.md`、`stage-outputs/01_case_truth_lock_LOCKED.md`、`02_narrative_plan_LOCKED.md`、`03_script_DRAFT.md`、`03_script_LOCKED.md`、`change-requests/`。

生命周期 `DRAFT → APPROVED → LOCKED`；状态 `READY | MISSING | STALE | BLOCKED`。下游只读 LOCKED，SHA-256 冻结后只登记 manifest/state。LOCKED 不原地覆盖；变更走 CR，上游重开则依赖 Script 标 STALE。

`Continue {absolute_path}` 按 manifest → state → locks → CR 恢复，列四态和 next_station，不依赖对话摘要。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
