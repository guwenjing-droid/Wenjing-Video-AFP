# Modality & Observability Policy

## 合法模态

| input_modality | 必须实际存在 | 默认 analysis_scope |
|---|---|---|
| TRANSCRIPT_ONLY | transcript | content, narrative, engagement_partial |
| VIDEO | video（是否含可用音轨另记） | content/narrative/engagement/audiovisual 的实际可见子集 |
| FRAMES_AUDIO | frames；audio 可有可无但必须如实登记 | visual 子集 + audio 子集 |
| MIXED | 两类以上实际材料 | 各材料交集/并集内的可观察子集 |

文件扩展名或用户口头声明不能替代可读性检查。

## 子维度规则

- transcript：语言、观点、文本顺序、文本钩子、部分叙事/参与机制。
- video/frames：景别、构图、站位、字幕是否出现、色彩/光影；只有连续视频或足够连续帧才可判断运镜/镜头长度。
- audio：可听台词、音乐、音效、节奏；无音频时全部 NOT_OBSERVABLE。
- 平台留存：除非提供真实 analytics，否则永远不是 OBSERVED。

每项状态只允许：`OBSERVED | NOT_PRESENT | NOT_OBSERVABLE | ANCHOR_LIMITED`。

## 违规即 BLOCK

- transcript-only 填写实际运镜、表演、字幕样式、BGM、音效或转场。
- 单帧推断镜头运动；静音材料推断音乐；摘要伪造时间码。
- scope 大于实际材料可观察范围。

