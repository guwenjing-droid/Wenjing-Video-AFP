# AFP-SPEC 合规证书

- skill：wenjing-video-visual-bible v0.1.0
- partner：wenjing
- skill_type：independent
- 检查日期：2026-09-10
- 检查工具：一平老师 `afp-skill-creator v0.6` P8

## 判定结果

- 目标等级：Silver
- 判定：provisional
- 待达成项：3 个真实目标用户案例与正式生态备案；本地接口/结构/自动化测试见 P9 报告。

## 逐条结果

| 条款 | 结果 | 证据 |
|---|---|---|
| §5 Hard Stops | PASS | 7 个 stages 均有 Gate/确认框/禁止未过 Hard Gate 自动推进；Next/Back/Edit 已定义 |
| §6 Evidence Chain | PASS | Script provenance、source/rights/version/hash 与 evidence anchors 为必填审计项 |
| §7 Output Structure | PASS | HUD、每 stage 输出 schema、具名落盘件、7 行用户核查清单齐备 |
| §8 Handoff | PASS（Independent 适用项） | Integration Guide 定义输入/输出/状态/错误，P0 可独立读 state，P6 指向真实下游 |

## 声明

本证书为工程自评；不把待完成的真实用户案例写成 certified。重大版本需重跑 P8。
