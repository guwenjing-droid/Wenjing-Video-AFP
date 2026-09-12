# P1 后端、能力与模式解析

先读取 manifest/state 的 `generation_backend_choice`，只展示当前已登记、已验证且有兼容 Producer 的候选；候选至少包含 provider、model/profile、能力适配、成本单位或 `COST_UNKNOWN`、预计请求数、质量/连续性风险和 producer 名称。运行者可选择 `ECONOMY | BALANCED | QUALITY_FIRST`，或使用已有的明确预授权。

若选中 Seedance，再按 `modules/seedance-capability-profile.md` 读取当前 profile，解析 `DRY_RUN | PILOT | SHOT | BATCH`。真实调用要求 profile 为 `VERIFIED_CURRENT` 且来源、验证时间、模型 ID、支持参数和限制可定位；无法确认时降级 DRY_RUN 或 BLOCK，不猜测。

若选中非 Seedance，本 Skill 只写 `ROUTE_TO_COMPATIBLE_PRODUCER` 并停止。目标 Producer 已安装且接口兼容时交还路由层点将；缺少时写 `BACKEND_ADAPTER_MISSING`。禁止为了继续而强制回落 Seedance。

为每个 shot 建立 capability mapping。读取 `creative_required_duration`，若 profile 提供离散档位，选择不短于创作需求的最小时长档并记录 `selected_generation_duration` 与 `trim_surplus_seconds`；若支持连续区间则在合法精度内映射。无足够档位时写 `SPLIT_REQUIRED` 并回 Storyboard Director，禁止向下 clamp 或把 10s/12s/15s 设为统一默认。Storyboard 要求超出能力时记录 mismatch，不偷偷改镜头或参数。

## 输出 schema

```json
{"backend_selection":{"selection_mode":"OPERATOR_CHOICE|AUTO_COST_AWARE","status":"SELECTED|PENDING|ROUTE_REQUIRED|BACKEND_ADAPTER_MISSING","selected_provider":"","selected_model":"","selected_producer":"","cost_mode":"ECONOMY|BALANCED|QUALITY_FIRST","candidates":[],"fallback_policy":"ASK_OPERATOR|DRY_RUN_ONLY"},"run_mode":"","profile_status":"","model_id":"","supported":[],"duration_mappings":[{"shot_id":"","creative_required_duration":0,"selected_generation_duration":0,"mapping":"EXACT|ROUND_UP_AND_TRIM|SPLIT_REQUIRED","trim_surplus_seconds":0}],"mismatches":[],"next_station":"P2|ROUTE|BLOCKED"}
```

落盘到 `{project_path}/stage-outputs/08_generation/generation_manifest.json` 的 DRAFT `inputs.capability_profile`，并更新 state。

╭─ Gate ─────────────────────────────────────────╮
│ HARD：运行者/预授权先选后端与成本档；Seedance   │
│ 真实调用须 VERIFIED_CURRENT；非 Seedance 路由。 │
╰────────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P1 后加载 P2。*
