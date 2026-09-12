# P6 · Lock 与 Continuity Reviewer 接棒

## 边界

只冻结 GREEN Storyboard 并登记接棒，不执行 Preflight 或视频生成。

## 执行

1. 验证 P0–P5 Gate、audit=GREEN、输入 hash 和开放 CR。
2. 保留 `05_storyboard_DRAFT.json`，另写 `05_storyboard_LOCKED.json`；不得覆盖改名。
3. 将 `status=LOCKED`、artifact/schema version、input refs、lock time 写入 LOCKED 文件，再计算整文件 SHA-256。
4. manifest/state 登记路径/hash，写 `next_station=wenjing-video-continuity-reviewer:PREFLIGHT`。
5. 只报告接棒条件，不自动调用下游。

## 输出 schema

- `{project_path}/stage-outputs/05_storyboard_LOCKED.json`
- `{project_path}/00_project_manifest.yaml`
- `{project_path}/00_project_state.md`

Reviewer 的最小输入为 Script Lock、Storyboard Lock、条件性 Visual Bible Lock；任何 hash/状态不符均 BLOCK。

## Gate

```
╭─ Storyboard Director · P6 完成 ───────────╮
│ Storyboard：LOCKED · hash：{值}
│ shots/sequences：{N}/{N}
│ 接棒：wenjing-video-continuity-reviewer PREFLIGHT
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不覆盖 DRAFT；不锁 YELLOW/RED；不在锁后润色；不把 Producer 参数塞入 Artifact；不自动运行 Reviewer。

---
*P6 是最后一个阶段，完成后输出全流程交付确认单。*
