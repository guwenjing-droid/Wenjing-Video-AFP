# wenjing-video-reference-analyzer

对参考视频、transcript、帧或音频做五层逆向分析，输出 `Reference Analysis LOCKED Artifact`，供后续原创 Narrative 可选采用。

## 能做

- Content、Narrative、Engagement、Audiovisual、Transfer 五层分析。
- 输入模态和逐维可观察范围控制。
- Evidence Anchors、视频声称/核验事实分层。
- 原创迁移、禁复制、局限与外部补充隔离。

## 不做

不生成最终剧本、Storyboard、Seedance Prompt 或视频；不把 transcript 当实际视听证据；不仿写或复制原视频。

## 输入与输出

输入至少一种：transcript、video、frames、audio。输出：

```text
stage-outputs/00_reference_analysis/reference_analysis_manifest.yaml
stage-outputs/00_reference_analysis/<reference_id>_DRAFT.md
stage-outputs/00_reference_analysis/<reference_id>_LOCKED.md
```

## 流程

P0 模态 → P1 Content → P2 Narrative → P3 Engagement → P4 Audiovisual → P5 Transfer/Audit → P6 Lock/Handoff。

只有 transcript 时，P4 必须 `NOT_OBSERVABLE`，但 Content、Narrative 与部分 Engagement 仍可继续。

## 续传

`Continue {project_ref}`。通过 Adapter 从 manifest/state/Artifacts/CR 恢复，不依赖旧对话。

## 接棒

主要可选消费方：`wenjing-video-narrative-designer`。采用优先级固定为 `Case Truth Lock > 用户/项目约束 > Reference Analysis`。本 Skill 不自动触发下游。

## MVP

v0.1 优先保证冻结接口、模态/可观察性/原创 Gate、落盘、续传和专项接棒测试。自动抽帧、ASR、多参考比较和扩展示例进入 v0.2 backlog。

## P9 本地工程验收

- 契约测试：43/43 PASS。
- Reference Analysis → Narrative Designer：17/17 PASS。
- 状态：Bronze Local Ready；Silver provisional。
- 待补：干净新会话、真实参考视频、3 位真实用户和项目级纵向联跑。

## 版本

- v0.1.0：CR-001 首个 MVP。
