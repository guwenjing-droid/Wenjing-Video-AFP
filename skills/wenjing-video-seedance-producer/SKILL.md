---
name: wenjing-video-seedance-producer
version: 0.1.3
description: >
  AFP 视频产线的独立 Seedance 生产执行件：消费 LOCKED Storyboard、条件性视觉资产和
  GREEN PREFLIGHT（或仅用于 DRY_RUN 的 DRY_RUN_GREEN），把逐镜意图编译为可追溯的七段 Seedance Prompt 与调用参数，执行
  DRY_RUN、Pilot、逐镜或已授权批量生成，并记录 prompt hash、参考图顺序、模型参数、
  输出和重试范围。【触发词覆盖】：把锁定分镜编译成 Seedance Prompt / 生成 Seedance
  Pilot / 按分镜逐镜生成视频 / 批量提交已审查镜头 / 生成 generation manifest 和日志 /
  检查 Prompt 与调用参数一致 / 用 GREEN Preflight 生成 Pilot /
  为每个镜头写 Seedance 调用包 / 从失败镜头继续生成 / 继续 Seedance Producer。
  【触发隔离】：只负责 AFP 视频
  项目的模型适配、Prompt 编译、提交和工程记录；用户要改事实、叙事、剧本、视觉资产、
  Storyboard 或做 QA 时不触发。本 Skill 不修改任何上游 LOCKED Artifact，不内嵌
  Reviewer，不硬编码模型能力，也不在缺少 GREEN PREFLIGHT、当前能力档或成本授权时
  发起真实生成。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-seedance-producer

把已审查的模型无关分镜编译成 Seedance 请求并留下可恢复、可核验、可局部重跑的工程记录。本 Skill 是 Seedance 专用适配器，不代表系统必须选择 Seedance。

## 原则

1. 真实模式只消费 `decision=GREEN` 且 `producer_eligible=true` 的 PREFLIGHT；`DRY_RUN_GREEN` 只允许 DRY_RUN，不重做 Reviewer。
2. Prompt 每一项都必须回指 Storyboard、Visual Bible 或项目约束；不新增剧情、对白、角色、动作或镜头事实。
3. 模型 ID、参数范围、音频和参考能力来自当前 capability profile；不使用历史硬编码。
4. Storyboard 的 `creative_required_duration` 是创作需求；Producer 依据当前 profile 映射到最小且足够的后端时长档，并记录裁切计划。没有足够档位时返回 SPLIT_REQUIRED，禁止向下 clamp。
5. 真实调用前必须同时满足：有效锁与 hash、GREEN PREFLIGHT、`VERIFIED_CURRENT` 能力档、成本授权。
6. DRY_RUN 只证明接口、请求包与工程控制可运行；Mock 成败必须标 `is_mock=true`，不代表已生成视频，更不代表 POSTGEN 通过。
7. 失败镜头从最近合法检查点局部重跑；未受影响的 LOCKED Artifact 与成功结果继续有效。
8. 运行者拥有生成后端、模型档与成本模式选择权；若项目选择非 Seedance，记录路由结果并退出，不强制回落或越权执行。

## HUD

```json
{
  "project_id":"",
  "acceptance_profile":"REAL_MEDIA|V0_1_DRY_RUN",
  "run_mode":"DRY_RUN|PILOT|SHOT|BATCH",
  "backend_selection":{"selection_mode":"OPERATOR_CHOICE|AUTO_COST_AWARE","status":"PENDING","selected_provider":"","selected_model":"","selected_producer":"","candidates":[],"fallback_policy":"ASK_OPERATOR|DRY_RUN_ONLY"},
  "current_station":"P0",
  "inputs":{"storyboard":"MISSING","visual_bible":"NOT_SELECTED","preflight":"MISSING","capability_profile":"MISSING"},
  "scope":{"shot_ids":[],"pilot_shot_id":"","batch_id":""},
  "compilation":{"total":0,"ready":0,"blocked":0},
  "duration_mapping":{"mapped":0,"split_required":[],"excess_generation_seconds":0,"policy":"SMALLEST_SUFFICIENT_TIER"},
  "authorization":{"required":false,"status":"NOT_REQUIRED","max_generation_rounds":null},
  "execution":{"submitted":0,"succeeded":0,"failed":0,"not_submitted":0},
  "rerun_scope":{"from_checkpoint":"","affected_artifacts":[],"unaffected_locked_artifacts":[]},
  "gate":{"input":"PENDING","capability":"PENDING","compile":"PENDING","parity":"PENDING","cost":"PENDING","execution":"PENDING","handoff":"PENDING"},
  "next_station":"P0"
}
```

