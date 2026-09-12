# P1 · 最短合法路由

## 边界
只依据 manifest 枚举和 Artifact 状态选择下一件 Skill，不做业务诊断。

## 执行
读取 `modules/downstream-skill-map.md`。CASE、SOURCE_LOCKED、KNOWLEDGE、STORY 已实现；参考分析分支对四者按需。先根据路线点将唯一入口，入口生成 Script LOCKED 后合流现有通用下游。从首个缺失/STALE/未通过 Gate 的必需 Artifact 点将 owner，记录 required/skipped/why_minimal。Dry Run 不询价、不等待外部服务。

## 输出 schema
把 route decision 与唯一 `next_skill` 写入 `00_project_state.md`。

## Gate
新增路线、核心 Skill 或职责变化立即停止走 CR；既定枚举路由为 AUTO/REVIEW。

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

╭─ Orchestrator · P1 完成 ─────────────╮
│ 路线：{route} · 下一件：{next_skill}  │
│ 跳过：{skipped}                       │
╰─────────────────────────────────────╯

---
*P1 完成后加载 `stages/02-dispatch-and-accept.md`。*
