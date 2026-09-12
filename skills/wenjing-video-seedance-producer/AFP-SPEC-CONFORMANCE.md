# AFP SPEC Conformance

- skill: wenjing-video-seedance-producer v0.1.2
- partner: wenjing
- skill_type: independent
- checked_at: 2026-09-10
- checker: yiping-afp-skill-creator v0.6 P8

## 目标

- target: Silver
- decision: provisional Silver
- release: v0.1.2 MVP
- pending: 3 个真实用户案例、真实 Seedance Pilot 与纵向联跑

## 检查

| 项 | 结果 | 证据 |
|---|---|---|
| 唯一 thin router | PASS | `SKILL.md` |
| Stage 顺序与不可跳过 | PASS | P0–P6 |
| Module 按需加载 | PASS | 7 modules |
| Hard Gate | PASS | GREEN、能力档、parity、成本授权 |
| Artifact Contract | PASS | Prompt/manifest/log templates + creative-to-backend duration mapping |
| 状态与恢复 | PASS | project contract/state template |
| 触发隔离 | PASS | frontmatter + conflict report |
| 证据链 | PASS | hash/reference/parameter/attempt records |
| 真实生成诚实性 | PASS | DRY_RUN 不冒充输出 |
| 自动化测试 | PASS | contract/gate/handoff suites |

本证书为合伙人项目自评，接受后续复核。真实用户门槛和真实 Seedance Pilot 尚未完成，因此不声明正式 Silver。
