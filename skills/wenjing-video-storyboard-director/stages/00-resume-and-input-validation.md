# P0 · 恢复与输入校验

## 边界

只校验项目状态、Script Lock 与条件性 Visual Bible；不设计镜头。

## 执行

1. Read `modules/project-contract.md`、`modules/script-read-policy.md`。
2. 只读 manifest/state 与 Script LOCKED；校验路径、版本、状态、hash。
3. 从 manifest 判定 Visual Bible 为 `NOT_SELECTED | OPTIONAL_SELECTED | REQUIRED`，同时读取 acceptance profile；后两者 Read `modules/visual-bible-read-policy.md` 与 LOCKED manifest。Dry Run 只接受规格级接棒，真实轨仍要求实际 READY。
4. 从最近合法 checkpoint 恢复，列出 READY/MISSING/STALE/BLOCKED；保留无关锁定 sequence。
5. 输入不合法时 BLOCK，不代替上游修复。

## 输出 schema

落盘更新 `{project_path}/00_project_state.md` 的 input snapshot、selected paths、rerun scope、P0 Gate 与 next_station。

## Gate

```
╭─ Storyboard Director · P0 完成 ───────────╮
│ Script：{READY|BLOCKED} · Visual：{状态}
│ 恢复点：{checkpoint}
│ 下一步：P1 Story Unit Mapping
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不接受 DRAFT/STALE Script；不把 Visual Bible 缺失静默降级；不全库扫描；不信对话代替磁盘。

---
*P0 完成后加载 `stages/01-story-unit-mapping.md`。*
