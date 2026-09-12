# Seedance Capability Profile

模型能力会变化，运行时必须使用可审计 profile，不从旧 Prompt 或记忆推断。

本 profile 只证明某个 Seedance 候选的当前能力与成本证据，不证明 Seedance 是系统唯一或最便宜的后端。跨 provider 比较由 manifest/state 的 `generation_backend_choice` 汇总；本 Skill 不读取或解释不属于自己的模型字段。

## 必需字段

- provider、model_id、model_version/profile_version
- status：`VERIFIED_CURRENT | SYNTHETIC_TEST | STALE | UNRESOLVED`
- source 与 verified_at
- duration 模式（`DISCRETE_TIERS|CONTINUOUS_RANGE`）、合法档位/范围/精度、裁切支持，以及 aspect_ratio、resolution、quality、audio、reference inputs、request mode 的支持范围
- reference count/size/order semantics 和已知限制
- cost unit 或 `UNKNOWN`、rate limit、output contract
- profile_sha256

## 路由

- 真实调用：只接受 `VERIFIED_CURRENT`。
- DRY_RUN 测试：可接受明确标记的 `SYNTHETIC_TEST`，输出不得提交。
- STALE/UNRESOLVED：不猜测；请求更新 profile 或保持 DRY_RUN_BLOCKED。
- Storyboard `creative_required_duration` 映射：选择最小且足够的合法档；多余部分登记裁切。无足够档位返回 `SPLIT_REQUIRED`，不向下 clamp。
- Storyboard 要求与能力冲突：记录 mismatch 并路由用户/上游决策，不静默降级。
- cost 为 `UNKNOWN` 时：标 `COST_UNKNOWN`，不得参与“最低成本”自动排序；仍可由运行者在明确未知的前提下选择。
