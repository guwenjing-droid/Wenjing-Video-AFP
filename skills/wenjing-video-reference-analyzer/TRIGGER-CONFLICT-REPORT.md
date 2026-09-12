# Trigger Conflict Report · wenjing-video-reference-analyzer

## 结果

`PASS_WITH_ISOLATION`

## 扫描范围

- Codex 已配置 Skill 根
- Agent 平台已配置 Skill 根
- OpenClaw / WorkBuddy 已配置 Skill 根

## 相邻能力

| Skill/类别 | 可能相邻词 | 隔离判据 |
|---|---|---|
| `wenjing-video-narrative-designer` | 参考机制、叙事 | 本 Skill 分析原始参考；Narrative 只采用已锁抽象规则 |
| `script-to-seedance-storyboard` | 镜头语言、视频分镜 | 对方把文本改分镜；本 Skill 不生成分镜 |
| `knowledge-to-comic` | 镜头、视觉 | 对方创作漫画；本 Skill 只逆向分析参考视频 |
| `vidu-skills-1.3.1` | reference-to-video | 对方直接生成；本 Skill 不调用生成模型 |
| 未来 Orchestrator | 完整做视频 | 本 Skill 只响应精确单点分析口令 |

## 结论

无需改变职责或冻结 Artifact Contract。保留负向触发：“参考生视频/生图”若意图为生成调用，不触发本 Skill。
