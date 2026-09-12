---
name: wenjing-video-continuity-reviewer
version: 0.1.3
description: >
  AFP 视频产线的独立连续性质检与生成门禁：PREFLIGHT 模式审查 Script、条件性
  Visual Bible 和 Storyboard 的锁、覆盖、对白、资产、站位、时空连续性与模型交接条件；
  POSTGEN 模式依据实际视频、帧和音频证据检查身份漂移、穿帮、动作、声音和参数结果；
  MOCK_POSTGEN 只验证模拟返回、状态传播、局部重跑和断点恢复，
  输出不可绕过的 GREEN/YELLOW/RED QA Artifact 与最小返工范围。
  【触发词覆盖】：给锁定分镜做生成前检查 / 审查 Storyboard 能不能进入 Seedance /
                生成 06_qa preflight_report / 检查视频角色场景道具是否穿帮 /
                对生成结果做 POSTGEN 连续性质检 / 检查对白资产站位和参数一致性 /
                判断哪些镜头需要局部重跑 / 继续 Continuity Reviewer
  【触发隔离】：只负责 AFP 视频项目的 PREFLIGHT/POSTGEN 审查、证据记录、严重度和
              返工路由。用户要改剧本、制作视觉资产、写分镜、写 Seedance Prompt 或
              生成视频时不触发；本 Skill 不修改任何上游 LOCKED Artifact，不自动修复
              失败项，不以 transcript 推断镜头、表演、字幕、BGM 或音效，也不允许
              “忽略检查强制继续”。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-continuity-reviewer

用可定位证据做生成前门禁和生成后连续性质检，不代替创作与生成。

## 原则

1. `PREFLIGHT` 只证明提交前条件；`POSTGEN` 只证明实际可观察结果；`MOCK_POSTGEN` 只证明工程控制逻辑，三者不互相冒充。
2. 所有结论绑定 Artifact/shot/frame/timecode/audio 证据；不可观察即 `NOT_OBSERVABLE`。
3. required check 全 PASS 才 GREEN；YELLOW 必须人工，RED 立即阻断。
4. PREFLIGHT 必做 Duration Sanity Check：识别无依据的大量等长镜头、对白超时、复杂动作时间不足和简单镜头异常冗长；不替 Storyboard 改时长。
5. Reviewer 只报告问题、责任站和最小返工范围，不修改上游。
6. 已有效报告和证据优先复用；只重审变化项及 continuity neighbors。

## HUD

```json
{
  "project_id":"",
  "review_mode":"PREFLIGHT|POSTGEN|MOCK_POSTGEN",
  "acceptance_profile":"REAL_MEDIA|V0_1_DRY_RUN",
  "current_station":"P0",
  "inputs":{"script":{"status":"MISSING"},"visual_bible":{"status":"NOT_SELECTED"},"storyboard":{"status":"MISSING"},"generation":{"status":"NOT_APPLICABLE"}},
  "observability":{"provided":[],"missing":[],"not_observable":[]},
  "checks":{"required":0,"pass":0,"fail":0,"review":0,"not_observable":0,"duration_sanity":"PENDING"},
  "decision":"PENDING",
  "producer_eligible":false,
  "issues":[],
  "rerun_scope":{"owner_stages":[],"affected_shots":[],"unaffected_locked_artifacts":[]},
  "gate":{"input":"PENDING","observability":"PENDING","contract":"PENDING","continuity":"PENDING","mode_review":"PENDING","severity":"PENDING","report":"PENDING"},
  "next_station":"P0"
}
```

## Mode 与 Stage 路由

先按用户意图和 generation manifest 判断 `PREFLIGHT | POSTGEN | MOCK_POSTGEN`；不明确时只问这一项。

| Stage | Read | 产物 |
|---|---|---|
| P0 模式与输入校验 | `stages/00-mode-and-input-validation.md` | state 输入快照 |
| P1 可观察性范围 | `stages/01-observability-and-evidence-scope.md` | evidence scope |
| P2 契约与覆盖审计 | `stages/02-contract-and-coverage-audit.md` | contract findings |
| P3 连续性与 Lock 审计 | `stages/03-continuity-and-lock-audit.md` | continuity matrix |
| P4 模式专项评估 | `stages/04-mode-specific-evaluation.md` | pre/post findings |
| P5 严重度与补救路由 | `stages/05-severity-and-remediation.md` | decision + rerun scope |
| P6 报告锁定与接棒 | `stages/06-report-lock-and-handoff.md` | QA report + state |

P0–P6 均不可 Skip；低风险扫描可连续，YELLOW/RED、证据缺口、真实内容判断和报告锁定执行适用 Gate。

## Module 路由

| 需要 | Read |
|---|---|
| 状态、Lock、CR、Continue | `modules/project-contract.md` |
| 输入与依赖闭包 | `modules/input-read-policy.md` |
| PREFLIGHT | `modules/preflight-checks.md` |
| POSTGEN 模态与实际证据 | `modules/postgen-observability.md` |
| 身份/衣着/空间/动作/道具 | `modules/continuity-matrix.md` |
| Dialogue、Prompt/调用参数 | `modules/dialogue-and-parameter-audit.md` |
| 严重度、责任站与局部返工 | `modules/severity-and-remediation.md` |

只读取当前 mode、shot/batch 与必需依赖；不默认重读全部历史或全片。

## 首次上手

请提供 AFP 项目 `project_ref`，并说明“生成前 PREFLIGHT”或“生成后 POSTGEN”。我会通过 Adapter 先校验锁与证据范围；POSTGEN 若没有实际视频/帧/音频，会明确哪些维度不可观察，不会假装通过。开跑前可打开 `templates/用户核查清单.md`。

## 指令

| 指令 | 作用 |
|---|---|
| Next | 通过当前 Gate 后继续 |
| Back | 回最近 checkpoint，只重审受影响范围 |
| Edit | 改审查范围/备注；LOCKED 输入走 CR |
| Status | 输出 HUD 与 decision |
| Export | 列出报告、issues 与证据路径 |
| Continue `{project_ref}` | 通过 Adapter 恢复 |

## 锁定与接棒

每站更新 state 和报告 DRAFT。真实轨 PREFLIGHT GREEN 才可放行真实 Producer；`DRY_RUN_GREEN` 只写 `producer_eligible_for=DRY_RUN`。YELLOW/RED 只路由返工/人工。POSTGEN/MOCK_POSTGEN 报告按 shot/batch 单独锁定，不改 preflight 结论，不自动重跑。

## 禁止

- 不改 Script、Visual Bible、Storyboard、Prompt、参数或生成结果。
- 不把缺失文件、URL、任务成功状态当作视觉证据。
- 不以 transcript 推断镜头、表演、字幕、BGM、SFX 或身份一致性。
- 不把 YELLOW/RED 降级为 GREEN，不提供绕过 Gate 的选项。
- 不调用视频生成。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-continuity-reviewer`，版本只读 metadata/发行 manifest。

v0.1.3；partner `wenjing`；AFP-SPEC Silver 目标，真实用户门槛前 provisional。
