# PREFLIGHT Checks

1. Artifact lock/schema/integrity 与 open CR：本地文件系统且 hash 可用时必须 `VERIFIED`；无 hash 能力时为 `NOT_OBSERVABLE`，V0_1_DRY_RUN 不因此自动 BLOCK，STRICT/REAL PRODUCTION 可要求 `VERIFIED`；`FAIL` 必须 BLOCK，禁止伪造 SHA-256；
2. Script/Dialogue/VO/knowledge coverage；
3. 真实轨检查 required assets 存在、READY、完整性状态、用途和依赖；`V0_1_DRY_RUN` 检查 planned asset specs 与 `dry_run_readiness=READY`，并把真实媒体检查标 DEFERRED；同时独立复核 required asset binding closure 和每个 ref 的单一 canonical asset_id；
4. 角色数量/身份/服装/站位、场景/光线/道具状态；
5. Duration Sanity Check：
   - 每镜必须有 `estimated_duration`、`creative_required_duration`、`duration_basis` 与 `duration_driver`，兼容 `duration_seconds` 不得与 creative 值冲突；
   - 异常大量完全等长镜头且内容依据不同 → YELLOW；若来自固定 10s/12s/15s 默认或缺少逐镜依据 → RED；
   - `speech_time > creative_required_duration` → RED；
   - 复杂顺序 action atoms、长运镜或多角色调度明显无法完成 → RED；
   - 极短信息/插入/反应镜头异常冗长 → YELLOW，除非 comprehension/camera/transition 依据充分；
   - 超过创作单镜上限却被 clamp、未拆镜 → RED；
   - Storyboard 不得包含后端时长档，Producer 映射必须保持待处理状态。
6. 总时长、比例、音频策略与项目约束；
7. Action atoms、入口/出口、轴线/视线/transition 连续；
8. Producer 所需约束可映射，但本报告不编写模型 Prompt 或调用参数。

真实轨所有 required PASS 才 `decision=GREEN, producer_eligible=true`。Dry Run 轨所有规格、覆盖和边界检查 PASS 时写 `decision=DRY_RUN_GREEN, producer_eligible_for=DRY_RUN`。纯文字不能补偿真实生产所需资产，也不得把 DRY_RUN_GREEN 用于 PILOT/SHOT/BATCH。
