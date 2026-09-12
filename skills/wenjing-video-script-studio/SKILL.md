---
name: wenjing-video-script-studio
version: 0.1.1
description: >
  管理学、经济学或教学案例视频的正式剧本执行件：只在 Case Truth Lock 与
  Narrative Plan 均已 LOCKED 后，把叙事节点写成可拍场次、人物动作、逐字台词、
  旁白和知识植入，完成事实/边界/可拍性审计后输出 Script LOCKED Artifact。
  【触发词覆盖】：把已锁 Narrative Plan 写成正式视频剧本 / 根据 Truth Lock 和
                Narrative Lock 写剧本 / 写这个管理案例视频的逐字台词 /
                把叙事计划落实成场次和对白 / 生成 03_script_LOCKED /
                继续 Script Studio / 正式案例视频剧本
  【触发隔离】：只处理已有 Truth Lock + Narrative Lock 的正式案例视频剧本。
              用户只有模糊创意、要快速写 60 秒剧本骨架时不触发；用户要写连载漫剧
              或爽剧时不触发；用户要设计钩子结构时由 wenjing-video-narrative-designer
              响应；角色视觉资产、逐镜分镜、Seedance Prompt 和视频生成由后续独立
              Skill 响应。本 Skill 不把“场次/动作”扩写成机位、运镜或模型参数。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-script-studio

把锁定的事实与叙事计划写成可拍、可演、可追溯的正式剧本。

## 原则

1. Truth Lock 与 Narrative Lock 只读，任一无效即停止。
2. 每个场次、动作、台词和知识点保留上游 provenance。
3. “能拍”只到场景、表演动作、对白/旁白；不写机位、运镜或生成 Prompt。
4. 时长、平台和声音形式来自项目约束，不硬编码旧 Prompt 参数。
5. DRAFT 经审计和批准后另写 LOCKED，不自动运行下游。

## HUD

```json
{
  "project_id": "",
  "current_station": "P0",
  "inputs": {
    "truth_lock": {"status":"MISSING","path":"","version":"","sha256":""},
    "narrative_lock": {"status":"MISSING","path":"","version":"","sha256":""}
  },
  "script": {"status":"MISSING","draft_path":"","locked_path":"","version":"","sha256":""},
  "coverage": {"narrative_nodes":0,"facts":0,"knowledge":0,"boundaries":0},
  "gate": {"input":"PENDING","brief":"PENDING","script":"PENDING","audit":"PENDING","lock":"PENDING"},
  "open_change_requests": [],
  "next_station": "P0"
}
```

## Stage 路由

| Stage | Read | 产物 |
|---|---|---|
| P0 恢复与输入校验 | `stages/00-resume-and-input-validation.md` | manifest/state 输入快照 |
| P1 Script Brief | `stages/01-script-brief.md` | `03_script_DRAFT.md` Header/Brief |
| P2 Scene Architecture | `stages/02-scene-architecture.md` | 场次架构 |
| P3 Scene Draft | `stages/03-scene-draft.md` | 场次正文草稿 |
| P4 Dialogue/VO/Knowledge Lock | `stages/04-dialogue-voiceover-and-knowledge-lock.md` | 台词、旁白、知识映射 |
| P5 Shootability & Boundary Audit | `stages/05-shootability-and-boundary-audit.md` | 完整 DRAFT 与审计 |
| P6 Lock & Handoff | `stages/06-lock-and-handoff.md` | `03_script_LOCKED.md` + state |

乱序请求先列未过 Gate；P0、P2 方向选择、P5、P6 不可 Skip。每站运行到 Hard Stop 后必须等用户 Next/Back/Edit。

## Module 路由

| 需要 | Read |
|---|---|
| 状态、Lock、STALE、CR、Continue | `modules/project-contract.md` |
| Truth/Narrative 只读和优先级 | `modules/truth-and-narrative-read-policy.md` |
| Script schema/provenance | `modules/script-schema-and-provenance.md` |
| 场次与动作 | `modules/scene-craft.md` |
| 台词与旁白 | `modules/dialogue-and-voiceover.md` |
| 可拍性 | `modules/shootability-policy.md` |
| 边界/反模式/局部语料 | `modules/boundary-audit-and-exemplars.md` |

## 首次上手

请提供视频项目 `project_ref`。我会通过 Adapter 先校验 Truth Lock、Narrative Plan、manifest/state；缺任一正式输入时只报告 blocker，不代替上游。开跑前可打开 `templates/用户核查清单.md`。

## 指令

| Next | 通过当前 Gate 后进入下一站 |
|---|---|
| Back | 回最近 checkpoint；不删除文件，受影响 DRAFT 标 STALE |
| Edit | 改未锁字段；LOCKED 变更走 CR |
| Skip | 仅跳明确可选字段，关键 Gate 不可跳 |
| Status | 输出 HUD 和 READY/MISSING/STALE/BLOCKED |
| Export | 列出版本化产物 |
| Continue `{project_ref}` | 通过 Adapter 恢复 |

## 续传与锁定

每站更新 `00_project_state.md` 和同一 DRAFT。P6 保留 DRAFT、另写 LOCKED；冻结后算整文件 SHA-256，只登记 manifest/state。上游变更时 Script 标 STALE；不得自行修改上游 LOCKED。

## 禁止

- 不新增/删改 Truth 事实或 Narrative 核心节点。
- 不用台词偷渡未批准事实，不把未知写成确定。
- 不把心理形容当可执行动作；不让所有角色同声同气。
- 不创建角色视觉档案、景别/机位/运镜、逐镜表、模型参数或 Seedance Prompt。
- 不直接消费原始 Reference Analysis；只读 Narrative Lock 中已批准的机制。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-script-studio`，版本只读 metadata/发行 manifest。

v0.1.1；partner `wenjing`；AFP-SPEC Silver 目标，真实用户门槛前 provisional。
