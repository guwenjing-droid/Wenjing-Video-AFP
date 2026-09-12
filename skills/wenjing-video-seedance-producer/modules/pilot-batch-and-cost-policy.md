# Pilot Batch and Cost Policy

## 模式

- DRY_RUN：零外部调用；验证序列化请求、Prompt/参数/参考顺序和日志 schema。
- PILOT：一个代表 shot；用于验证关键连续性和模型适配。
- SHOT：指定一个或少量 shot 的逐镜生成。
- BATCH：多个已 READY 的 shot；必须在授权 scope 内。

## Pilot 选择

优先覆盖主要角色身份、关键场景、对话/动作难点、最多参考资产或最高连续性风险。选择理由写入 manifest，不默认选第一镜。

## 授权

授权必须含 mode、shot/batch scope、最大请求/轮次、有效期或当前 turn 证据。空字段不是授权。FAST 的预授权也必须在 manifest/state 中可定位；STRICT 的 Pilot 为 HARD。

## 成本感知

先复用合法资产和成功输出；满足质量前提下选更少请求与更少重试的方案。超过上限、扩大 scope 或切换更高成本 profile 必须重新授权。

## 运行者选择与质量底线

- 真实生成前展示 `ECONOMY / BALANCED / QUALITY_FIRST`，并列 provider/model、能力适配、成本证据、预计请求数和风险。
- `ECONOMY` 只能在 Storyboard、Dialogue、Knowledge、Action Clarity、Continuity 与当前 profile 能力全部 PASS 时推荐。
- 成本单位、积分或价格无法由当前 profile/来源核验时标 `COST_UNKNOWN`；不得伪造价格、跨平台换算或“最便宜”结论。
- Storyboard 已选 `shot_budget_policy` 是预计请求数的基础；Producer 不自行删镜、合镜或改变镜头内容。
- 成本估算使用 `selected_generation_duration`；优先最小且足够的合法档并裁切冗余，不得用更短档损害表达，也不得无理由统一上调到 12 秒。
- 选择非 Seedance 时，本 Skill 不执行；返回兼容 Producer 路由或 `BACKEND_ADAPTER_MISSING`。
