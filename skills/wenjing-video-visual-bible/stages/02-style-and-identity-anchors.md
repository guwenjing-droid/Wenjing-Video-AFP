# P2 · 风格与身份锚

> Visual Bible · Stage 02

## 边界

只冻结全局视觉方向与角色身份不可变特征；不制作逐镜构图。

## 执行

1. Read `modules/identity-consistency.md`；读取项目约束和已选风格/身份资产。
2. 为全局 style 写媒介、时代、材质、色彩、光线、写实度和禁止项；不得继承历史样例的任务特定风格。
3. 为每个核心角色写身份锚：稳定面部/体型/年龄带/标志特征与可变服装状态，区分 invariant 与 variant。
4. 对复用候选做 version/hash/rights/style/identity/readiness 兼容检查，记录 `REUSE` 或 `REGENERATE` 原因。
5. 方向存在多个合法方案时给 2–3 个方案及代价，由用户或 manifest 中的预授权规则选择。

## 输出 schema

- `stage-outputs/04_visual_bible/style_spec_LOCKED.md`
- `stage-outputs/04_visual_bible/identity_anchors/{character_id}_LOCKED.md`
- asset manifest DRAFT 中的 style/identity/reuse 字段

方向 Gate：FAST 可按已登记偏好 REVIEW；GUIDED/STRICT 或品牌/IP/高连续性项目为 HARD。未确认不得进入高成本生成。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

## Gate

```
╭─ Visual Bible · P2 完成 ─────────────────╮
│ 风格方向：{摘要} · Gate：{状态}
│ 身份锚：{N} · 复用/重建：{R}/{G}
│ 下一步：P3 角色参考集
╰───────────────────────────────────────╯
```

## 反模式

- 不把服装变体写进身份不变量；不以“高清/8K”代替视觉风格；不复用权利或版本不明资产；不承诺绝对一致。

---
*P2 完成后加载 `stages/03-character-reference-sets.md`。*
