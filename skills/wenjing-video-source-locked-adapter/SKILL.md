---
name: wenjing-video-source-locked-adapter
version: 0.1.1
description: >
  SOURCE-LOCKED 视频入口：把用户指定的文章、小说、案例或原始剧本，在锁定来源范围后
  忠实转换为可拍、可演、可追溯的正式视频剧本，并输出兼容通用下游的
  03_script_LOCKED.md。【触发词覆盖】：忠实改编这篇文章 / 原文不增不删改成视频剧本 /
  保留全部台词做成可拍 Script / source locked adapter / 生成 SOURCE_LOCKED Script。
  【触发隔离】：自由原创故事交给 wenjing-video-story-studio；纯知识讲解交给
  wenjing-video-knowledge-pov；案例事实与教学边界交给 wenjing-video-case-planner；
  逐镜分镜、视觉资产、模型 Prompt 与媒体生成不由本 Skill 处理。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-source-locked-adapter

把“忠实于指定来源”落实为可验证的 Script，而不是凭感觉改写。

## 不可破坏原则

1. 先由用户锁定选定来源范围；范围外内容不进入，范围内内容不得静默遗漏。
2. 原始对白逐字保留；叙述可做等义、可观察转换，但不得改变人物、顺序、因果或结局。
3. 时长不足时提供“扩大时长/缩小来源范围”选择并 BLOCK；不得自行删减。
4. Reference Analysis 仅为可选机制输入，优先级为 `用户/来源事实约束 > Reference Analysis`。
5. 只到 `03_script_LOCKED.md`；不写镜头、运镜、字幕、音乐、音效或模型参数。

## HUD

```json
{"content_route":"SOURCE_LOCKED","current_station":"P0","source_lock":"MISSING","adaptation_plan":"MISSING","script":"MISSING","reference_analysis":"NOT_PROVIDED","coverage":{"selected_spans":0,"mapped_spans":0,"verbatim_dialogue":0},"gate":"PENDING","next_station":"P0"}
```

## Stage 路由

| Stage | 读取 | 结果 |
|---|---|---|
| P0 | `stages/00-resume-and-input-validation.md` | 输入/恢复快照 |
| P1 | `stages/01-source-scope-lock.md` | Source Lock |
| P2 | `stages/02-adaptation-plan.md` | Adaptation Plan |
| P3 | `stages/03-script-draft.md` | Script DRAFT |
| P4 | `stages/04-dialogue-and-coverage-lock.md` | 对白/来源覆盖 |
| P5 | `stages/05-fidelity-audit.md` | 审计决定 |
| P6 | `stages/06-lock-and-handoff.md` | Script LOCKED |

## Module 路由

- 状态/续传/CR：`modules/project-contract.md`
- 忠实度：`modules/source-fidelity-policy.md`
- 可选参考：`modules/reference-input-policy.md`
- 输出 schema：`modules/script-output-contract.md`

## 指令

`Next` 继续；`Back` 回最近检查点；`Edit` 改 DRAFT；`Skip` 仅跳可选 Reference；
`Status` 显示 HUD；`Export` 列出产物；`Continue {project_ref}` 通过 Adapter 恢复。

## 运行规则

- P0 只按需读取 manifest/state、用户指定来源和已选 Reference；不扫描历史资产库。
- FAST/GUIDED/STRICT 只改变展示与确认密度，不取消来源范围和最终 Script Hard Gate。
- 复用有效 LOCKED；局部失败只重跑受影响 span/scene，并传播 STALE。
- 外部媒体生成不在职责内；v0.1 测试只用 DRY_RUN/MOCK。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-source-locked-adapter`，版本只读 metadata/发行 manifest。

v0.1.1；AFP-SPEC Silver 目标，本地证据 provisional。
