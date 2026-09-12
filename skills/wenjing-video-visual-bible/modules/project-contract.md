# Project Contract

## 最小项目壳

直接触发时先查 `00_project_manifest.yaml`、`00_project_state.md` 和 `stage-outputs/03_script_LOCKED.md`。manifest/state 缺失时可按 templates 建最小壳，只填本件所需字段；不得假设 Orchestrator 已运行。

## 状态与锁

- 状态：`DRAFT | APPROVED | LOCKED | READY | MISSING | STALE | BLOCKED`。
- LOCKED 只读；修改走 `change-requests/CR-{id}.md`。
- 每次写文件后登记版本、绝对或项目相对路径、SHA-256 与时间。
- 上游变更时只把受影响资产及依赖后代标 STALE；其他锁定资产保留。

## 最短路径与恢复

只读当前 Stage 的必需依赖闭包和 manifest 明确选择的资产。Continue 先从 state 重建 HUD，验证最近 checkpoint；不重问已记录决策，不默认重读历史素材，不重建仍兼容的 READY 资产。

## Gate

Hard Gate 永不取消；FAST/GUIDED/STRICT 只改变 REVIEW 密度。外部生成、成本、品牌/IP 与核心身份方向按项目风险执行 Gate。空字段不等于授权。

## v0.1 Dry Run 验收档

当 manifest 明确 `acceptance_profile: V0_1_DRY_RUN` 时，真实资产生成不属于本次验收。规格完整的资产保持 `status=SPEC_READY_ASSET_MISSING`，另写 `dry_run_readiness=READY` 与 `real_media_readiness=DEFERRED`。该状态只允许规格级 Visual Bible 接棒，不允许任何真实生成路径把它解释为实际 `READY`。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
