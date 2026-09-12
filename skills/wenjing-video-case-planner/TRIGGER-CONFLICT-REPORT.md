# Trigger Conflict Report · wenjing-video-case-planner

## 1. 检查范围

已静态扫描当前可读取的 Codex、Agents 和 OpenClaw Skill 目录，重点比对管理案例、教学案例、视频化、漫画化、剧本、分镜、视觉资产和 Seedance 等语义。

## 2. 本件精确意图

只响应：

- 管理学/经济学教学案例的事实锁。
- 教学目标和 1–3 个知识点。
- 可戏剧化空间与禁止虚构边界。
- Case Truth Lock。

明确不响应完整视频、漫画生成、剧本、视觉资产、分镜、连续性审查或 Seedance 生成。

## 3. 相邻 Skill

| 现有 Skill | 相邻范围 | 隔离结论 |
|---|---|---|
| wanwu-manhua | 案例漫画化、角色、分镜、图像 | 不使用漫画化、知识漫画和把案例变成分镜等口令 |
| knowledge-to-comic | SCQA 案例转漫画分镜与图像 | 本件只生成 Truth Lock |
| one-min-script | 内容转短视频剧本 | 不使用写短视频脚本或一分钟剧本 |
| script-to-seedance-storyboard | 原文转 Seedance 分镜 | 不使用 Seedance 分镜或剧本改分镜 |
| novel-visual-element-extractor | 人物与场景视觉设定 | 本件不建立视觉资产 |
| pov-science-storyboard | 科普视频分镜 | 本件限定管理/经济教学案例的事实锁 |
| commercial-ad-storyboard | 商业广告分镜 | 路线、产物与触发词均不同 |

## 4. 家族内隔离

- 不使用总控宽口令：帮我完整做视频、开始视频项目、视频全流程。
- 不使用 Narrative 口令：增强钩子、设计传播性、情绪曲线。
- 不使用 Script、Visual、Storyboard、Continuity 或 Producer 的专用口令。

## 5. 结论

- 静态预检：PASS_WITH_ISOLATION。
- 完全相同的精确触发词：未发现。
- 需要 Committee 仲裁：0。
- 待 P9：在安装后的新会话分别测试主要触发、语义变体和隔离口令。
