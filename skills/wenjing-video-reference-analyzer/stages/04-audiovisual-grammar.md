# P4 · Audiovisual Grammar

> 只分析实际提供并可定位的视觉/音频信息，不生成镜头方案或提示词。

## 执行

1. Read `modules/modality-observability-policy.md` 与 `modules/audiovisual-grammar-method.md`。
2. 若 `TRANSCRIPT_ONLY`：整节写 `analysis_status: NOT_OBSERVABLE`，列出缺失的 video/frames/audio 后结束本节。
3. 其他模态逐项判断景别、构图、运镜、镜头长度、动作/站位、字幕、音乐、音效、转场、色彩、光影、风格是否可观察。
4. 每项只登记 Observation + Anchor；解释性判断另标 ANALYTIC_INFERENCE。
5. 音频缺失则音乐/音效 NOT_OBSERVABLE；视频或帧缺失则视觉项 NOT_OBSERVABLE。帧序列不足时不得声称运镜。

## 完成标准

- G-RA-02 无越模态结论。
- 每个子维度是 OBSERVED、NOT_PRESENT、NOT_OBSERVABLE 或 ANCHOR_LIMITED 之一。
- 没有把分析写成待生成视频的镜头指令。

## 输出 schema 与落盘

更新 DRAFT 的 Audiovisual Grammar、Evidence Anchors 与 G-RA-02 状态，更新 state。

## Hard Stop

```text
╭─ Reference Analyzer · P4 完成 ─╮
│ Audiovisual：OBSERVED | PARTIAL | NOT_OBSERVABLE
│ G-RA-02：PASS | REVIEW | BLOCK
│ 下一步：P5 Transfer & Boundary Audit
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────────╯
```

不自动进入 P5；G-RA-02 BLOCK 时不得继续。

## 反模式

- transcript 推镜头/BGM；单帧推运镜；静音视频推音效；把字幕文本等同实际字幕样式。

---
*P4 确认后加载 `stages/05-transfer-and-boundary-audit.md`。*
