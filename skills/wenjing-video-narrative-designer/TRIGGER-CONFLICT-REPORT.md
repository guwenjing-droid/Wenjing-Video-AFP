# Trigger Conflict Report · wenjing-video-narrative-designer

## 1. 检查范围

已静态扫描当前可读取的 Codex、Agents 和 OpenClaw Skill 目录，重点比对管理案例、教学案例、视频叙事、钩子、情绪曲线、剧本、漫画、分镜和 Seedance 等语义。

## 2. 本件精确意图

只响应：

- 已有 Case Truth Lock 的管理/经济/教学案例视频叙事设计。
- Hook Promise、Participation、Narrative Nodes、Emotion/Knowledge Map。
- Narrative Plan DRAFT/LOCKED。
- 可选采用已经锁定的 Reference Analysis 抽象迁移规则。

明确不响应：事实锁定、原始参考视频拆解、完整视频制作、正式剧本/台词、漫画生成、角色/场景资产、分镜、连续性质检或 Seedance 生成。

## 3. 相邻 Skill 对比

| 相邻 Skill | 相邻范围 | 关键差异 | 结论 |
|---|---|---|---|
| `wenjing-video-case-planner` | 管理案例视频前置 | 上游只锁事实/教学/边界；本件只读其 LOCKED | PASS |
| `one-min-script` | 钩子、结构、情绪 | 从模糊想法直接做 60 秒可拍剧本/口播分镜；本件要求 Truth Lock 且不写剧本/镜头 | PASS_WITH_ISOLATION |
| `drama-episode-writer` | 情绪曲线、钩子 | 写竖屏漫剧逐集剧本并含分镜；本件只做管理案例 Narrative Plan | PASS_WITH_ISOLATION |
| `wanwu-manhua` | 案例叙事提案 | 继续生成角色、分镜和漫画图像；本件不输出视觉或图像 | PASS_WITH_ISOLATION |
| `knowledge-to-comic` | SCQA、案例传播 | 产出漫画分镜脚本及图像；本件只产 Narrative Lock | PASS_WITH_ISOLATION |
| `pov-science-storyboard` | 钩子、节奏、互动 | 第一人称科普完整分镜、旁白和音效；领域与产物均不同 | PASS |
| `script-to-seedance-storyboard` | 视频结构/节奏 | 将已有剧本改成 Seedance 分镜；本件不写模型专属分镜 | PASS |
| 未来 `wenjing-video-reference-analyzer` | Reference 机制 | 对原始参考视频做逆向分析；本件只消费其 LOCKED Artifact | PASS_BY_CONTRACT |
| 未来 `wenjing-video-script-studio` | 案例叙事落地 | 下游写正式剧本；本件不写最终台词、场次或动作稿 | PASS_BY_CONTRACT |

## 4. 高风险宽词处理

以下词不能单独作为本件触发：

- “设计钩子”
- “写故事”
- “写短剧”
- “做短视频”
- “设计情绪曲线”
- “增强传播性”

只有它们与“已有 Truth Lock / 管理案例视频 / Narrative Plan”等限定共同出现时，才进入本件。

## 5. 家族内隔离

- 不使用总控宽口令：“完整做视频”“开始视频项目”“视频全流程”。
- 不使用 Reference Analyzer 口令：“拆解这个视频”“学习这个爆款”“分析镜头语言”。
- 不使用 Script/Storyboard/Producer 口令：“写正式剧本”“逐镜分镜”“生成 Seedance Prompt”。

## 6. 结论

- 静态预检：`PASS_WITH_ISOLATION`。
- 完全相同的精确触发词：未发现。
- 需要修改职责或 Artifact Contract：0。
- 需要 Committee 仲裁：0。
- 待 P9：安装后测试主要触发、语义变体和不应触发口令。
