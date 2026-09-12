# POSTGEN Observability

| 证据 | 可评估 | 不足以评估 |
|---|---|---|
| 完整视频 | 时序、运动、转场、画面连续 | 无音轨时的声音 |
| 足够帧+时间码 | 身份/服装/场景/道具、部分动作状态 | 完整运动、口型同步、声音 |
| 音频 | Dialogue/VO/SFX/BGM 与时序 | 视觉、运镜、表演 |
| transcript | 文本内容/顺序 | 镜头、字幕呈现、BGM/SFX、口型、表演 |
| metadata | 参数/任务/路径 | 实际成片质量 |

结论必须绑定 `file + timecode/frame/audio range`。抽帧不足或媒体不可读时写 NOT_OBSERVABLE；required 维度不可观察至少 YELLOW，关键安全/交付维度可 RED。

## MOCK_POSTGEN

Mock 结果不是媒体证据。允许检查 `is_mock`、request/result 状态、错误码、重试次数、检查点、受影响镜头和未受影响 Artifact；实际画面、身份、动作、字幕、声音与成片连续性全部写 `NOT_OBSERVABLE`。Mock 成功不得改写为 POSTGEN GREEN。
