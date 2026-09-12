# P2 · 报站、点将与验收

## 边界
只发出精确接棒话术并验收上站结果，不代替 Independent Skill。

## 执行
读取 `modules/handoff-phrases.md`，告诉用户当前站、执行件、必需输入、预期输出和放行条件。执行件返回后，只检查文件存在、状态/版本/完整性登记、Gate 决策及 open CR；通过则更新状态并再次路由，失败则写 owner 与最小重跑范围。

## 输出 schema
在 `00_project_state.md` 追加 handoff record：from/to/input/output/gate/result/time。

## Gate
锁、Gate 或职责冲突不得由总控修复或绕过。

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

╭─ Orchestrator · P2 站点验收 ─────────╮
│ 站点：{skill} · 结果：{PASS|BLOCKED}  │
│ 下一站/重跑：{target}                 │
╰─────────────────────────────────────╯

---
*全部必需站点通过后加载 `stages/03-close-and-resume.md`；否则按 P1 继续点将。*
