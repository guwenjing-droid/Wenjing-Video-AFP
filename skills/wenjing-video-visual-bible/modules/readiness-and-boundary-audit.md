# Readiness & Boundary Audit

## Readiness 状态机

真实资产状态仍为 `SPEC_MISSING → SPEC_READY_ASSET_MISSING → ASSET_GENERATED_UNREVIEWED → READY`。任一上游/文件失效可转 `STALE`；无法合法继续为 `BLOCKED`。禁止跨级。

`V0_1_DRY_RUN` 另有不冒充真实媒体的验收字段：规格完整时写 `dry_run_readiness=READY`，同时保留 `status=SPEC_READY_ASSET_MISSING` 和 `real_media_readiness=DEFERRED`。

## READY 判定

每个 required item 必须同时满足：

1. spec 完整且有 Script provenance；
2. 所列文件真实存在、可读、类型正确；
3. 每个文件 SHA-256 与 manifest 一致；
4. style/identity/wardrobe/space/prop-state 检查通过；
5. source/rights/version 可审计；
6. 所有 required dependencies READY；
7. 无影响本项的开放 CR。

## 边界扫描

Visual Bible 产物不得含逐镜镜号、镜头时长、景别/运镜调度、Seedance 参数/Prompt、视频生成调用或改写的剧情/台词。出现这些字段必须 RED 并删除越界内容，必要时写 CR。

## 双轨报告

readiness report 列每项 `PASS/FAIL/NOT_APPLICABLE/DEFERRED`、证据路径和最小补救动作：

- `REAL_GREEN`：满足全部实际 READY 条件，可服务真实生产；
- `DRY_RUN_GREEN`：规格、来源、边界、planned references 全部通过，真实文件检查为 DEFERRED；只服务 v0.1 Dry Run；
- `YELLOW`：仍有需人工或非关键缺口；
- `RED`：必需规格、边界或来源失败，立即 BLOCK。

`DRY_RUN_GREEN` 可以锁规格级 manifest，但不得被下游解释为真实资产 GREEN。
