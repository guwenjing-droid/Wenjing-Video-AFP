# Routing Contract

Orchestrator 必须选择满足目标的最短合法路径，只读所需 Manifest、LOCKED Artifact 和必要资产。它不得代替 Independent Skill 生产业务 Artifact。

## 路由矩阵

| route | 顺序 |
|---|---|
| CASE | `wenjing-video-case-planner -> wenjing-video-narrative-designer -> wenjing-video-script-studio` |
| SOURCE_LOCKED | `wenjing-video-source-locked-adapter` |
| KNOWLEDGE | `wenjing-video-knowledge-pov` |
| STORY | `wenjing-video-story-studio` |
| common downstream | `wenjing-video-visual-bible -> wenjing-video-storyboard-director -> wenjing-video-continuity-reviewer(PREFLIGHT) -> wenjing-video-seedance-producer -> wenjing-video-continuity-reviewer(POSTGEN)` |

在 common downstream 中，Storyboard Director 先定义动态 `creative_required_duration`；Reviewer PREFLIGHT 签 Duration Sanity；Producer 再映射后端时长档。这个分层不新增 Stage。

`wenjing-video-reference-analyzer` 是所有路线的可选辅助分支。CASE 中交给 Narrative Designer；其余路线交给对应入口 Skill。它不能越过真值优先级，也不能直接生成 Script、Storyboard 或 Producer Prompt。

## 路由决策

1. 若用户只要求单个已知 Artifact，且合法上游已 LOCKED，则可直接调用对应 Skill。
2. 已存在且 hash 有效的 LOCKED Artifact 直接复用。
3. 局部失败从最近合法检查点恢复。
4. 在质量与约束等价时，选择更少步骤、上下文和高成本生成轮次。
5. 非 Seedance 真实生产在无兼容 adapter 时 Hard Stop；Dry Run 可继续输出后端无关计划并标记缺口。
6. Orchestrator 只检查当前 route 加已选可选分支所需的 canonical skill id；缺失项逐个列出并 BLOCK，不自行模拟，不要求扫描未来路线。

## 接棒成功条件

消费者必须识别生产者、schema major version、LOCKED 状态、version、content_ref、integrity_status 和必需字段。本地 hash 可用时 expected 与 actual 必须一致；任何一个不满足都不得自动接棒，未知内容不能靠推测补齐。
