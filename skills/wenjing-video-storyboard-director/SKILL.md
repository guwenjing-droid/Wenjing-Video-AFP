---
name: wenjing-video-storyboard-director
version: 0.1.3
description: >
  AFP 正式视频产线的模型无关分镜执行件：只在 Script 已 LOCKED 后，将场次、动作、
  Dialogue Lock 和知识节点映射为逐镜 JSON；按需继承 Visual Bible 的 READY 资产，
  完成动作原子化、镜头语法、站位、时长、声音与连续性审计后输出 Storyboard LOCKED。
  【触发词覆盖】：把已锁视频剧本拆成正式分镜 / 根据 Script Lock 做逐镜 Storyboard /
                把复杂动作拆成可生成镜头 / 生成 05_storyboard_LOCKED.json /
                为管理案例视频规划景别机位运镜 / 把 Visual Bible 接成分镜 /
                检查逐镜对白资产和空间连续性 / 继续 Storyboard Director
  【触发隔离】：只处理 AFP 项目中已有 Script LOCKED 的模型无关正式分镜。用户只有
              小说原文、要直接生成 Seedance 描述词、商业广告分镜或科普短视频分镜时
              不触发；剧本写作、canonical 资产生成、Preflight 审查、Seedance Prompt、
              模型参数和视频生成由其他 Independent Skill 负责。本 Skill 不改写锁定台词
              与事实，不把镜头描述冒充模型调用 Prompt。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-storyboard-director

把正式剧本转成可审计、可接棒、与生成模型解耦的逐镜执行包。

## 原则

1. Script LOCKED 只读，事实、顺序、知识点与 Dialogue Lock 不增不删。
2. 复杂动作先原子化，再选择满足叙事功能的最少合法镜头；每镜按对白、动作、镜头运动与理解成本推导最短充分时长，禁止用固定 10s/12s/15s 或全片等长作为默认。向运行者展示 ECONOMY / BALANCED / EXPRESSIVE 三档镜头预算，节省积分不得牺牲 Script、Dialogue、Knowledge、动作清晰度或连续性覆盖。
3. Visual Bible 仅按 manifest 条件加载；真实轨只引用 READY 资产，`V0_1_DRY_RUN` 只引用规格级 `planned_asset_refs`，两者不得混写。
4. 分镜描述止于镜头执行语法，不包含 Seedance 专属参数或提交调用。
5. 局部失败优先重跑 shot/sequence，不重做无关锁定内容。

## HUD

```json
{
  "project_id":"",
  "acceptance_profile":"REAL_MEDIA|V0_1_DRY_RUN",
  "current_station":"P0",
  "inputs":{"script":{"status":"MISSING","path":"","version":"","sha256":""},"visual_bible":{"requirement":"OPTIONAL","status":"NOT_SELECTED","path":"","sha256":""}},
  "storyboard":{"status":"MISSING","draft_path":"stage-outputs/05_storyboard_DRAFT.json","locked_path":"stage-outputs/05_storyboard_LOCKED.json","sha256":""},
  "coverage":{"story_units":0,"beats":0,"dialogue":0,"knowledge":0,"assets":0},
  "shot_budget_policy":{"mode":"PENDING_OPERATOR_CHOICE","minimum_legal_shots":null,"selected_shot_count":null,"estimated_generation_requests":null,"protected_coverage":["SCRIPT","DIALOGUE","KNOWLEDGE","ACTION_CLARITY","CONTINUITY"]},
  "duration_policy":{"mode":"SHORTEST_SUFFICIENT","speech_rate_profile":"","uniform_duration_default":false,"shots_explained":0,"split_required":[]},
  "rerun_scope":{"from_checkpoint":"","affected_shots":[],"unaffected_locked_sequences":[]},
  "gate":{"input":"PENDING","units":"PENDING","atoms":"PENDING","grammar":"PENDING","binding":"PENDING","audit":"PENDING","lock":"PENDING"},
  "open_change_requests":[],
  "next_station":"P0"
}
```

## Stage 路由

