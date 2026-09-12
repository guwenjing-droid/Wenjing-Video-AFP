# AFP-SPEC 合规证书（本地自评）

- Skill：`wenjing-video-narrative-designer` v0.1.0
- partner：`wenjing`
- skill_type：`independent`
- 检查日期：2026-09-10
- 检查工具：一平 `afp-skill-creator v0.6` P8，对照 AFP-SPEC v0.1
- 证书性质：本地自评；不是 Steering Committee 官方认证

## 判定结果

- 目标等级：Silver
- 当前等级：Bronze `certified`（本地自评）
- Silver 判定：`provisional`
- 待达成：P9 干净新会话运行测试；Analyzer 建成后的真实专项接棒；Silver 所需 3 个真实用户案例
- Gold：未申请

## §5 Hard Stops · 7/7

| ID | 结果 | 证据 |
|---|---|---|
| H1 | PASS | P0–P6 共 7/7 个 stage 有统一交付确认框 |
| H2 | PASS | 7/7 含 `Next` 行和下一步 |
| H3 | PASS | 7/7 明确不允许自动推进 |
| H4 | PASS | 主控含 Next / Back / Edit |
| H5 | PASS | P1/P2/P3 方向性决策使用 2–3 个实质方案 |
| H6 | PASS | Back 回到最近磁盘 checkpoint，受影响草稿标 STALE |
| H7 | PASS | 乱序请求先列未过 Gate，不允许越阶 |

## §6 Evidence Chain · 6/6

| ID | 结果 | 证据 |
|---|---|---|
| E1 | PASS | P3 登记 4 份真实历史方法来源及保留/拒绝边界 |
| E2 | PASS | promise/node/knowledge 逐项绑定 fact_id / knowledge_id / boundary |
| E3 | PASS | FACT、ALLOWED、CONDITIONAL、FORBIDDEN 只读政策完整 |
| E4 | PASS | 无法验证内容显式标 `unverified`，禁止进入 LOCKED Narrative 核心结论 |
| E5 | PASS | 不承诺爆款或传播成功，不宣称未提供的视听分析 |
| E6 | PASS | 数据保留 source/source_id、数据期间或发布日期与限定词 |

## §7 Output Structure · 6/6

| ID | 结果 | 证据 |
|---|---|---|
| O1 | PASS | 主控 HUD JSON 可解析，含 meta/upstream/stage/gate/continuation/history |
| O2 | PASS | 7/7 stages 有输出 schema |
| O3 | PASS | 主控列出 Draft、LOCKED、manifest/state 正式交付物 |
| O4 | PASS | 7/7 使用同一 Skill 的 Hard Stop 确认框结构 |
| O5 | PASS | P0 落 manifest/state；P1–P5 落 Draft；P6 落独立 LOCKED |
| O6 | PASS | 用户核查清单 7 行对应 P0–P6，含核查项和落盘件 |

## §8 Multi-Agent Handoff · 适用项 4/4

本件是 Independent Skill，不检查 Orchestrator 业务纯度和 Shared Primitive 调用契约；其跨 Skill 交接适用项如下：

| ID | 结果 | 证据 |
|---|---|---|
| M1 | PASS | P6 给出 `wenjing-video-script-studio` 下一站与直击口令；不自动代跑 |
| M2 | PASS | manifest/state/locked/stale/CR/Continue 格式完整 |
| M3 | PASS | P0 先读取项目状态、Truth Lock 和可选 Reference Analysis |
| M6 | PASS | Pipeline v0.3、Narrative schema v0.2、Reference Contract v0.1 |
| M4 | N/A | 本件不是 Orchestrator |
| M5 | N/A | 本件不是 Shared Primitive |

## CR-001 专项合规

- Reference Analysis 是 optional auxiliary input，缺失不阻断标准 CASE。
- 采用优先级固定：`Case Truth Lock > 用户/项目约束 > Reference Analysis`。
- 输入模态、可观察性、原创迁移和采用 Gate 均存在。
- transcript-only 的未提供视听维度必须 `NOT_OBSERVABLE`。
- Narrative Plan 记录 ref 与 transfer rule provenance；不把 Reference 设为 Script Studio 直接必需输入。

## P9 工程验证

- 静态/契约测试：40/40 PASS。
- 文件级 Artifact 接棒测试：14/14 PASS。
- Case Planner → Narrative Designer 的 LOCKED、版本、SHA-256 与 STALE 阻断已验证。
- transcript-only 可观察性和原创迁移拦截已验证。

仍待外部运行/项目级条件：

1. 可用 OpenClaw/Codex 干净新会话中的真实触发、Hard Stop、写盘和 Continue。
2. Reference Analyzer 建成后的 `Reference Analysis LOCKED → Narrative Designer` 真实专项接棒。
3. 3 个真实用户案例门槛。
4. 核心产线的一条真实管理学案例纵向联跑。

## 自评声明

本证书证明当前 package 的 AFP-SPEC v0.1 静态条款与 P9 本地工程测试结果。外部运行和真实案例未完成前不将 Silver 标为 `certified`，也不宣称 AFP 官方认证。

—— wenjing，2026-09-10
