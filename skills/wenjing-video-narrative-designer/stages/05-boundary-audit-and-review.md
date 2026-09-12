# P5 · 边界审计与 Draft 审批

> wenjing-video-narrative-designer · Stage 05  
> 目的：逐项核对 Narrative Draft 是否忠实继承 Truth Lock、兑现钩子并守住相邻 Skill 边界。

## 一、本阶段做什么

本阶段只审计、修复和展示 Draft；不生成 LOCKED，不写正式剧本、镜头或下游内容。

前置条件：P4 knowledge_coverage=100%，emotion_alignment=ALIGNED。Read `modules/boundary-audit.md`、`modules/anti-patterns.md`、`modules/truth-lock-read-policy.md`；审阅前 Read `modules/exemplars.md` 的反面例作对照。

## 二、审计逻辑

按顺序检查：

1. **上游完整性**：Truth Lock 路径、版本、hash 与 P0 一致，未新增 STALE/CR。
2. **事实忠实**：所有 promise、node、payoff 和知识解释均有 fact_id/knowledge_id/boundary 依据；限定词和不确定性未被强化。
3. **Boundary**：FORBIDDEN 零命中；所有 CONDITIONAL 都有已批准 decision_id；ALLOWED 没有暗中改变事实强度。
4. **Hook 兑现**：每个 Hook Promise 有明确 Payoff Node，内容与承诺等价。
5. **教学完整**：1–3 个知识点全部覆盖，目标受众与结尾学习状态一致。
6. **情绪与参与**：曲线有依据；参与机制服务教学且不诱导虚假互动。
7. **职责边界**：不得出现最终台词、逐场剧本、镜头、运镜、角色视觉、画风或模型参数。
8. **Reference Adoption（若使用）**：执行 G-RA-01 输入模态、G-RA-02 可观察性、G-RA-03 原创迁移和 G-ND-RA 采用审计；确认没有从 transcript 虚构视听信息，也没有复制 source-specific/do-not-copy 内容。
9. **Schema**：12 节必填区、Decision Log、Approval Log、Downstream Handoff 齐全；`reference_analysis_refs` 与 `adopted_transfer_rule_ids` 允许为空，但非空时必须完整。

## 三、审计结论与修复

- `READY_FOR_APPROVAL`：必填项齐全，FORBIDDEN=0，无阻断问题。
- `REVIEW_REQUIRED`：存在非核心风险或需用户裁决的 CONDITIONAL；留在 P5。
- `BLOCKED`：上游变更/hash 异常、关键事实无锚、钩子未兑现、教学方向缺失或越界内容未清除。

发现问题时按 issue_id 登记：severity、section、upstream_ref、evidence、required_action、owner。不得用“基本完成”绕过阻断项。

## 四、输出 schema 与落盘

更新 `{project_path}/stage-outputs/02_narrative_plan_DRAFT.md`：

- Boundary Audit：检查项、结果、证据、issue_id。
- Consistency Declaration：事实、钩子、知识、情绪、参与、职责边界。
- Review Summary：READY_FOR_APPROVAL / REVIEW_REQUIRED / BLOCKED。
- Approval Preview：即将冻结的版本、路径和不可变章节。
- Approval Log：当前仍为 PENDING；不得提前写 APPROVED。
- Reference Adoption Audit：每个 reference/transfer rule 的 modality、observability、Truth、project constraint、originality 结果和证据；未使用时写 `N/A`。

同步 state：`current_station=P5`、`next_station=P6|P5`、`boundary_audit=PASS|REVIEW_REQUIRED|BLOCKED`、`reference_input_modality=PASS|REVIEW|BLOCK|N/A`、`reference_observability=PASS|REVIEW|BLOCK|N/A`、`reference_originality=PASS|REVIEW|BLOCK|N/A`、`reference_adoption=PASS|REVIEW|BLOCK|N/A`、`final_lock=PENDING|APPROVED_BY_POLICY`、review_status、issues、blocker。

FAST 仅在 manifest 已有明确 narrative_lock 预授权、审计 PASS 且 Draft 完整展示后，才可记 `APPROVED_BY_POLICY`；仍须在本 Hard Stop 等待 `Next` 进入 P6。GUIDED/STRICT 的 `Next` 明确表示用户批准当前 Draft 冻结为 LOCKED。

## 五、Hard Stop · 最终审批

```text
╭─ 管理案例视频叙事设计器 · P5 完成 ─────╮
│ 🚦 审计：{READY_FOR_APPROVAL|REVIEW_REQUIRED|BLOCKED}
│ ⛔ FORBIDDEN 命中：{count}
│ 🟡 待裁决条件：{count}
│ 🪝 未兑现 Hook：{count}
│ 🎞️ Reference Gate：{PASS|REVIEW|BLOCK|N/A}
│ ✅ Draft：{draft_absolute_path}
│ 🔐 Lock 授权：{PENDING|APPROVED_BY_POLICY}
│ 📍 下一步：{P6 Lock|留在 P5 修复}
│ 👉 Next 批准/进入锁定 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

这是最终人工/策略 Review Gate。审计未达 READY_FOR_APPROVAL 时不得 `Next`；即使全部通过，也不得在本阶段直接创建 LOCKED 文件。

即使审计结果明确，也不允许自动推进到 P6。

## 六、反模式

- 不把审阅变成顺手重写上游事实。
- 不把 REVIEW_REQUIRED 当 PASS。
- 不在用户或预授权策略批准前写 LOCKED。
- 不遗漏 Hook 的承诺—兑现核对。
- 不只查事实而忽略相邻 Skill 越界。
- 不把“传播性强”当审计通过证据。
- 不因参考视频知名或数据表现好而跳过原创迁移审计。

---

*P5 完成后，主控加载 `stages/06-lock-and-handoff.md`。*
