# Project Contract

- 直接触发先读 `00_project_manifest.yaml`、`00_project_state.md` 与 `03_script_LOCKED.md`；缺 state/manifest 可按模板建最小壳，不依赖 Orchestrator。
- LOCKED 只读；变更走 `change-requests/CR-{id}.md`。DRAFT 与 LOCKED 必须并存。
- 每次落盘登记 path/version/SHA-256/time。上游变化只把依赖 shots/sequences 标 STALE。
- Continue 只读当前站必需依赖闭包，从最近合法 checkpoint 恢复，不重问已记录决定。
- FAST/GUIDED/STRICT 改变确认密度，不取消事实、Dialogue、资产与 Lock Hard Gate。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
