# wenjing-video-narrative-designer

把已锁定的管理学、经济学或教学案例事实组织成可审计的 Narrative Plan，供 `wenjing-video-script-studio` 继承。

## 能做什么

- 从 Case Truth Lock 提取受众、教学目标、知识点和改编边界。
- 比较 2–3 个钩子、叙事与参与策略。
- 设计模型无关的 Narrative Nodes、Hook–Payoff、情绪与知识映射。
- 可选读取 `wenjing-video-reference-analyzer` 产出的 Reference Analysis LOCKED Artifact，只迁移通过 Gate 的抽象机制。
- 生成 Draft，经审批和审计后冻结为 Narrative LOCKED。
- 通过 `00_project_state.md` 跨对话恢复。

## 不做什么

不修改 Truth Lock，不写最终台词、场次、正式剧本、角色视觉、镜头、Storyboard 或 Seedance Prompt。也不直接拆解原始参考视频；原始视频分析属于独立的 `wenjing-video-reference-analyzer`。

## 精确触发示例

- “为这个管理案例设计视频叙事结构。”
- “把已锁定的案例变成 Narrative Plan。”
- “给这个教学案例设计钩子和参与机制。”
- “用这个 Reference Analysis 为案例提出原创迁移方案。”

“锁定案例事实”“写正式剧本”“做分镜”“生成 Seedance Prompt”不属于本 Skill。

## 正式输入

必需：

```text
00_project_manifest.yaml
00_project_state.md
stage-outputs/01_case_truth_lock_LOCKED.md
```

可选：

```text
stage-outputs/00_reference_analysis/<reference_id>_LOCKED.md
```

采用优先级固定为：

```text
Case Truth Lock > 用户/项目约束 > Reference Analysis
```

Reference 缺失不阻断标准 CASE 流程。只有 transcript 时不得推断镜头、运镜、表演、字幕、音乐、音效或其他未提供的视听信息。

## 流程

1. P0：恢复与输入校验。
2. P1：Narrative Brief。
3. P2：钩子与参与策略。
4. P3：Narrative Nodes。
5. P4：情绪与知识映射。
6. P5：边界审计与 Draft 审批。
7. P6：Lock 与 Script Studio 交接。

方向性选择、CONDITIONAL 裁决和最终锁定保留 Hard/Review Gate；不得越过。

## 核心产物

```text
stage-outputs/02_narrative_plan_DRAFT.md
stage-outputs/02_narrative_plan_LOCKED.md
```

LOCKED 文件是正式继承物。若使用 Reference Analysis，Narrative Plan 会记录 `reference_analysis_refs` 和 `adopted_transfer_rule_ids`；Script Studio 不直接依赖原始参考视频。

## 断点恢复

```text
Continue {project_ref}
```

Skill 会读取 manifest、state、LOCKED Artifacts 和开放 Change Request，列出 READY/MISSING/STALE/BLOCKED 后从下一安全站恢复。

## 用户监督

开跑前查看 `templates/用户核查清单.md`。LOCKED 变更必须创建 `change-requests/CR-{id}.md`，不能原地覆盖。

## 包结构

- `SKILL.md`：薄路由、HUD、触发隔离和通用指令。
- `stages/`：P0–P6 的时序流程。
- `modules/`：项目契约、Truth 只读、叙事策略、参与、审计、反模式和局部示例。
- `templates/`：Narrative Plan、manifest、state、Change Request 和用户核查清单。
- `tests/`：P9 建立核心 fixtures、契约测试和接棒测试。
- `TEST-LOG.md`：P9 结果、限制和待补运行验收。

## 方法来源

方法机制定向提炼自用户历史资产 `桃子AI写爽文指令.txt`、`内容转1分钟剧本 v2.0.txt`、`AI猫微信文章.txt`，并辅参 `编剧.txt`。历史 Prompt 只提供方法来源，没有被原样拼接成 Skill。

## MVP 与后续增强

v0.1 优先保证可运行、可测试、可接棒。更多完整示例、平台差异说明和低风险表达优化进入 v0.2 backlog，不阻塞当前版本。

## P9 本地工程验收

- 契约测试：40/40 PASS。
- Artifact 接棒测试：14/14 PASS。
- 当前状态：Bronze Local Ready；Silver provisional。
- 待补：干净新会话运行测试、3 位真实用户、Analyzer 建成后的真实专项接棒、项目级真实案例纵向联跑。

## 版本

- v0.1.0：核心 Narrative Designer MVP；初始版本已包含 CR-001 的可选 Reference Analysis 接口，不改变七阶段职责和正式输出。
