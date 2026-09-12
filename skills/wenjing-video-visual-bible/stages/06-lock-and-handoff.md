# P6 · Lock 与 Storyboard 接棒

> Visual Bible · Stage 06

## 边界

只冻结通过审计的 Visual Bible manifest 并登记接棒；不运行 Storyboard Director。

## 执行

1. 确认 readiness report 为 `REAL_GREEN` 或当前档位合法的 `DRY_RUN_GREEN`，P0–P5 Gate 合法，无影响本件的开放 CR。
2. 真实轨校验所有 required asset 的路径、version、sha256、readiness 与依赖；Dry Run 轨校验 spec paths、provenance、`dry_run_readiness` 与空真实媒体声明。
3. 保留 `asset_manifest_DRAFT.yaml`，另写 `asset_manifest_LOCKED.yaml`；禁止覆盖改名。
4. 计算 LOCKED manifest 整文件 SHA-256，登记到 project manifest/state。
5. state 写 `current_station=visual_bible_complete`、`next_station=wenjing-video-storyboard-director`，并记录 ready asset paths；不自动调用下游。

## 输出 schema

- `stage-outputs/04_visual_bible/asset_manifest_LOCKED.yaml`
- 更新 `00_project_manifest.yaml`
- 更新 `00_project_state.md`

接棒最小输入：Script Lock + Visual Bible LOCKED manifest。真实轨还需 manifest 中所列 READY 文件；Dry Run 轨只传 `planned_asset_refs`，不得消费或假装存在真实媒体。下游不得消费 DRAFT、STALE、BLOCKED 项。

## Gate

```
╭─ Visual Bible · P6 完成 ─────────────────╮
│ Visual Bible：LOCKED · hash：{值}
│ Required assets：real {N}/{N} READY · dry-run {N}/{N} READY
│ 接棒：wenjing-video-storyboard-director
╰───────────────────────────────────────╯
```

LOCK 必须满足编排方案 Gate；未获合法确认/预授权不得假装完成。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不覆盖 DRAFT；不把缺失资产标成实际 READY；不把目录 hash 当文件 hash；不自动进入下游；不把 Storyboard 字段塞入 manifest。

---
*P6 是最后一个阶段，完成后输出全流程交付确认单。*
