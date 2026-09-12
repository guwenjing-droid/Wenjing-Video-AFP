# Prompt Compiler

## 七段结构

1. Output Settings：`creative_required_duration`、`selected_generation_duration`、duration mapping/trim plan、aspect ratio、resolution、audio policy。
2. Dialogue Lock：角色、逐字对白、顺序；无对白写 `NONE`。
3. Character Lock：可见角色、身份、服装状态、站位。
4. Ordered References：按实际请求数组顺序列 order、asset_id、用途和 hash。
5. Scene and Prop Anchors：空间、光影、道具位置/状态，只取锁定来源。
6. Timeline：每 1–3 秒或按 Storyboard beat，写构图、镜头、动作、连续性、Dialogue/SFX。
7. Negative Constraints：上游和项目已定义的禁止项；默认防止额外角色、身份漂移、无授权文字/水印/气泡，但不得与用户明确的字幕/音乐要求冲突。

## 编译纪律

- 每段保留 `source_refs`；不得把抽象情绪替换成上游没有的表演动作。
- 镜头词汇必须对应 Storyboard 的 shot size、camera、blocking 或 transition；不为“电影感”堆词。
- 可从受控词类中选用运镜、摄影、人物动作、环境、情绪氛围和时间状态表达，但每个词都必须对应 Storyboard/Visual Bible 的可定位字段；词表是措辞库，不是内容来源。
- 内容语言可适配 provider，但 Dialogue Lock 的字符、标点、顺序不可变。
- 后端时间轴覆盖映射后的生成档位；创作内容只占 creative duration，超出部分仅可用于安全尾帧/裁切，不新增动作或对白。
- Prompt 不是最终真相源；冲突时 `Storyboard LOCK > Visual asset lock > project constraint`，出现不可判定冲突即 BLOCK。
