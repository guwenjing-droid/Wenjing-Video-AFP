# P6 · Lock & Handoff

> 只冻结 Reference Analysis 并生成接棒信息；不自动运行 Narrative Designer。

## 前置复核

1. DRAFT 九区齐全；contract=`reference-analysis/0.1`。
2. G-RA-01/02 无 BLOCK；G-RA-03 仅保留 PASS 或已人工处理的 MEDIUM，HIGH 全 EXCLUDED。
3. 批准记录含批准人/方式/时间；不得从沉默推定批准。
4. reference_id、source paths、modality、scope、rule IDs 与 manifest 一致。

## 冻结

1. 保留 DRAFT，不覆盖。
2. 另写 `stage-outputs/00_reference_analysis/<reference_id>_LOCKED.md`，status=`LOCKED`，版本从 manifest 取得。
3. 写完后计算整文件 SHA-256；只登记到 reference manifest、project manifest/state，不回写 LOCKED 正文。
4. state 标记本 Artifact READY，登记 next_station=`wenjing-video-narrative-designer`（可选）。
5. 输出直击口令：“使用这个 Reference Analysis 为已锁定案例设计原创 Narrative Plan。”

## 接棒边界

- Narrative Designer 仍以 `Case Truth Lock > 用户/项目约束 > Reference Analysis` 采用。
- 本 Artifact 是可选输入；不产生 Truth Lock，不直接进入 Script Studio。
- 若没有 Case Truth Lock，只完成分析并提示接棒尚缺，不代替 Case Planner。

## 输出 schema 与落盘

LOCKED、reference manifest、project manifest/state；必要时创建 Change Request，不删除历史版本。

## Hard Stop

```text
╭─ Reference Analyzer · P6 完成 ─╮
│ LOCKED path / version / SHA-256
│ 可用规则 IDs / EXCLUDED IDs
│ 可选下一站：wenjing-video-narrative-designer
│ NEXT：结束 / Back / Edit(走 CR) / Export
╰──────────────────────────────╯
```

即使下游已安装，也不得自动运行或代写 Narrative Plan。

## 反模式

- 改名 DRAFT 代替独立 LOCKED；把 hash 写回被校验文件；自动点将下游；把 EXCLUDED 规则列为可采用。

---
*P6 是本 Skill 最后一站；交接后结束。*
