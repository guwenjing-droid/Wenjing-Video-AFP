# Artifact Contracts

本文件定义跨平台必须保留的业务接口。文件名可以由 adapter 映射，但 Artifact ID、schema version、状态、来源、依赖、Gate 结果和完整性字段不可省略。

## 通用信封

每个正式 Artifact 至少包含：

| 字段 | 含义 |
|---|---|
| `artifact_id` | 项目内唯一 ID |
| `artifact_type` / `schema_version` | 契约身份与版本 |
| `project_id` / `route` | 所属项目和路线 |
| `status` | DRAFT、APPROVED、LOCKED、STALE 或 REJECTED |
| `content_ref` / `storage_backend` | 平台无关内容引用及其 Adapter 类型 |
| `created_at` / `created_by` | 时间和生产 Skill |
| `source_artifacts` | 上游 ID、版本和 SHA-256 |
| `observability` | OBSERVED、INFERRED 或 NOT_OBSERVABLE |
| `gate_result` | 最近 Gate、结果与证据 |
| `sha256` / `integrity_status` | 可观察 hash 与 `VERIFIED/NOT_OBSERVABLE/DEFERRED/FAIL` |
| `upstream_refs` / `upstream_integrity` | 上游身份、版本与完整性结论 |
| `approved_by` / `updated_at` | 批准者与更新时间 |

LOCKED Artifact 不可原位改写。任何有效变更都要产生新版本，并按 [state-resume-rules.md](state-resume-rules.md) 传播 STALE。

锁定提交固定为 `finalize artifact → compute hash → update registry/state → verify`。本地 hash 可用时，消费者必须验证 status、version、expected hash 与 actual hash；不一致立即 BLOCK，不得静默修正。无 hash 能力的平台保留空 `sha256` 并写 `NOT_OBSERVABLE`，禁止伪造。

## Reference Analysis LOCKED

- Schema：`reference-analysis/0.1`
- 生产者：`wenjing-video-reference-analyzer`
- 内容：输入模态清单、Content Intelligence、Narrative Reverse Engineering、Engagement Engineering、Audiovisual Grammar、Transfer Engine。
- 强制约束：未提供的模态必须为 `NOT_OBSERVABLE`；不得从 transcript 虚构镜头、表演、字幕、音乐或音效。
- 消费者：CASE 的 Narrative Designer；SOURCE_LOCKED、KNOWLEDGE、STORY 的对应入口。
- 优先级：CASE 为 `Case Truth Lock > 用户/项目约束 > Reference Analysis`；其他路线为 `用户/来源/内容真值 > Reference Analysis`。

## CASE 专用上游

- `Case Truth Lock`：事实、证据范围、知识点、教学目标、可戏剧化空间和禁止虚构项。
- `Narrative Plan LOCKED`：Narrative Nodes、Hook、Setup、Escalation、Turning Point、Payoff、Ending、情绪曲线及已采用/拒绝的迁移规则。
- CASE Script 只有在上述必需输入均 LOCKED 后才能进入 LOCKED。

## Script LOCKED

- Schema：`script/0.1`
- 标准文件：`03_script_LOCKED.md`
- 生产者：CASE 使用 Script Studio；其他三条路线使用各自入口 Skill。
- 必需内容：路线与真值来源、场次、角色、动作、逐字对白/旁白、知识或剧情节点、禁改边界、覆盖审计。
- 必需锁：`truth_lock` 与适用于路线的 `narrative_lock` / `source_lock` / `story_lock`。
- 消费者：Visual Bible 和 Storyboard Director。

## Visual Bible LOCKED

- 生产者：`wenjing-video-visual-bible`
- 内容：角色身份锚、场景、道具、服装状态、风格与多视图参考规范、复用来源和 readiness。
- Dry Run 允许规格锁定但不得把未生成资产标为真实 READY；真实资产必须记录 URI、版本和可验证哈希。

## Storyboard LOCKED

- 生产者：`wenjing-video-storyboard-director`
- 格式：逐镜结构化 JSON。
- 内容：shot ID、时间、景别、构图、动作原子、对白锁引用、资产引用、连续性进出状态、视听意图及模型无关生成要求。
- 动态时长：每镜必须记录 `estimated_duration`、`creative_required_duration`、`duration_basis` 和 `duration_driver=SPEECH|ACTION|CAMERA|COMPREHENSION|MIXED`；`duration_seconds` 仅作等值兼容镜像。
- 时长边界：禁止固定 10/12/15 秒或全片等长默认；超载对白/动作优先拆镜；Storyboard 不包含后端固定档位。
- 每个对白、知识节点和必需动作必须可回溯到 Script。
- 每个 `required=true` 资产至少被一个 shot 引用；每个引用只含一个 canonical asset_id，禁止 `CHR-001/002` 等组合简写。Storyboard 自审与 Reviewer 都必须检查。

## Continuity Gate Artifacts

- PREFLIGHT：检查锁、覆盖、对白、资产、站位、时空连续性和 Producer 接棒条件。
- PREFLIGHT Duration Sanity：检查异常等长、对白超时、复杂动作/运镜时间不足、简单镜头冗长和超载未拆镜。
- 真实生产允许令牌：`GREEN`。
- 无成本演练允许令牌：`DRY_RUN_GREEN`，只授权 Dry Run。
- POSTGEN：真实媒体时检查可观察视听结果；Mock 时只能检查契约、状态与模拟返回，视听质量为 `NOT_OBSERVABLE`。
- PREFLIGHT/RECHECK 报告使用 `preflight_report_v{n}`，包含 `supersedes/superseded_by/review_scope/affected_artifacts`；不得覆盖历史报告。

## Producer Artifact

- 生产者：当前为 `wenjing-video-seedance-producer`。
- 输出：逐镜 Prompt、模型参数、参考资产清单、generation plan、成本/镜头策略、返回状态和 provenance。
- 时长映射：保留 Storyboard creative 值，另写 `selected_generation_duration`、`mapping=EXACT|ROUND_UP_AND_TRIM|SPLIT_REQUIRED`、裁切余量与 profile 来源；禁止向下 clamp。
- 必须声明 `run_mode: DRY_RUN | REAL`、`backend`、`external_calls` 和 `estimated_cost`。
- 非 Seedance 后端没有兼容 adapter 时返回 `BACKEND_ADAPTER_MISSING`，不可伪装执行。

## 最小合法链

四条路线必须先产生兼容 Script LOCKED；Visual Bible 是否产生真实资产取决于项目，但 Storyboard、PREFLIGHT 和 Producer Dry Run 仍须保持引用完整。路由细节见 [routing-contract.md](routing-contract.md)。
