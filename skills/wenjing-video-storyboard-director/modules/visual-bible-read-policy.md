# Visual Bible Read Policy

先从 project manifest 判定 `NOT_SELECTED | OPTIONAL_SELECTED | REQUIRED`：

- NOT_SELECTED：不加载 Visual Bible，asset binding 标 `TEXT_ONLY`；若下游连续性风险要求资产则 BLOCK 并升级为 REQUIRED。
- OPTIONAL_SELECTED/REQUIRED：只读 `asset_manifest_LOCKED.yaml` 中当前 shots 用到的条目与文件。

真实生产引用必须同时满足 manifest LOCKED、item READY、path 存在、完整性校验码匹配、依赖 READY、无相关 CR，并只记录到 `asset_refs`。

当 `acceptance_profile=V0_1_DRY_RUN` 时，可消费 LOCKED manifest 中 `dry_run_readiness=READY` 的规格，但只能记录到 `planned_asset_refs`，字段为 `asset_id/spec_path/purpose/real_media_status=DEFERRED`；不得填写真实媒体 path/hash，也不得放行真实生成。失败按 asset 影响到的 shots 局部传播 STALE。