| Stage | Read | 产物 |
|---|---|---|
| P0 恢复与输入校验 | `stages/00-resume-and-input-validation.md` | state 输入快照 |
| P1 Story Unit Mapping | `stages/01-story-unit-mapping.md` | Storyboard DRAFT 骨架 |
| P2 Action Atomization | `stages/02-action-atomization.md` | action atoms |
| P3 Shot Grammar & Blocking | `stages/03-shot-grammar-and-blocking.md` | 构图/机位/运镜/站位 |
| P4 Timing/Dialogue/Audio/Asset Binding | `stages/04-timing-dialogue-audio-and-asset-binding.md` | 时长与锁定映射 |
| P5 Continuity & Boundary Audit | `stages/05-continuity-and-boundary-audit.md` | GREEN/YELLOW/RED 审计 |
| P6 Lock & Handoff | `stages/06-lock-and-handoff.md` | Storyboard LOCKED + state |

P0/P1/P5/P6 不可 Skip。低风险填充与校验按项目 Gate 频率连续；方向性镜头方案、冻结输入冲突和 LOCK 仍执行适用 Hard Gate。

## Module 路由

| 需要 | Read |
|---|---|
| 状态、Lock、CR、Continue、局部重跑 | `modules/project-contract.md` |
| Script 只读与 provenance | `modules/script-read-policy.md` |
| Visual Bible 条件读取与 READY 资产 | `modules/visual-bible-read-policy.md` |
| story units / beats | `modules/story-unit-method.md` |
| 复杂动作拆分 | `modules/action-atomizer.md` |
| 景别、机位、运动、构图、站位 | `modules/shot-grammar.md` |
| 最短充分时长推导与超载拆镜 | `modules/duration-estimation.md` |
| coverage、连续性、边界与 schema | `modules/continuity-and-boundary-audit.md` |

只加载当前 Stage 命中的 module、Script anchors 与必要资产；禁止默认遍历全部历史库或 Visual Bible 文件。

## 首次上手

请提供 AFP 视频项目 `project_ref`。我会通过 Adapter 先校验 `03_script_LOCKED.md`，再依据 manifest 判断是否需要读取 `04_visual_bible/asset_manifest_LOCKED.yaml`。开跑前可打开 `templates/用户核查清单.md`。

## 指令

| 指令 | 作用 |
|---|---|
| Next | 通过当前 Gate 后进入下一站 |
| Back | 回最近 checkpoint，只标记受影响 shots/sequences STALE |
| Edit | 改 DRAFT；LOCKED 或上游变更走 CR |
| Skip | 只跳明确 optional 项，关键 Gate 不可跳 |
| Status | 输出 HUD 和 READY/MISSING/STALE/BLOCKED |
| Export | 列出 DRAFT/LOCKED 与 hash |
| Continue `{project_ref}` | 通过 Adapter 按需恢复 |

## 续传与锁定

每站写 `00_project_state.md` 与同一 Storyboard DRAFT。恢复时校验依赖 hash，从最近合法 checkpoint 继续。P6 保留 DRAFT，另写 LOCKED 并登记整文件 SHA-256；不自动运行 Reviewer。

## 禁止

- 不新增、删除、重排 Script 事实/台词/知识点。
- 不生成或改写 canonical 角色、场景、道具资产。
- 不把不存在、未锁、非 READY 或完整性校验无效的媒体写入 `asset_refs`；Dry Run 规格只能进入 `planned_asset_refs`。
- 不写任何生成后端的 model、quality、mode、reference_images 或 API 调用；可估算镜头对应的生成请求数，但不选择或调用模型。
- 不为节省积分合并存在空间/时间切换、互斥站位、过载动作、台词缺口或连续性风险的镜头。
- 不把后端固定时长档写回创作时长；不得以统一 10s/12s/15s、强制 clamp 或无意义延长替代逐镜推导。
- 不执行 Preflight/Postgen QA，不调用视频生成。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-storyboard-director`，版本只读 metadata/发行 manifest。

v0.1.3；partner `wenjing`；AFP-SPEC Silver 目标，真实用户门槛前 provisional。
