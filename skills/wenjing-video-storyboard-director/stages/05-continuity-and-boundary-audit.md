# P5 · Continuity & Boundary Audit

## 边界

只审计 Storyboard DRAFT；不偷偷修上游或执行下游 Preflight。

## 执行

Read `modules/continuity-and-boundary-audit.md`，检查：Script/beat/action/dialogue/knowledge coverage；JSON schema 与稳定 ID；逐镜时长依据、异常等长、对白/动作下限、简单镜头冗长与超载拆镜；required asset binding closure；每个 ref 是单一 canonical asset_id、无斜杠组合简写；轴线/视线/站位/动作/道具/服装/光线连续性；Visual asset 状态/integrity；模型专属字段与越界职责。失败计算最小 shot/sequence 重跑范围。

## 输出 schema

审计结果写入 DRAFT `audit` 与 `{project_path}/stage-outputs/05_storyboard_audit.md`：

- GREEN：全部 required 检查通过，且无 required asset 未绑定、无非 canonical/组合 asset ref；
- YELLOW：歧义或人工方向复核，不能直接 LOCK；
- RED：事实、Dialogue、资产、连续性、schema 或边界失败，BLOCK。

## Gate

```
╭─ Storyboard Director · P5 完成 ───────────╮
│ 审计：{GREEN|YELLOW|RED}
│ coverage：{PASS|FAIL} · affected shots：{列表}
│ 下一步：P6 Lock & Handoff
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不把 YELLOW 当 GREEN；不由 Director 冒充 Reviewer；不因单镜失败重跑全片；不静默删除越界字段。

---
*P5 完成后加载 `stages/06-lock-and-handoff.md`。*
