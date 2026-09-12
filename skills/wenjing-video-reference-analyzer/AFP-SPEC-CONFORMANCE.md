# AFP-SPEC 合规证书（本地自评）

- Skill：`wenjing-video-reference-analyzer` v0.1.0
- partner：`wenjing`
- skill_type：`independent`
- 检查日期：2026-09-10
- 检查工具：一平 `afp-skill-creator v0.6` P8，对照 AFP-SPEC v0.1
- 证书性质：本地自评；不是 Steering Committee 官方认证

## 判定

- 目标等级：Silver
- 当前等级：Bronze `LOCAL READY`（本地工程自评）
- Silver：`provisional`
- 待达成：干净运行会话、真实参考材料运行、3 位真实用户

## §5 Hard Stops · 7/7

- 7 个 stage 均有统一 Hard Stop、下一站和不自动推进纪律。
- 主控含 Next/Back/Edit/Skip/Status/Export/Continue。
- P5 提供迁移强度多方案，但 G-RA-03 不由方案选择覆盖。
- 乱序和关键 Gate Skip 均被拒绝。

## §6 Evidence Chain · 6/6

- Observation、Video Claim、Analytic Inference、Externally Verified、Unverified 分层。
- transcript 行号、视频/音频时间码和 frame_id 均有 Evidence Anchor 规则。
- ANCHOR_LIMITED 必须降级置信度；禁止伪造定位符。
- 外部补充与观察严格分栏，含来源、日期和核验状态。
- 历史方法来源及保留/拒绝边界已登记。
- 不承诺爆款、真实留存或未提供的视听效果。

## §7 Output Structure · 6/6

- HUD JSON 可解析，含 modality、observed/missing、scope、Gate、Artifact 和 continuation。
- P0–P6 均有输出 schema 与具名落盘路径。
- 九区 Reference Analysis 模板与冻结 Contract 对齐。
- DRAFT/LOCKED、reference manifest、project manifest/state、CR 模板齐全。
- 7 行用户核查清单对应 P0–P6。
- 子文档首行 frontmatter 为 0。

## §8 Independent Handoff · 4/4

- P6 给出 Narrative Designer 可选下一站与直击口令，不自动代跑。
- 磁盘续传、版本、SHA-256、LOCKED/STALE/CR 协议完整。
- Narrative Designer 已具备 `reference-analysis/0.1` 可选消费接口。
- 优先级固定：`Case Truth Lock > 用户/项目约束 > Reference Analysis`。

Orchestrator 业务纯度与 Shared Primitive 调用契约不适用于本件。

## CR-001 专项

- G-RA-01 输入模态、G-RA-02 可观察性、G-RA-03 原创迁移均已落实。
- TRANSCRIPT_ONLY 的 Audiovisual Grammar 强制 NOT_OBSERVABLE。
- 不生成最终 Narrative、剧本、Storyboard、Seedance Prompt 或视频。

## P9 工程验证

- 契约测试：43/43 PASS。
- `Reference Analysis LOCKED → Narrative Designer` 文件级专项接棒：17/17 PASS。
- transcript-only、mixed、越模态、原创性与完整性 fixtures 均通过。

仍待外部条件：干净新会话、真实参考材料运行、3 位真实用户和项目级纵向联跑。

—— wenjing，2026-09-10
