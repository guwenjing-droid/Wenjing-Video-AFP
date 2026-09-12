# Generic Agent Platform Adapter

## 能力盘点

迁移前确认目标平台是否具备：多 Agent/节点、持久文件或对象、结构化状态、人工审批、条件路由、版本/哈希、局部重试、外部 Tool 权限和成本控制。缺失能力必须用显式人工步骤或外部存储补齐。

## 最小映射

1. 以 [../manifest.yaml](../manifest.yaml) 注册 12 个逻辑组件。
2. 以 [../contracts/artifact-contracts.md](../contracts/artifact-contracts.md) 建立输入输出 schema。
3. 以 [../contracts/routing-contract.md](../contracts/routing-contract.md) 建立四条路线和可选参考分支。
4. 以 [../contracts/gate-policy.md](../contracts/gate-policy.md) 实现 Hard/Review/Auto Gate。
5. 以 [../contracts/state-resume-rules.md](../contracts/state-resume-rules.md) 实现 checkpoint 和最小范围恢复。
6. 把每个 Skill 的 `SKILL.md` 及其相对依赖映射为独立 Agent/Workflow 指令。
7. 根据能力选择 `runtime/local-file-adapter.md` 或 `runtime/document-board-adapter.md`，不要把平台逻辑写进业务 Skill。

## Adapter 必须保证

- 输入不可观察信息不会被猜测；
- 真值与用户约束优先于参考迁移；
- 只有合法 LOCKED 上游可以接棒；
- Dry Run 和 Real Tool 权限隔离；
- 路由可审计，失败可局部重跑；
- 平台专用字段不会污染平台无关 Artifact 内容。
- canonical skill id 不含版本后缀；版本来自 metadata/manifest。
- 无 hash 能力时显式 NOT_OBSERVABLE，报告按版本新增而非覆盖。

如果平台只能运行单 Agent，应在一次执行中模拟独立节点与 Artifact Gate，但仍需保存各阶段独立输出，禁止把所有职责压成一个不可审计回答。
