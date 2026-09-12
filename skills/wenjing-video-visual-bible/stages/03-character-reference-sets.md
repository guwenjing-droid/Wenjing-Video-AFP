# P3 · 角色参考集

> Visual Bible · Stage 03

## 边界

只建立角色 reference spec、实际文件与 readiness；不写角色剧情或逐镜表演。

## 执行

1. Read `modules/character-reference-method.md` 和对应身份锚。
2. 按角色重要度选择最小充分视图：核心角色正/侧/背与必要表情/动作；次要角色按实际镜头需求裁剪。
3. 生成或整理角色 sheet spec，确保同一身份锚、比例、服装状态和命名；禁止互相矛盾的排版要求。
4. 现有资产通过兼容检查则复用。需要真实生图时，先校验工具与成本授权；`V0_1_DRY_RUN` 只输出完整 spec，保持 `SPEC_READY_ASSET_MISSING`，并在规格通过后写 `dry_run_readiness=READY`。
5. 对实际文件做存在性、可读性、hash、视图覆盖和身份一致性检查；未审查生成物为 `ASSET_GENERATED_UNREVIEWED`。

## 输出 schema

- `stage-outputs/04_visual_bible/character_sheets/{character_id}.md`
- `stage-outputs/04_visual_bible/character_refs/{character_id}/...`
- 更新 asset manifest DRAFT 和 state

实际文件通过检查才标实际 READY；Dry Run 规格就绪不等于图片存在。单角色失败只重跑该角色及依赖项。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

## Gate

```
╭─ Visual Bible · P3 完成 ─────────────────╮
│ 角色资产 READY：{N}/{required}
│ 复用：{N} · 待生成/待审：{N}
│ 下一步：P4 场景与道具参考集
╰───────────────────────────────────────╯
```

## 反模式

- 不把 Prompt 文本标成图片 READY；不为无镜头需求的次要角色过度生成；不因一个角色失败重跑其他角色。

---
*P3 完成后加载 `stages/04-scene-and-prop-reference-sets.md`。*
