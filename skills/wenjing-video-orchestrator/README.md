# wenjing-video-orchestrator

文婧 AFP 视频生产系统的薄总控。它编排 11 个 Independent Skill，只负责报站、点将、验收和断点恢复。

## 使用

说“启动 AFP 视频全流程”，或“继续整个视频生产项目 {绝对路径}”。明确的单件任务请直接触发对应 Independent Skill。

v0.1 默认验收档为 Dry Run：真实案例内容走完整逻辑链，图像/视频生成使用规格、Prompt、参数与 Mock 结果；真实媒体延期到首次生产。

## 边界

总控不创作、不审美、不写 Prompt、不调用生成模型。当前正式路线为 CASE、SOURCE_LOCKED、KNOWLEDGE、STORY；四者在 `03_script_LOCKED.md` 合流复用通用下游。COMMERCIAL、BOOK_FASTLANE、SERIES_IP 仍返回 NOT_IMPLEMENTED/BLOCKED。

## 版本

- v0.1.0（2026-09-11）：首个 MVP，支持 CASE、可选参考分析、Dry Run 与局部恢复。
- v0.2.0（2026-09-11）：新增 SOURCE_LOCKED、KNOWLEDGE、STORY 三个入口路由，通用下游和冻结 Script contract 不变。
