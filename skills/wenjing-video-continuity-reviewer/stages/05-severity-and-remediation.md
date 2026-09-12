# P5 · 严重度与补救路由

## 边界
只分类 issue、指定责任站和最小复测范围；不执行修复。

## 执行
Read `modules/severity-and-remediation.md`。真实 PREFLIGHT 全 PASS=GREEN；Dry Run PREFLIGHT 的规格/合同检查全 PASS=`DRY_RUN_GREEN`；MOCK_POSTGEN 工程控制检查为 `MOCK_PASS|MOCK_FAIL`。需人工或 required 可观察不足=YELLOW；事实/Dialogue/当前档位关键输入/身份/空间/参数/安全失败=RED。每个 issue 绑定 owner_stage、affected scope、remediation 与 retest_from。

## 输出 schema
使用 `templates/issue-record.md` 写 issues；报告写 decision、producer_eligible、producer_eligible_for、rerun_scope。只有真实 PREFLIGHT GREEN 可 `producer_eligible=true`；DRY_RUN_GREEN 仅写 `producer_eligible_for=DRY_RUN`。

## Gate
```
╭─ Continuity Reviewer · P5 完成 ───────────╮
│ decision：{GREEN|YELLOW|RED}
│ issues：{N} · affected shots：{列表}
│ 下一步：P6 报告锁定与接棒
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不按平均分掩盖致命项；不把人工不确定写 PASS；不把修复建议当已修复；不整线返工。

---
*P5 完成后加载 `stages/06-report-lock-and-handoff.md`。*
