# wenjing-video-seedance-producer

AFP 视频生产系统核心主链第 7 件 Independent Skill。它把 GREEN PREFLIGHT 放行的 LOCKED Storyboard 编译为逐镜 Seedance Prompt 与请求记录，将创作所需时长映射为最小且足够的后端档位，必要时裁切或要求拆镜，并在授权范围内执行 DRY_RUN、Pilot、逐镜或批量生成。

它是 Seedance 专用适配器，不代表系统必须选择 Seedance。项目选择非 Seedance 时，本 Skill 只返回兼容 Producer 路由或 `BACKEND_ADAPTER_MISSING`，不得强制回落。真实生成前运行者可比较 ECONOMY/BALANCED/QUALITY_FIRST；价格未知时明确显示 `COST_UNKNOWN`。

## 输入

- `stage-outputs/05_storyboard_LOCKED.json`
- 条件性 `stage-outputs/04_visual_bible/asset_manifest_LOCKED.yaml`
- state 指向的 `stage-outputs/06_qa/preflight_report_v{n}.md`，必须 GREEN 且 `producer_eligible=true`
- 当前 Seedance capability profile

## 输出

- `stage-outputs/07_model_prompts/seedance/<shot_id>_LOCKED.md`
- `stage-outputs/08_generation/generation_manifest.json`
- `stage-outputs/08_generation/generation_log.md`

## 最小运行

从 DRY_RUN 开始，验证 Prompt 七段结构、Dialogue/reference/parameter parity 和日志 schema。真实 Pilot 还需要可调用 backend、`VERIFIED_CURRENT` profile 与成本授权。

## 测试

```powershell
pwsh -File tests/run-contract-tests.ps1
pwsh -File tests/run-gate-tests.ps1
pwsh -File tests/run-handoff-tests.ps1
pwsh -File tests/run-duration-mapping-tests.ps1
```

版本 v0.1.2；真实用户、真实 Seedance Pilot 与运行历史完成前为 AFP-SPEC provisional Silver。
