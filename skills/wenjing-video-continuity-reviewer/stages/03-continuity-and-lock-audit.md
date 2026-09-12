# P3 · 连续性与 Lock 审计

## 边界
只对照锁定期望构建连续性矩阵；不修改镜头或资产。

## 执行
Read `modules/continuity-matrix.md` 与 `modules/dialogue-and-parameter-audit.md`。按 shot/neighbor 检查身份、服装、场景/光线、道具持有与状态、站位/视线/轴线、动作入口/出口、Dialogue/VO 和适用参数一致性。未观察维度保留 NOT_OBSERVABLE。

## 输出 schema
报告 DRAFT 写 `continuity_checks[]`，每项含 expected/source、observed/evidence、result、affected_shots。

## Gate
```
╭─ Continuity Reviewer · P3 完成 ───────────╮
│ continuity：PASS {N} / FAIL {N} / N/O {N}
│ 下一步：P4 模式专项评估
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不以“看起来差不多”判身份；不忽略邻镜入口/出口；不把参数一致等同结果一致。

---
*P3 完成后加载 `stages/04-mode-specific-evaluation.md`。*
