# Source Fidelity Policy

P1 给选定范围内每个可表达单元稳定 `source_span_id`，记录 locator、type、exact dialogue、sequence 与约束。P2 每个 span 只能为：

- `VERBATIM_DIALOGUE`：exact_text 必须逐字一致；
- `DIRECT_ACTION`：原文已有动作直接映射；
- `OBSERVABLE_EQUIVALENT`：把不可见叙述等义变成可观察表演，不新增事实；
- `NONVISUAL_VO`：保持原意进入旁白。

选定范围内不允许 `OMITTED`。如果内容与时长冲突，状态为 BLOCKED，要求用户缩小来源范围或扩展时长。人物、事件顺序、因果、数值、结局和原对白零改写。

