# P3 · 完成、暂停与恢复

## 边界
只汇总可验证状态和写恢复点，不补做执行件工作。

## 执行
v0.1 完成需：8 个 Independent Skill 接口可用、真实案例逻辑纵向联跑、Visual/Storyboard/Preflight/Prompt/Mock QA/restart/resume 通过，且薄总控自测通过。真实媒体为 DEFERRED，不计 blocker。暂停时把最近合法检查点、受影响范围和 resume prompt 写盘。

## 输出 schema
更新 `00_project_state.md` 的 project status、completion profile、deferred validations、current blocker 与 resume prompt；输出 Artifact 清单。

## Gate
只有全部 v0.1 必需项通过才标 COMPLETE；延期项必须明确列出。

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

╭─ Orchestrator · P3 完成 ─────────────╮
│ v0.1：{COMPLETE|BLOCKED}              │
│ 延期真实媒体验证：{items}             │
╰─────────────────────────────────────╯

---
*P3 为最后阶段；新会话使用 `Continue {project_path}`。*
