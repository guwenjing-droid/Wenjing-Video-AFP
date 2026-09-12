# P0 · Resume & Input Validation

> 只恢复项目并验证双 LOCKED 输入，不写剧本。

## 执行

Read project contract 和 Truth/Narrative 只读政策。读取 manifest/state、Truth Lock、Narrative Lock、开放 CR；重算两个文件 SHA-256。任一 MISSING、非 LOCKED、STALE、hash/version 不一致或有阻断 CR，即留在 P0。

确认 Narrative 中采用的所有 fact_id、knowledge_id、boundary_id 在 Truth 中可解析；Reference provenance 只随 Narrative 读取，不直接打开原始 Reference Artifact。

## 输出 schema 与落盘

更新 `00_project_state.md`：两输入 path/version/hash/status、READY/MISSING/STALE/BLOCKED、block reasons、next_station。不得伪造上游。

## Hard Stop

```text
╭─ Script Studio · P0 完成 ─╮
│ Truth / Narrative：READY | BLOCKED
│ 完整性 / 引用解析
│ 下一步：P1 Script Brief
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────╯
```

不自动进入 P1；不得 Skip。

---
*P0 确认后加载 `stages/01-script-brief.md`。*

