# P0 · 恢复与输入校验

> Visual Bible · Stage 00

## 边界

只建立项目壳并验证 Script Lock、状态与所选资产；不盘点或生成资产。

## 执行

1. Read `modules/project-contract.md` 和 `modules/script-read-policy.md`。
2. 只读 manifest/state 与 `stage-outputs/03_script_LOCKED.md`；校验路径、LOCKED 状态、版本和 SHA-256。
3. 读取 manifest 明确选择的 style/identity/scene/prop references，记录权利、版本、hash 与兼容状态；不扫描未选素材。
4. 若 state 已存在，从最近合法 checkpoint 恢复，保留未受影响 LOCKED/READY 资产。
5. 缺失、hash 不符、STALE、权利不明或 Script 版本不兼容时标 BLOCKED，不代替 Script Studio 修复。

## 输出 schema

更新 `{project_path}/00_project_state.md`：`script_lock`、`selected_artifact_paths`、`rerun_scope`、P0 Gate 与 next_station。输入全绿才进入 P1。

## Gate

```
╭─ Visual Bible · P0 完成 ─────────────────╮
│ Script Lock：{READY|BLOCKED} · hash：{值}
│ 已选参考资产：{N} · 未选资产不加载
│ 恢复点：{checkpoint}
│ 下一步：P1 资产盘点
╰───────────────────────────────────────╯
```

Hard Gate 失败必须停；成功后按项目 Gate 频率继续。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不信对话记忆代替磁盘；不全库扫描；不接受 DRAFT/STALE Script；不静默重建有效资产。

---
*P0 完成后加载 `stages/01-asset-inventory.md`。*
