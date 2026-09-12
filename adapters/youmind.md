# YouMind Adapter

本方案不假设 YouMind 原生兼容 Codex/AFP Skill。应把整个发行包作为系统规格读取，而不是只上传某个 `SKILL.md`。

## 导入与识别

1. 把 README、Overview、Manifest、Contracts、12 个 Skill 目录和 Examples 一起加入同一项目知识空间。
2. 将 `wenjing-video-orchestrator` 识别为 Router/Coordinator；将其余 11 项识别为职责互斥的执行 Agent 或 Workflow 节点。
3. 不把多个 Skill 的方法揉成一个超长 Prompt。
4. 关键中文 `stages/`、`modules/`、`templates/` 在导入时本地展开或作为 UTF-8 文档保存；运行时不要依赖 CDN 外链再次读取。

## Board / Agent / Workflow 映射

| AFP 元素 | 建议映射 |
|---|---|
| Orchestrator | 主 Agent 或路由 Workflow |
| Independent Skill | 独立 Agent、子 Workflow 或模板化任务 |
| Artifact | Board 卡片或关联文档 |
| Artifact status | 卡片字段：DRAFT / APPROVED / LOCKED / STALE |
| Gate | 审批列、条件节点或自动校验任务 |
| State | 项目级结构化卡片或数据库行 |
| `content_ref` | document_id / object_ref |
| `storage_backend` | DOCUMENT_BOARD |
| source hash/version | 卡片元数据或不可变附件版本；不可观察时明确 NOT_OBSERVABLE |

Board 可按 `Intake -> Draft -> Review -> Locked -> Production -> QA` 展示，但必须另外保存 route、artifact ID、schema version、dependencies、hash、current stage 和 last checkpoint，不能只靠看板位置表达状态。

## 保持业务契约

- LOCKED 内容变更必须新建版本并令下游 STALE。
- Reference Analysis 只做可选输入；未提供模态保持 NOT_OBSERVABLE。
- Orchestrator 只路由，不代替执行 Agent 写业务 Artifact。
- 恢复从最后合法 checkpoint 开始。
- Dry Run 必须封锁所有外部媒体 Tool；真实 Tool 调用需单独授权与成本 Gate。
- 无 SHA-256 能力时保留空 `sha256` 并写 `integrity_status=NOT_OBSERVABLE`；V0_1_DRY_RUN 不因此自动 BLOCK，STRICT/真实生产可要求 VERIFIED。
- PREFLIGHT/RECHECK 使用独立 `preflight_report_v{n}` 文档，记录 supersedes、superseded_by、review_scope、affected_artifacts，不覆盖历史。

若 YouMind 的字段或自动化名称不同，可以改变实现形式，但不得降低以上语义。使用 [Document/Board Adapter](../runtime/document-board-adapter.md)；重新导入 v1.1 后，以现有样本做端到端无成本验证。
