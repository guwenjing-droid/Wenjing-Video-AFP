---
name: wenjing-video-orchestrator
version: 0.2.1
description: >
  文婧 AFP 视频生产系统的 Pattern 5 薄总控：当用户要从头启动、继续或查看一条完整的
  CASE、SOURCE-LOCKED、KNOWLEDGE 或 STORY 视频生产线时，读取项目 manifest/state，报站、按冻结路由点将
  Independent Skill、验收上站 Artifact，并从最近合法检查点恢复。
  【触发词覆盖】：启动 AFP 视频全流程 / 从头做一个管理学案例视频 / 继续整个视频生产项目 /
                查看 AFP 视频项目进度 / 恢复中断的视频产线 / 按最短路径完成案例视频 /
                运行文婧视频生产系统 / 帮我走完整视频产线 / 从头做知识视频 /
                忠实改编并走完整产线 / 从头做原创故事视频
  【触发隔离】：只响应跨多个阶段的全流程编排、恢复和进度请求。用户明确要事实锁、
              参考视频拆解、叙事、剧本、视觉圣经、分镜、连续性审查或 Seedance Prompt/
              生成时，应直接触发对应 Independent Skill；本总控不代跑、不复制其业务逻辑。
agent_created: true
partner: wenjing
skill_type: orchestrator
afp_spec_target: silver
---

# wenjing-video-orchestrator

只做四件事：读取状态、报站、规则点将、验收接棒。

## 核心纪律

1. 只读取 `00_project_manifest.yaml`、`00_project_state.md` 和当前站必需的 LOCKED Artifact；不扫描全部历史库。
2. 只调用满足目标所必需的 Skill；可选 Reference Analyzer 只在用户有参考分析意图或 manifest 选中时进入，且适用于四条已实现路线。
3. 验收只检查状态、版本、路径、完整性校验码和 Gate 决策；不重做业务判断。
4. 局部失败从最近合法检查点恢复；不受影响的 LOCKED Artifact 保持有效。
5. v0.1 验收遵循 `V0_1_DRY_RUN`；`DRY_RUN_GREEN` 只放行 DRY_RUN，不冒充真实媒体。

## HUD

```json
{
  "project_id":"",
  "content_route":"CASE",
  "supported_routes":["CASE","SOURCE_LOCKED","KNOWLEDGE","STORY"],
  "control_mode":"FAST|GUIDED|STRICT",
  "acceptance_profile":"V0_1_DRY_RUN|REAL_MEDIA",
  "current_station":"P0",
  "next_station":"",
  "route_decision":{"required_skills":[],"skipped_skills":[],"why_minimal":""},
  "artifact_gate":{"expected":"","status":"MISSING|READY|STALE|BLOCKED","path":"","sha256":""},
  "current_blocker":"",
  "resume_prompt":""
}
```

## Stage 路由

| Stage | Read | 只产出 |
|---|---|---|
| P0 恢复/建壳 | `stages/00-resume-or-intake.md` | 状态快照 |
| P1 最短合法路由 | `stages/01-route-plan.md` | route decision |
| P2 报站、点将、验收 | `stages/02-dispatch-and-accept.md` | handoff record |
| P3 完成/暂停/恢复 | `stages/03-close-and-resume.md` | completion/resume record |

## 按需模块

| 需要 | Read |
|---|---|
| 下游 Skill、输入/输出和放行条件 | `modules/downstream-skill-map.md` |
| state、STALE、局部重跑和 Continue | `modules/state-and-resume.md` |
| FAST/GUIDED/STRICT 与 Dry Run | `modules/gate-and-acceptance-policy.md` |
| 标准接棒话术 | `modules/handoff-phrases.md` |

## 首次上手

请提供项目引用 `project_ref`（可为本地项目目录，也可为 Document/Board object ref）；若是新项目，请提供内容路线、原料和目标受众。总控先通过 Adapter 读取项目状态，再展示当前站、可用锁定产物、最短合法路径和需要点将的 Independent Skill。开跑前可查看 `templates/用户核查清单.md`。

## 指令

`Next` 进入已报站的下一件｜`Back` 回最近合法检查点｜`Status` 查看进度｜`Continue {project_ref}` 恢复｜`Export` 列出 Artifact｜`Stop` 安全暂停并写状态。

## 禁止

- 不写事实锁、叙事、剧本、Visual Bible、Storyboard、QA 或模型 Prompt。
- 不调用图像/视频模型，不决定内容方向，不覆盖 LOCKED 文件。
- 不把未实现的 COMMERCIAL/BOOK_FASTLANE/SERIES_IP 路线伪装为可运行。
- 不因局部失败从头重跑，不把 Dry Run 或 Mock 结果说成真实媒体。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical Skill 只按 `wenjing-video-<name>` 调用，版本只读 metadata/发行 manifest，不依赖目录名，禁止从安装目录名推断。

v0.2.1；支持 CASE / SOURCE_LOCKED / KNOWLEDGE / STORY；Pattern 5 Orchestrator；AFP-SPEC provisional Silver。
