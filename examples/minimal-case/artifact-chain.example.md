# Expected Artifact Chain

1. Case Truth Lock：只包含已提供案例中可验证的行为、结果与知识边界。
2. Narrative Plan LOCKED：用冲突和决策点组织事实，不新增结果。
3. `03_script_LOCKED.md`：锁定逐字对白、旁白与动作。
4. Visual Bible / Storyboard：建立可追溯视觉规范和逐镜计划；每镜动态推导 creative duration，不套统一 12 秒。
5. PREFLIGHT：完成 Duration Sanity 后签发 `DRY_RUN_GREEN`。
6. Producer：把 creative duration 映射为后端最小充分档，输出 Prompt、参数、资产清单和 generation plan，`external_calls: 0`。
7. Mock POSTGEN：只验证返回、状态与恢复，不评价真实视听质量。
