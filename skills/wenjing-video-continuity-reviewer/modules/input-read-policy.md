# Input Read Policy

PREFLIGHT 必需 Script LOCKED、Storyboard LOCKED；Visual Bible 按 Storyboard/manifest 条件需要。POSTGEN 另需 generation manifest 与实际输出证据。MOCK_POSTGEN 需明确 `is_mock=true` 的 generation manifest 和模拟结果记录，不得要求或假设真实媒体存在。

通过 Runtime Adapter 逐项解析 `content_ref`，校验 version/status/integrity。具备本地文件系统与 SHA-256 能力时必须复算并匹配，结果写 `VERIFIED`；不具备 hash 能力时保留 `sha256` 字段为空并写 `NOT_OBSERVABLE`，禁止伪造。预期值与可观察实际值不符写 `FAIL` 并 BLOCK，Reviewer 不代替 owner 修复。

真实轨只读取当前 shot/batch 的 Artifact slices、READY assets、Prompt/parameter record 与媒体证据；required asset 非 READY 时 BLOCK。`V0_1_DRY_RUN` 可读取规格级 `planned_asset_refs`，且 `NOT_OBSERVABLE` 不自动 BLOCK，但只能形成 `DRY_RUN_GREEN` 并放行 DRY_RUN。STRICT 或 REAL PRODUCTION 可把 `integrity_status=VERIFIED` 设为必需。DRAFT、STALE、缺失或 `FAIL` 始终 BLOCK。
