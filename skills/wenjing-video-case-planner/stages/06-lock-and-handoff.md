# P6 · Lock 与交接

> wenjing-video-case-planner · Stage 06  
> 目的：冻结经批准的 Case Truth Lock，登记完整性信息并把正式继承物交给 Narrative Designer。

## 一、前置条件与边界

只有同时满足以下条件才执行：

- P5 `review_status=READY_FOR_APPROVAL`
- 用户明确以 `Next` 批准当前 Draft
- Draft 文件存在且与用户看到的版本一致
- 没有开放的阻断级 Change Request

本阶段只执行冻结、登记和交接，不修改内容，不运行下游 Skill。

开始前 Read `modules/project-contract.md`。

## 二、锁定动作（原子化提交）

1. 读取 Draft，确认 status、version 和 Approval Log。
2. 将 status 改为 `LOCKED`，写入批准时间、批准者标识和来源 Draft 路径。
3. 生成新的正式文件：
   `{project_path}/stage-outputs/01_case_truth_lock_LOCKED.md`
4. 保留 Draft，不覆盖、不删除。
5. 完成所有正文、metadata、批准记录与非阻断风险的最终写入；从此刻起不得再修改该 LOCKED 文件。
6. 对最终 LOCKED 文件重新计算整文件 SHA-256。
7. 按同一提交单元把 `artifact_id/artifact_type/version/status/content_ref/storage_backend/sha256/integrity_status/upstream_refs/upstream_integrity/approved_by/updated_at` 同步写入 manifest 与 state；`integrity_status=VERIFIED` 仅在实际 hash 可计算且匹配时使用。
8. 重新读取 LOCKED 文件、manifest 与 state，复算实际 SHA-256，并验证两处 expected hash、version、status 完全一致。
9. 只有第 8 步通过才提交 P6 完成状态与下一站。不得把整文件 hash 写回 LOCKED 文件自身，以免形成自引用并改变被校验内容。

固定顺序为：`finalize artifact → compute hash → update registry/state → verify`。禁止先计算 hash 后继续修改 LOCKED Artifact，也禁止只更新 manifest 或只更新 state。

## 三、交接检查

逐项验证：

- LOCKED 文件存在且可读。
- status 确为 LOCKED。
- Source Registry、Final Fact Table、Teaching Goal、Knowledge Points、Dramatization Space、Forbidden List、Approval Log、Downstream Handoff 均存在。
- manifest/state 的 expected hash 均与文件 actual hash 一致，且 version/status 一致。
- 下游只需读取正式文件即可开始，不依赖本次对话。

任一项失败：保留可审计证据并标记 `integrity_status=FAIL`、`status=BLOCKED`，保持 `next_station=P6`，不得静默修正或声称交接成功。

## 四、输出 schema 与状态更新

更新：

- manifest：登记 case_truth_lock path、version、status、sha256；sha256 指向冻结后的 LOCKED 整文件。
- state：`current_station=P6`、`stage_status.case_planner=COMPLETE`、`next_station=wenjing-video-narrative-designer`、locked_artifacts、resume_prompt；state 的 hash 必须与 manifest 一致。
- resume_prompt：提示下游读取 manifest/state 和 `01_case_truth_lock_LOCKED.md`。

若下游 Skill 尚未安装，只记录下一站和直击口令，不伪装已经调用。

## 五、CHANGE_REQUEST 规则

锁定后发现问题：

1. 从 `templates/change-request-template.md` 创建 `change-requests/CR-{id}.md`。
2. 记录目标版本、原因、影响 fact/knowledge/boundary、拟议修改和受影响下游。
3. 用户批准后将本件及依赖产物标记 STALE，回到相应阶段修订。
4. 重新通过 HARD Gate 并发布新版本；禁止原地静默改写 LOCKED 文件。

## 六、Hard Stop · 最终交付确认单

这是本件最终 Hard Stop。完成后输出绝对路径、版本、hash、下一站和直击口令，然后停止。不得自动进入 Narrative Designer。

```text
╭─ 管理案例视频化事实规划器 · P6 完成 ─────╮
│ 🔒 状态：LOCKED
│ 📦 产物：{locked_absolute_path}
│ #️⃣ SHA-256：{sha256_from_manifest_and_state}
│ 💾 项目状态：已更新
│ 📍 下一站：wenjing-video-narrative-designer
│ 👉 Next：确认本件结束；不会自动运行下游
│ 🔗 直击口令：增强这个案例视频的钩子和传播性
╰──────────────────────────────────╯
```

## 七、反模式

- 不覆盖 Draft。
- 不在批准后继续顺手润色内容。
- 不只在对话里宣布 LOCKED 而不创建文件。
- 不遗漏 hash、批准记录或下一站。
- 不在下游不存在时声称已点将成功。

---

*P6 完成后，本 Skill 结束；正式继承物交给 `wenjing-video-narrative-designer`。*
