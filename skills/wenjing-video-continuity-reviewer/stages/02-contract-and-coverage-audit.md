# P2 · 契约与覆盖审计

## 边界
只查 Artifact schema、锁、路径、hash、coverage/readiness；不评价美学。

## 执行
按当前 mode 读取最小依赖闭包；核对 Script/Storyboard/Visual/generation 的版本与 hash、稳定 ID、Dialogue/knowledge coverage，以及 Storyboard 动态时长字段完整性。真实轨核对 required asset 存在与 READY；Dry Run 轨核对 planned specs 与明确延期字段。旧报告只有依赖 hash 未变才复用。

## 输出 schema
报告 DRAFT 增 `contract_checks[]`：check_id、required、result、expected、observed、evidence；动态时长缺失或 compatibility mirror 冲突定位到 Storyboard Director；更新 state。

## Gate
```
╭─ Continuity Reviewer · P2 完成 ───────────╮
│ contract checks：{pass}/{required}
│ blocker：{无|列表}
│ 下一步：P3 连续性与 Lock 审计
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不用文件名代替 hash；不接受缺失 required asset；不把 DRAFT 当 LOCKED；不静默补字段。

---
*P2 完成后加载 `stages/03-continuity-and-lock-audit.md`。*
