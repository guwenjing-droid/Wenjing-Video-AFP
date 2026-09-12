# P6 · Lock & Handoff

> 只冻结 Script 并登记 Visual Bible 下一站，不自动代跑。

## 前置与冻结

确认双上游仍为 LOCKED 且 hash 匹配；P5 blocker=0；覆盖与批准记录完整。保留 `03_script_DRAFT.md`，另写 `03_script_LOCKED.md`，status/version/approval 固定。写完后计算整文件 SHA-256，只登记 manifest/state，不回写 LOCKED 正文。

state 记录 next_station=`wenjing-video-visual-bible`。输出直击口令：“根据这个 Script LOCKED 建立角色、场景和道具 Visual Bible。”不得创建视觉资产或自动运行下游。

## 输出 schema 与落盘

`03_script_LOCKED.md` + manifest/state；若需改 LOCKED，创建 CR 并传播 STALE。

## Hard Stop

```text
╭─ Script Studio · P6 完成 ─╮
│ LOCKED path / version / SHA-256
│ coverage / approval / next station
│ NEXT：结束 / Back / Edit(走 CR) / Export
╰──────────────────────────╯
```

不自动运行 Visual Bible。

---
*P6 是本 Skill 最后一站；交接后结束。*

