# P3 · Shot Grammar & Blocking

## 边界

只为 beats/atoms 选择构图、景别、机位、运动、站位和转场；不写生成模型 Prompt。

## 执行

1. Read `modules/shot-grammar.md`；先计算满足 Script、Dialogue、Knowledge、Action Clarity 与 Continuity 全覆盖的 `minimum_legal_shots`，不得用固定镜头数代替计算。
2. 每镜明确 `shot_size/angle/composition/camera_motion/blocking/focus`，并绑定 atom/beat。
3. 确立轴线、视线、入出画方向和 screen geography；切换必须有叙事或信息理由。
4. 输出三个可比预算档：A `ECONOMY`（最少合法镜头）、B `BALANCED`（清晰度与成本平衡）、C `EXPRESSIVE`（情绪/节奏增强）。每档必须列出预计镜头数、预计生成请求数、可合并项、拒绝合并项、表达收益与连续性代价；用户或 manifest 预授权策略决定。
5. 反应、呼吸、建立/收束镜头只在 Script/Narrative 功能需要时加入，不机械套模板。
6. 只有五项保护覆盖全部 PASS 才允许推荐 `ECONOMY`：Script、Dialogue、Knowledge、Action Clarity、Continuity。任一合镜导致多地点/多时间、互斥站位、动作过载、台词超时或信息缺失，必须保留拆镜并记录 `merge_rejection`。

## 输出 schema

回填 DRAFT `shot_budget_policy` 与 `shots[]` 中 camera/composition/blocking/transition；稳定 `shot_id` 不因文字润色改变。`shot_budget_policy` 记录 mode、decision_source、minimum_legal_shots、selected_shot_count、estimated_generation_requests、protected_coverage、options 与 merge_rejections。更新 state。

## Gate

```
╭─ Storyboard Director · P3 完成 ───────────╮
│ shots：{N} · 预算档：{ECONOMY|BALANCED|EXPRESSIVE}
│ 最少合法镜头/预计请求：{N}/{N}
│ 轴线/视线/空间：{PASS|REVIEW}
│ 下一步：P4 Timing/Dialogue/Audio/Assets
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不强制九种景别；不为“电影感”乱动镜头；不让机位破坏空间；不把情绪形容当表演动作；不把“少镜头”变成动作和台词过载。

---
*P3 完成后加载 `stages/04-timing-dialogue-audio-and-asset-binding.md`。*
