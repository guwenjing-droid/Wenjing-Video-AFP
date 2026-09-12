# P1 · 可观察性与证据范围

## 边界
只声明本轮能观察什么、不能观察什么；不下 PASS/FAIL 结论。

## 执行
POSTGEN/MOCK_POSTGEN Read `modules/postgen-observability.md`。POSTGEN 登记 VIDEO/FRAMES/AUDIO/TRANSCRIPT/METADATA；PREFLIGHT 登记 Artifact/asset/parameter 可读范围；MOCK_POSTGEN 登记 MOCK_MANIFEST/MOCK_RESULT，并把所有媒体维度列为 NOT_OBSERVABLE。每个 required check 绑定所需模态；缺模态禁止推断。

## 输出 schema
写入报告 DRAFT `observability`：provided、missing、derived evidence、excluded dimensions、required gaps；更新 state。

## Gate
```
╭─ Continuity Reviewer · P1 完成 ───────────╮
│ provided/missing：{列表}
│ required evidence gap：{N}
│ 下一步：P2 契约与覆盖审计
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不从 transcript 猜画面/音乐；不从单帧判断运动/口型；不从视频无音轨判断原计划音频。

---
*P1 完成后加载 `stages/02-contract-and-coverage-audit.md`。*
