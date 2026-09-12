# P4 · 场景与道具参考集

> Visual Bible · Stage 04

## 边界

只建立可复用的空间、陈设和关键道具 reference；不决定逐镜景别、运镜或剪辑。

## 执行

1. Read `modules/scene-and-prop-method.md`，按资产清单读取相关 Script anchors。
2. 每个核心场景定义平面关系、入口/出口、关键轴线、光源、固定陈设与时间状态；按需要选择正反向、侧向或俯仰参考。
3. 每个关键道具定义外形、材质、比例、独特标志、持有者/位置和状态变化。
4. 优先复用通过兼容审查的现有场景/道具。真实生成沿用工具和成本授权 Gate；`V0_1_DRY_RUN` 只生成可接棒规格与 planned reference 清单。
5. 检查必需覆盖、空间自洽和道具状态；真实轨另查实际文件/完整性校验码，Dry Run 轨将其明确标 DEFERRED。局部失败只回该资产 checkpoint。

## 输出 schema

- `stage-outputs/04_visual_bible/scene_refs/{scene_id}/...`
- `stage-outputs/04_visual_bible/prop_refs/{prop_id}/...`
- `stage-outputs/04_visual_bible/scene_prop_sheets/{asset_id}.md`
- 更新 manifest DRAFT 和 state

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

## Gate

```
╭─ Visual Bible · P4 完成 ─────────────────╮
│ 场景 READY：{N}/{required} · 道具 READY：{N}/{required}
│ 空间/状态校验：{PASS|FAIL}
│ 下一步：P5 Readiness 与边界审计
╰───────────────────────────────────────╯
```

## 反模式

- 不用氛围词代替空间关系；不让同一道具无记录变形；不把镜头调度写进场景规范；不全量生成未用角度。

---
*P4 完成后加载 `stages/05-readiness-and-boundary-audit.md`。*
