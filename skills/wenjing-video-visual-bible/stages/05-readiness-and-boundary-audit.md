# P5 · Readiness 与边界审计

> Visual Bible · Stage 05

## 边界

只审计已建规范与资产，不偷偷补写 Script、Storyboard 或视频 Prompt。

## 审计

Read `modules/readiness-and-boundary-audit.md`，逐项执行：

1. Script coverage 与 evidence anchor；
2. 真实生产轨检查实际文件存在、可读、完整性校验码匹配；Dry Run 轨明确记为 DEFERRED；
3. style、identity、服装、空间和道具状态一致；
4. rights/source/version/复用兼容记录完整；
5. required asset 依赖闭包在当前验收档位全部就绪；不得混淆 dry-run readiness 与 real readiness；
6. 禁止字段扫描：镜号、运镜、Seedance 参数、视频生成调用、擅改剧本；
7. 对失败项计算最小 `rerun_scope`，不影响的 LOCKED/READY 资产保留。

## 输出 schema

落盘 `stage-outputs/04_visual_bible/readiness_report.md`，结论仅允许：

- `REAL_GREEN`：所有 required assets 实际 READY，可进入真实生产；
- `DRY_RUN_GREEN`：所有 required specs 与 planned references 就绪，只可进入 Dry Run；
- `YELLOW`：只缺非关键或需人工确认项，不可冒充完整 ready；
- `RED`：必需资产/边界/来源/hash 失败，BLOCK。

## Gate

P5 是 HARD/AUTO 组合：`REAL_GREEN` 仍需核心身份资产审阅；`DRY_RUN_GREEN` 只冻结规格级包。YELLOW/RED 不得进入 Lock。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

```
╭─ Visual Bible · P5 完成 ─────────────────╮
│ 审计：{GREEN|YELLOW|RED}
│ READY：{N}/{required} · 最小重跑范围：{列表}
│ 下一步：P6 Lock 与接棒
╰───────────────────────────────────────╯
```

## 反模式

- 不以任务提交成功代替文件成功；不跳过 hash；不把 YELLOW 写成 GREEN；不因局部失败整线重跑。

---
*P5 完成后加载 `stages/06-lock-and-handoff.md`。*
