# P4 · Timing / Dialogue / Audio / Asset Binding

## 边界

只完成时长、锁定文本、声音事件和资产引用；不指定模型参数或提交数组顺序。

## 执行

1. Read `modules/duration-estimation.md`。逐镜计算 speech/action/camera/comprehension 四类候选时长，按项目配置的中文语速区间而非单一硬编码值估算对白。
2. 以最长必要因素为 core，再加入自然停顿/动作收束/剪辑衔接所需的 transition buffer，得到最短充分的 `creative_required_duration`；若明确存在可复用的跨镜 overlap，只能作为有证据的单独抵扣且不得使结果低于任何硬下限。
3. 每镜写 `estimated_duration`、`creative_required_duration`、`duration_basis` 和 `duration_driver=SPEECH|ACTION|CAMERA|COMPREHENSION|MIXED`；兼容字段 `duration_seconds` 必须与 creative 值一致。
4. 若内容超过项目登记的创作单镜上限，或对白/复杂动作无法在一个镜头内完整表达，先按 Script 边界拆镜并保留 source refs；禁止强行 clamp。没有后端能力档时只标 `PRODUCER_MAPPING_REQUIRED`，不得臆测模型档位。
5. Dialogue/VO 逐字继承 Script，标点、顺序和 speaker 不变；无台词镜头显式为空。
6. 声音只登记 `dialogue/voiceover/ambient/sfx/music_intent` 的叙事需求；不擅设“无音乐/必须配乐”。
7. 若 Visual Bible 已选：真实轨绑定 READY asset_id/content_ref/hash 到 `asset_refs`；`V0_1_DRY_RUN` 把规格级就绪项绑定到 `planned_asset_refs` 并明确 `real_media_status=DEFERRED`。每个 ref 必须只含一个独立 canonical `asset_id`；禁止 `CHR-001/002`、`CST-001/002` 等斜杠拼接、范围或组合简写。无 Visual 时按契约标 `TEXT_ONLY` 或 `ASSET_REQUIRED`。
8. 记录 shot 间 continuity anchors：动作、位置、视线、服装、道具、光线与 transition。
9. 建立 required asset binding closure：Visual Bible/manifest 中每个 `required=true` 的 asset_id 至少被一个镜头的 `asset_refs` 或合法 Dry Run `planned_asset_refs` 引用；任何未引用项立即 FAIL，不得标 P4 PASS。

## 输出 schema

回填 DRAFT 的 `estimated_duration/creative_required_duration/duration_basis/duration_driver/duration_seconds/dialogue/audio/asset_refs/planned_asset_refs/continuity`。完成逐镜可解释性、非默认等长、对白/动作硬下限、超载拆镜、总时长、Dialogue Lock、canonical asset_id 与 required asset binding closure 自动校验；更新 state。

## Gate

```
╭─ Storyboard Director · P4 完成 ───────────╮
│ 时长：{actual}/{target} · 动态推导：{PASS|FAIL}
│ 超载拆镜：{N} · Dialogue：{PASS|FAIL}
│ READY asset refs：{N}/{required}
│ 下一步：P5 Continuity & Boundary Audit
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不改写台词以塞进时长；不默认全片等长；不把 transition buffer 当任意压缩额度；不引用未 READY 资产；不把 URL/任务 ID 当文件；不写 reference_images 调用数组。

---
*P4 完成后加载 `stages/05-continuity-and-boundary-audit.md`。*