## Mode 与 Stage 路由

| Stage | Read | 产物 |
|---|---|---|
| P0 恢复与输入门禁 | `stages/00-resume-and-input-gate.md` | input snapshot |
| P1 后端、能力与模式解析 | `stages/01-capability-and-mode-resolution.md` | backend choice + capability binding |
| P2 Prompt 编译 | `stages/02-prompt-compilation.md` | per-shot Prompt Package |
| P3 请求一致性锁 | `stages/03-request-parity-lock.md` | READY/BLOCKED request records |
| P4 Pilot 与成本 Gate | `stages/04-pilot-and-cost-gate.md` | authorized execution plan |
| P5 执行与局部恢复 | `stages/05-execution-and-local-recovery.md` | request/output records |
| P6 日志固化与接棒 | `stages/06-manifest-log-and-handoff.md` | manifest + log + POSTGEN route |

P0–P6 均不可 Skip。DRY_RUN 也必须完成 P0–P6；P4 记录 `NOT_REQUIRED`，P5 可记录 `NOT_SUBMITTED` 或明确标识的 `MOCK_SUCCEEDED/MOCK_FAILED` 测试返回。

## Module 路由

| 需要 | Read |
|---|---|
| 状态、Lock、CR、Continue | `modules/project-contract.md` |
| 最短合法输入闭包 | `modules/input-read-policy.md` |
| 当前模型能力与字段映射 | `modules/seedance-capability-profile.md` |
| 七段 Prompt 编译 | `modules/prompt-compiler.md` |
| Dialogue、参考顺序与参数 parity | `modules/dialogue-reference-parameter-lock.md` |
| Pilot、批量与成本授权 | `modules/pilot-batch-and-cost-policy.md` |
| 外部调用、重试、manifest/log | `modules/generation-execution-and-logging.md` |

只读取当前 shot/batch 和必要依赖；历史素材不在运行时默认加载。

## 首次上手

请提供 AFP 项目 `project_ref` 和目标模式。开跑前可打开 `templates/用户核查清单.md` 逐阶段核对。若没有真实 Seedance 后端或成本授权，我会完成 DRY_RUN 请求包和日志，但明确标记 `NOT_SUBMITTED`；不会把模拟结果说成成片。

## 指令

| 指令 | 作用 |
|---|---|
| Next | 当前 Gate 合法后继续 |
| Back | 回最近 checkpoint，只重跑受影响镜头 |
| Edit | 修改本件 DRAFT；上游 LOCKED 变更走 CR |
| Status | 输出 HUD、scope 和 Gate |
| Export | 列出 Prompt、manifest、log 与输出路径 |
| Continue `{project_ref}` | 通过 Adapter 恢复 |

## 锁定与接棒

Prompt Package 锁定后记录其 sha256；请求提交时同时记录参考图有序数组与参数快照。实际输出存在且状态可核验时，才把对应 shot/batch 接棒给 `wenjing-video-continuity-reviewer` 的 POSTGEN 模式。无输出的 DRY_RUN 只结束在接口验证，不触发视觉结论。

## 禁止

- 不修改 Truth、Narrative、Script、Visual Bible、Storyboard 或 PREFLIGHT。
- 不把自身参数检查包装成 Reviewer 结论。
- 不硬编码模型 ID、支持能力、价格或固定 quality；价格未知时标 `COST_UNKNOWN`，不得声称最便宜。
- 不把 Storyboard 创作时长改写成后端固定档；不向下 clamp，不用统一 12 秒作为默认生成时长。
- 不把占位符、任务成功提示或 transcript 当成实际视频证据。
- 不在未授权时发起有成本的 Pilot/SHOT/BATCH。
- 不因单镜头失败默认全片重跑。
- 不接收非 Seedance 请求后仍由本 Skill 执行；应路由到已安装的兼容 Producer，缺少适配器则保持 `BACKEND_ADAPTER_MISSING` 或 DRY_RUN。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-seedance-producer`，版本只读 metadata/发行 manifest。

v0.1.3；partner `wenjing`；AFP-SPEC Silver 目标，真实用户门槛前 provisional。
