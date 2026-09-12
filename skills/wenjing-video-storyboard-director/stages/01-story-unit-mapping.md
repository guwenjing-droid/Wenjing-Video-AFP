# P1 · Story Unit Mapping

## 边界

只把 Script 场次映射为 sequence/story unit/beat 骨架；不选择镜头语法。

## 执行

1. Read `modules/story-unit-method.md` 和所需 Script 段落。
2. 按场景、时间、因果与转折建立稳定 `sequence_id`、`beat_id`。
3. 为每个 beat 记录 Script evidence、叙事功能、人物、地点、动作、Dialogue/VO、知识节点和连续性入口/出口。
4. 检查每个 Script scene/beat 恰被覆盖；不得为凑节奏增删内容。

## 输出 schema

使用 `templates/storyboard-schema.json` 建立并落盘 `{project_path}/stage-outputs/05_storyboard_DRAFT.json`；更新 state。P1 coverage AUTO 全绿才进入 P2。

## Gate

```
╭─ Storyboard Director · P1 完成 ───────────╮
│ sequences/beats：{N}/{N}
│ Script coverage：{PASS|FAIL}
│ 下一步：P2 Action Atomization
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不把每句台词机械当独立镜头；不重排因果；不遗漏静默反应或知识 beat；不写模型参数。

---
*P1 完成后加载 `stages/02-action-atomization.md`。*
