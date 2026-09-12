---
name: wenjing-video-visual-bible
version: 0.1.2
description: >
  管理学、经济学或教学案例视频的视觉资产执行件：读取已锁定 Script 与项目约束，
  盘点角色、场景、道具和服装状态，建立可追溯的身份锚、多视图参考规范、实际资产
  readiness 与锁定清单，供 Storyboard 继承；在项目采用 V0_1_DRY_RUN 时，可输出
  明确标注为规格级就绪、真实媒体延期的 Visual Bible，不把规格冒充图片。
  【触发词覆盖】：根据已锁剧本建立视频视觉圣经 / 为正式案例视频做角色场景道具设定 /
                建立角色一致性参考图和身份锚 / 生成 04_visual_bible 资产清单 /
                检查视频角色场景道具资产是否 READY / 继续 Visual Bible /
                把 Script Lock 接成 Storyboard 可用的视觉资产
  【触发隔离】：只处理已有 Script LOCKED 的角色、场景、道具、服装状态、视觉风格和
              canonical reference 资产。没有锁定剧本时不代写剧本；不写逐镜 Storyboard、
              景别运镜、Seedance 视频 Prompt，不调用视频生成。用户只要单张通用图片、
              小说人物提炼或知识漫画时不触发。未生成或未通过存在性/hash/一致性检查的
              资产不得标为 READY 或交给下游。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-visual-bible

把锁定剧本中的视觉实体变成可定位、可复用、可审计的角色/场景/道具资产包。

## 原则

1. Script LOCKED 只读；角色事实、关系、时代和场景不得擅改。
2. 规范与实际文件分层；只有文件存在、完整性校验码有效且检查通过才是实际 `READY`。Dry Run 规格只可标 `dry_run_readiness=READY`。
3. 先复用兼容的 LOCKED/READY 资产，再补缺；不为跑完整流程重复生成。
4. 真实生图只在工具可用且外部调用/成本已授权时执行；`V0_1_DRY_RUN` 保留完整规格并允许规格级接棒，但不获得实际 `READY`。
5. 只负责资产，不写 Storyboard、视频 Prompt 或调用视频生成。

## HUD

```json
{
  "project_id": "",
  "acceptance_profile":"REAL_MEDIA|V0_1_DRY_RUN",
  "current_station": "P0",
  "script_lock": {"status":"MISSING","path":"","version":"","sha256":""},
  "visual_bible": {"status":"MISSING","draft_path":"stage-outputs/04_visual_bible/asset_manifest_DRAFT.yaml","locked_path":"stage-outputs/04_visual_bible/asset_manifest_LOCKED.yaml","sha256":""},
  "assets": {"required":0,"real_ready":0,"dry_run_ready":0,"reused":0,"missing":0,"stale":0,"blocked":0},
  "reuse_decisions": [],
  "rerun_scope": {"from_checkpoint":"","affected_artifacts":[],"unaffected_locked_artifacts":[]},
  "gate": {"input":"PENDING","inventory":"PENDING","direction":"PENDING","characters":"PENDING","scene_props":"PENDING","audit":"PENDING","lock":"PENDING"},
  "open_change_requests": [],
  "next_station": "P0"
}
```

## Stage 路由

| Stage | Read | 产物 |
|---|---|---|
| P0 恢复与输入校验 | `stages/00-resume-and-input-validation.md` | state 输入快照 |
| P1 资产盘点 | `stages/01-asset-inventory.md` | asset manifest DRAFT |
| P2 风格与身份锚 | `stages/02-style-and-identity-anchors.md` | style/identity specs |
| P3 角色参考集 | `stages/03-character-reference-sets.md` | character sheets/files |
| P4 场景与道具参考集 | `stages/04-scene-and-prop-reference-sets.md` | scene/prop sheets/files |
| P5 Readiness 与边界审计 | `stages/05-readiness-and-boundary-audit.md` | REAL_GREEN / DRY_RUN_GREEN / YELLOW / RED report |
| P6 Lock 与接棒 | `stages/06-lock-and-handoff.md` | asset manifest LOCKED + state |

乱序请求先列未过 Gate。P0、P1、P2、P5、P6 不可 Skip；同一阶段的低风险填充和校验按项目 control mode 自动连续，方向、真实高成本生成和 LOCK 仍按 Gate 停止。

## Module 路由

| 需要 | Read |
|---|---|
| 项目壳、状态、Lock、CR、Continue、局部恢复 | `modules/project-contract.md` |
| Script 只读、事实与边界提取 | `modules/script-read-policy.md` |
| 资产 ID、类型、依赖与服装状态 | `modules/asset-taxonomy.md` |
| 全局风格、身份锚和复用兼容性 | `modules/identity-consistency.md` |
| 角色多视图与表情/动作参考 | `modules/character-reference-method.md` |
| 场景空间关系与道具参考 | `modules/scene-and-prop-method.md` |
| readiness、存在性、hash、职责与接棒 | `modules/readiness-and-boundary-audit.md` |

只加载当前 Stage 命中的 module 和必需依赖 Artifact；禁止默认遍历历史素材库。

## 首次上手

请提供视频项目 `project_ref`。我会通过 Adapter 先校验 manifest/state 与 `03_script_LOCKED.md`，再只读取当前任务需要的角色、场景、道具和已选参考资产。开跑前可打开 `templates/用户核查清单.md`。

## 指令

| 指令 | 作用 |
|---|---|
| Next | 通过当前 Gate 后进入下一站 |
| Back | 回最近合法 checkpoint；只把受影响后代标 STALE |
| Edit | 改未锁规格；LOCKED 变更走 CR |
| Skip | 仅跳明确可选资产，关键 Gate 不可跳 |
| Status | 输出 HUD 与 READY/MISSING/STALE/BLOCKED |
| Export | 列出版本化产物与 hash |
| Continue `{project_ref}` | 通过 Adapter 按需恢复 |

## 续传与锁定

每站只更新 `00_project_state.md` 中本件字段和 `04_visual_bible` 产物。恢复时从最近合法检查点开始；有效 LOCKED/READY 资产不重算。P6 保留 DRAFT，另写 LOCKED 并登记整文件 SHA-256。上游 Script 变化时只标记受影响资产及其后代 STALE。

## 禁止

- 不修改 Script LOCKED，不补写剧情事实、台词或人物关系。
- 不把规格文本、外部链接、Mock 文件或生成任务 ID 冒充实际资产文件。
- 不承诺“100% 一致”；用身份锚、视图覆盖和审计降低漂移。
- 不写逐镜机位/运镜/时长，不写 Seedance Prompt，不调用视频生成。
- 不复用无权利依据、无 hash、版本不兼容或已 STALE 的资产。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-visual-bible`，版本只读 metadata/发行 manifest。

v0.1.2；partner `wenjing`；AFP-SPEC Silver 目标，真实用户门槛前 provisional。
