---
name: wenjing-video-knowledge-pov
version: 0.1.1
description: >
  KNOWLEDGE 视频入口：把纯知识、科普或课程概念先锁定为有证据边界的知识真值，
  再选择 POV、讲解或视觉隐喻表达，写成兼容通用下游的 03_script_LOCKED.md。
  【触发词覆盖】：把这个知识点做成视频 / 做第一人称科普 / 课程概念讲解视频 /
  知识短视频 Script / knowledge POV / 生成 KNOWLEDGE Script。
  【触发隔离】：具体管理/经济案例事实由 wenjing-video-case-planner；已有文章小说剧本
  忠实改编由 wenjing-video-source-locked-adapter；纯原创剧情由 wenjing-video-story-studio；
  逐镜分镜、视觉资产、模型 Prompt 和真实媒体生成由通用下游负责。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-knowledge-pov

把知识“讲懂且不讲错”，POV 是可选表达模式，不是强制模板。

## 原则

1. 先锁 claim、证据状态、限定词和教学边界；未知不得伪装为事实。
2. 表达模式从 `POV_IMMERSIVE | EXPLAINER | VISUAL_METAPHOR` 中按内容选择。
3. 钩子、反差和悬念不能制造错误因果；核心知识 100% 覆盖或经用户批准缩小范围。
4. Reference Analysis 可选，优先级 `用户/知识事实约束 > Reference Analysis`，只迁移机制。
5. 只输出 Script，不写镜头、运镜、字幕/BGM/音效判断、模型 Prompt 或生成参数。

## HUD

```json
{"content_route":"KNOWLEDGE","current_station":"P0","knowledge_truth_lock":"MISSING","knowledge_narrative_plan":"MISSING","script":"MISSING","presentation_mode":"UNSET","reference_analysis":"NOT_PROVIDED","coverage":{"claims":0,"knowledge_points":0},"gate":"PENDING","next_station":"P0"}
```

## Stage 路由

| Stage | Read | 结果 |
|---|---|---|
| P0 | `stages/00-resume-and-input-validation.md` | 输入/恢复快照 |
| P1 | `stages/01-knowledge-truth-lock.md` | Knowledge Truth Lock |
| P2 | `stages/02-presentation-plan.md` | Knowledge Narrative Plan |
| P3 | `stages/03-script-draft.md` | Script DRAFT |
| P4 | `stages/04-claim-and-coverage-lock.md` | Claim/knowledge coverage |
| P5 | `stages/05-rigor-and-teaching-audit.md` | 审计决定 |
| P6 | `stages/06-lock-and-handoff.md` | Script LOCKED |

模块按需读取：`project-contract.md`、`knowledge-evidence-policy.md`、`reference-input-policy.md`、`script-output-contract.md`。

## 指令与运行

`Next / Back / Edit / Skip / Status / Export / Continue {project_ref}`。Skip 只能跳可选 Reference 或可选表现层，不得跳知识真值与 Script Gate。FAST 可合并展示，GUIDED/STRICT 提高确认密度；局部 claim/scene 失败局部重跑。只读当前依赖闭包，复用有效 LOCKED。v0.1 只做 DRY_RUN/MOCK。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-knowledge-pov`，版本只读 metadata/发行 manifest。

v0.1.1；AFP-SPEC Silver 目标，本地证据 provisional。
