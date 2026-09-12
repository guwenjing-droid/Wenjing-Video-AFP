# P0 · 恢复或建立最小项目壳

## 边界
只定位项目状态和合法检查点，不执行业务工作。

## 执行
通过 Runtime Adapter 读取项目 manifest/state；存在时校验当前站所需 content_ref、状态、版本和完整性状态。不存在时使用模板建立最小壳，并把用户选择限制为 `CASE | SOURCE_LOCKED | KNOWLEDGE | STORY`；不创建业务 Artifact。把有效、缺失、失效和阻断项分别列出。

路线确定后，只检查该路线最短合法路径所需的 canonical skill id 是否可调用，不扫描未来路线。canonical id 固定为 `wenjing-video-<name>`，版本来自 Skill metadata/发行 manifest，不从安装目录名推断。缺失时逐项列出 `missing_skills`，立即 BLOCK 当前路线；不得自行模拟缺失 Skill。

## 输出 schema
更新 `00_project_state.md` 的 current/next station、selected refs、`required_skills/available_skills/missing_skills`、blocker 和 resume prompt。

## Gate
输入冲突或锁失效立即 BLOCK；正常恢复为 AUTO，新项目路线/目标按 control mode REVIEW/HARD。

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

╭─ Orchestrator · P0 完成 ─────────────╮
│ 检查点：{checkpoint} · 状态：{status} │
│ 下一步：P1 最短合法路由              │
╰─────────────────────────────────────╯

---
*P0 完成后加载 `stages/01-route-plan.md`。*
