# P6 · Lock 与交接

> wenjing-video-narrative-designer · Stage 06  
> 目的：冻结获批 Narrative Plan，登记完整性信息并把正式继承物交给 Script Studio。

## 一、本阶段做什么

本阶段只执行冻结、登记与交接，不修改 Narrative 内容，不写剧本，也不自动运行下游 Skill。

开始前 Read `modules/project-contract.md` 与 `modules/truth-lock-read-policy.md`。

## 二、前置条件

必须同时满足：

- P5 `review_status=READY_FOR_APPROVAL`。
- GUIDED/STRICT 有用户明确 `Next` 批准；FAST 有 manifest 预授权记录且用户已在 P5 后 `Next`。
- Draft 文件存在，版本与用户/策略看到的版本一致。
- Truth Lock 仍为同一 LOCKED 版本/hash，未被标 STALE。
- FORBIDDEN=0、未决阻断 CONDITIONAL=0、未兑现 Hook=0。
- 没有影响本件的开放阻断级 Change Request。
- 若采用 Reference Analysis：所有 ref 仍为同一 LOCKED 版本/完整性登记，采用的 transfer rule 均通过 modality、observability、Truth、project constraint 与 originality Gate。

任一失败，保持 `next_station=P6|P5` 并 BLOCKED，不得声称交接成功。

## 三、锁定与完整性动作

1. 读取 Draft，核对 Contract Header、Review Summary 和 Approval Preview。
2. 复制为新的 `{project_path}/stage-outputs/02_narrative_plan_LOCKED.md`；保留 Draft，不覆盖、不删除。
3. 将 status 改为 LOCKED，写入版本、批准来源、批准时间和来源 Draft 路径。
4. 验证 12 节 schema、上游 path/version/hash、Decision/Approval Log 和 Downstream Handoff 完整；若存在 `reference_analysis_refs` / `adopted_transfer_rule_ids`，同时验证 provenance 与采用审计完整。
5. 冻结正式文件后计算其整文件 SHA-256，只登记到 manifest/state；不得把整文件 hash 写回 LOCKED 文件自身。
6. 更新 state 的 locked_artifacts、current/next station、resume_prompt 和时间戳。
7. 重新读取 manifest/state 并复算 hash；任一不一致则标 INVALID/BLOCKED。

## 四、下游交接契约

Script Studio 的正式输入：

1. `stage-outputs/01_case_truth_lock_LOCKED.md`
2. `stage-outputs/02_narrative_plan_LOCKED.md`
3. `00_project_manifest.yaml`
4. `00_project_state.md`

下游必须继承 immutable sections：Truth & Boundary Inheritance、Selected Strategy、Hook/Payoff Map、Narrative Nodes、Knowledge Map、Boundary Audit。若要修改，创建 Change Request 回到相应上游，不能静默改 LOCKED。

Reference Analysis 不增加 Script Studio 的直接必需输入。Script Studio 只读取 Narrative Plan 中已批准的抽象机制、`transfer_rule_id` 和适配说明，不得回到参考视频复制原内容。

## 五、输出 schema 与状态更新

- 正式产物：`{project_path}/stage-outputs/02_narrative_plan_LOCKED.md`。
- manifest：登记 narrative_plan path、version、status、sha256、locked_at、approved_by。
- state：`current_station=P6`、`stage_status.narrative_designer=COMPLETE`、`next_station=wenjing-video-script-studio`、locked_artifacts、resume_prompt。
- resume_prompt：要求下游读取两份 LOCKED、manifest/state，并先核对 hash 与 STALE。

若 Script Studio 尚未安装，只登记下一站和直击口令，不伪装已调用。

## 六、Change Request

锁定后需变更时，从 `templates/change-request-template.md` 创建 `change-requests/CR-{id}.md`，记录目标版本/hash、原因、影响节点/知识/边界、决策与需要重跑的下游。批准后将本件及依赖物标 STALE，生成新版本 Draft 并重新过 Gate；禁止原地覆盖旧 LOCKED。

## 七、Hard Stop · 最终交付确认单

```text
╭─ 管理案例视频叙事设计器 · P6 完成 ─────╮
│ 🔒 状态：LOCKED
│ 📦 产物：{locked_absolute_path}
│ #️⃣ SHA-256：{sha256_from_manifest_and_state}
│ 🔗 上游 Truth：{version}/{hash_match}
│ 💾 项目状态：已更新
│ 📍 下一站：wenjing-video-script-studio
│ 👉 Next：确认本件结束；不会自动运行下游
│ 🔗 直击口令：把 Truth Lock 和 Narrative Lock 写成正式视频剧本
╰──────────────────────────────────╯
```

这是本件最终 Hard Stop。即使下游已安装，也不得自动运行 Script Studio。

## 八、反模式

- 不覆盖或删除 Draft。
- 不在锁定过程中继续润色内容。
- 不把整文件 hash 写回被校验的 LOCKED 文件。
- 不遗漏上游版本/hash、批准记录或下一站。
- 不在下游不存在时声称接棒已完成。
- 不把 Reference Analysis 路径擅自升级成 Script Studio 的强制依赖。

---

*P6 完成后，本 Skill 结束；正式继承物交给 `wenjing-video-script-studio`。*
