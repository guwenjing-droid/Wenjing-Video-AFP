# Project Contract

## 逻辑 Artifact 引用

- Manifest：`00_project_manifest.yaml`
- State：`00_project_state.md`
- Storyboard：`stage-outputs/05_storyboard_LOCKED.json`
- 条件资产：`stage-outputs/04_visual_bible/asset_manifest_LOCKED.yaml`
- PREFLIGHT：由 state 的 `current_preflight_report_ref` 指向 `stage-outputs/06_qa/preflight_report_v{n}.md`；旧 `preflight_report.md` 仅作 v1.0 兼容输入
- Prompt：`stage-outputs/07_model_prompts/seedance/<shot_id>_LOCKED.md`
- 生成事实：`stage-outputs/08_generation/generation_manifest.json`
- 人读日志：`stage-outputs/08_generation/generation_log.md`

## Lock 与 CR

上游 hash 变化时，本件 Prompt/请求/输出的依赖后代标记 STALE，停止新增成本。Producer 不解锁上游；需要改 Script/Storyboard/资产时创建 CR 并路由属主。自己的 DRAFT 可编辑，已提交请求不可覆写历史记录，只能追加新 attempt。

## Continue

通过 Adapter 解析 state 登记的 content_ref 并校验完整性，选择最近合法 checkpoint。状态与可观察 Artifact 冲突时标 FAIL/BLOCKED 并记录恢复差异，不得静默修正或从聊天记忆臆测已授权/已提交。

## Runtime efficiency

记录 `route_decision`、`selected_artifact_paths`、`reuse_decisions`、`rerun_scope` 和 `cost_policy`。只处理当前 shot/batch；无关锁定物不重读、不重建。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
