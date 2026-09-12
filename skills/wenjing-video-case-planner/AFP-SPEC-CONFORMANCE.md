# AFP-SPEC 合规证书

- skill：wenjing-video-case-planner v0.1.0
- partner：wenjing
- skill_type：independent
- 检查日期：2026-09-09
- 检查工具：一平老师 afp-skill-creator v0.6 · P8，对照 AFP-SPEC v0.1

## 判定结果

- 目标等级：Silver
- 判定：provisional
- 当前已认证基线：Bronze
- 待达成项：
  1. P9 补齐 3 个真实目标用户案例；合成 Fixture 不替代真实用户。
  2. 安装后新会话完成主要触发、变体触发、隔离口令、Hard Stop、写盘和 Continue 测试。
  3. wenjing-video-narrative-designer 建成后完成真实上下游读取与接棒测试。

## §5 Hard Stops：7/7 PASS

| ID | 结果 | 证据 |
|---|---|---|
| H1 | PASS | stages 共 7 个，确认框覆盖 7/7 |
| H2 | PASS | 7/7 确认框均含 Next 行；终站 Next 只确认结束，不自动运行下游 |
| H3 | PASS | SKILL.md 明确即使结果明确也不得自动推进 |
| H4 | PASS | 通用指令含 Next、Back、Edit |
| H5 | PASS | P2 冲突处理、P3 教学方向均提供多方案与代价 |
| H6 | PASS | Back 回到最近磁盘 checkpoint；不改 LOCKED；依赖草稿标 STALE |
| H7 | PASS | 乱序请求先查前置 Gate，未过则留在当前站 |

## §6 Evidence Chain：6/6 PASS

| ID | 结果 | 证据 |
|---|---|---|
| E1 | PASS | P3 记录用户授权历史资产和 AFP 工程改造来源；未虚构经典书目 |
| E2 | PASS | P1/P2 定义 source registry、source anchor 和外部核验动作 |
| E3 | PASS | 教育培训/案例视频领域采用 Fact、Interpretation、Inference、Unknown 分层 |
| E4 | PASS | 定义 UNVERIFIED_EXTERNALLY、INCONCLUSIVE 和 REVIEW_REQUIRED |
| E5 | PASS | 能力边界明确，不承诺完整研究、剧本、分镜或生成 |
| E6 | PASS | Source Registry 要求 version_or_date；时效信息进入外部核验边界 |

## §7 Output Structure：6/6 PASS

| ID | 结果 | 证据 |
|---|---|---|
| O1 | PASS | SKILL.md HUD 覆盖 meta、stage_status、gates、continuation、history |
| O2 | PASS | 7/7 stage 均有输出 schema 与落盘节 |
| O3 | PASS | 主控列出 Draft、LOCKED、manifest/state 三类最终交付物 |
| O4 | PASS | 七个 stage 使用同一家族确认框和 Next/Back/Edit 语义 |
| O5 | PASS | 7/7 stage 明确具名结果文件或状态文件；新对话可依盘恢复 |
| O6 | PASS | templates/用户核查清单.md 共 7 个阶段行，每行含动作、核查项和落盘件 |

## §8 Multi-Agent Handoff：PARTIAL / PROVISIONAL

| ID | 结果 | 证据或待办 |
|---|---|---|
| M1 | PROVISIONAL | 已定义下游和直击口令；下游 Skill 尚未建成，P9 后续接棒测试 |
| M2 | PASS | modules/project-contract.md 定义 manifest/state/Continue |
| M3 | PROVISIONAL | 本件能写交接状态；需 Narrative Designer 建成后验证读取 |
| M4 | N/A | 本件是 Independent，不是 Orchestrator |
| M5 | N/A | 当前不调用 Shared Primitive |
| M6 | PASS | project contract v0.2、case truth lock schema v0.2 |

## 静态验证摘要

- SKILL.md 位于包根目录。
- name、partner、skill_type、afp_spec_target、agent_created 一致。
- 子文件首行 frontmatter 数：0。
- stage 路由：7/7 存在。
- module 路由：5/5 存在。
- 包内显式引用：15 条，缺失 0。
- 触发词静态预检：PASS_WITH_ISOLATION。

## P9 工程测试摘要

- 自动契约测试：22/22 PASS，详见 `TEST-LOG.md`。
- 三类合成 Fixture 已覆盖正常路径、事实冲突阻断、Continue 与 STALE 传播；不计入真实用户案例。
- P9 发现并修复 P6 Hard Stop 标识缺口。
- P9 发现并修复整文件 SHA-256 自引用风险：LOCKED 冻结后计算，hash 只登记到 manifest/state。
- 新会话运行测试受本机 CLI 环境限制，状态保持 RUNTIME_PENDING；不得据此声称 Silver certified。

## 自评声明

本证书是施工期自评，接受 Steering Committee 复核。它不表示 Silver 已正式认证，也不表示该 Skill 已进入 AFP 官方生态或启用积分。

—— wenjing，2026-09-09
