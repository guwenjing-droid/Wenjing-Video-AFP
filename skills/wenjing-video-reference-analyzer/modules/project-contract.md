# Project Contract

## 逻辑 Artifact 引用

```text
00_project_manifest.yaml
00_project_state.md
change-requests/
stage-outputs/00_reference_analysis/
  reference_analysis_manifest.yaml
  <reference_id>_DRAFT.md
  <reference_id>_LOCKED.md
```

直接触发时，若 manifest/state 不存在，只按模板建立最小项目壳；不得伪造输入文件、Truth Lock 或未来下游产物。

## 生命周期与四态

- 分析：`DRAFT → APPROVED → LOCKED`。
- 资产：`READY | MISSING | STALE | BLOCKED`。
- 下游只读 LOCKED；hash 必须重算并与 manifest/state 一致。
- LOCKED 变更写 `change-requests/CR-{id}.md`，生成新版本，不原地覆盖。
- 输入材料被替换或重开时，本分析及已采用它的下游标 STALE。

## Continue

读取 manifest → state → reference manifest → LOCKED/DRAFT → open CR，列出四态、Gate 和 next_station。不得只依赖对话摘要，也不得重问已经锁定的信息。

## Gate 记录

每次写盘记录 station、decision、actor、time、affected files。Hard Gate 未过不得越阶；Back 不删除文件，只回 checkpoint 并传播 STALE。

## Portable Runtime v1.1

manifest/state 中每个 Artifact 条目至少包含 `artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`sha256`、`integrity_status`、`upstream_refs`、`upstream_integrity`、`approved_by`、`updated_at`。旧 `path/locked_path` 只作兼容别名。`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`：本地 hash 可用时必须复算匹配；不可用时保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

`content_ref` 是逻辑引用，由 `LOCAL_FILE` 或 `DOCUMENT_BOARD` Adapter 解析。业务层不得假设绝对路径或固定分隔符。文件能力顺序为平台原生工具 → 可选 Python → Adapter；shell 不是必需能力。
