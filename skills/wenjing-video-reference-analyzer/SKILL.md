---
name: wenjing-video-reference-analyzer
version: 0.1.1
description: >
  参考视频逆向分析器：对用户实际提供的 transcript、视频、帧、音频或组合材料，
  依次完成 Content Intelligence、Narrative Reverse Engineering、Engagement
  Engineering、Audiovisual Grammar 和 Transfer Engine，输出受可观察范围约束、
  有证据锚且可供原创视频生产选择采用的 Reference Analysis LOCKED Artifact。
  【触发词覆盖】：拆解这个参考视频 / 分析这个视频为什么有效 / 学习这个爆款视频 /
                参考这个视频做新的前先分析 / 提炼这个视频可迁移的机制 /
                分析参考视频的节奏和叙事 / 分析这个视频的镜头语言 /
                根据 transcript 拆解视频 / 逆向分析这个短视频 /
                生成 Reference Analysis / video reference analysis
  【触发隔离】：只负责分析、抽象和原创迁移规则，不写最终剧本、Storyboard、
              Seedance Prompt 或执行视频生成。用户要把 Truth Lock 设计成 Narrative Plan
              时由 wenjing-video-narrative-designer 响应；写正式剧本由
              wenjing-video-script-studio 响应；逐镜分镜和生成分别交给对应独立 Skill。
              “参考生视频/参考生图”若意图是直接调用生成模型，也不触发本 Skill。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-reference-analyzer

把参考视频材料逆向分析为可审计、可迁移但不可照抄的 Reference Analysis Artifact。

## 核心原则

1. 先登记实际材料，再限定可观察范围；声明不能扩大证据。
2. 观察、视频声称、分析判断、外部核验四类内容分层。
3. transcript-only 不分析实际镜头、表演、字幕、音乐、音效或转场。
4. Transfer Rule 只抽象机制，隔离专有内容和禁复制项。
5. 只生成 Reference Analysis，不代替 Narrative、Script、Storyboard 或 Producer。

## HUD

```json
{
  "project_id": "",
  "reference_id": "",
  "contract_version": "reference-analysis/0.1",
  "current_station": "P0",
  "input_modality": "UNKNOWN",
  "observed_materials": {},
  "missing_modalities": [],
  "analysis_scope": [],
  "gate": {
    "input_modality": "PENDING",
    "observability": "PENDING",
    "original_transfer": "PENDING"
  },
  "artifact": {
    "draft_path": "",
    "locked_path": "",
    "status": "MISSING",
    "sha256": ""
  },
  "continuation": {
    "manifest_path": "",
    "state_path": "",
    "open_change_requests": []
  },
  "next_station": "P0"
}
```

## 阶段路由

| 阶段 | Read | 交付 |
|---|---|---|
| P0 恢复与模态校验 | `stages/00-resume-and-modality-validation.md` | manifest/state + DRAFT Header |
| P1 Content Intelligence | `stages/01-content-intelligence.md` | DRAFT Content |
| P2 Narrative Reverse Engineering | `stages/02-narrative-reverse-engineering.md` | DRAFT Narrative |
| P3 Engagement Engineering | `stages/03-engagement-engineering.md` | DRAFT Engagement |
| P4 Audiovisual Grammar | `stages/04-audiovisual-grammar.md` | DRAFT Audiovisual / NOT_OBSERVABLE |
| P5 Transfer & Boundary Audit | `stages/05-transfer-and-boundary-audit.md` | 完整 DRAFT + Gate 结果 |
| P6 Lock & Handoff | `stages/06-lock-and-handoff.md` | 独立 LOCKED + manifest/state |

任何乱序请求先列出未通过 Gate；不得 Skip P0、P5 或 P6。每一运行阶段到确认框后必须停止，等待 Next/Back/Edit。

## 按需模块

| 需要 | Read |
|---|---|
| 项目目录、状态、LOCKED/STALE/CR | `modules/project-contract.md` |
| 模态与可观察范围 | `modules/modality-observability-policy.md` |
| 证据锚与 claim 分层 | `modules/evidence-and-claim-policy.md` |
| 受众、观点、逻辑链、论据 | `modules/content-intelligence-method.md` |
| 叙事和参与机制 | `modules/narrative-engagement-methods.md` |
| 视听语法 | `modules/audiovisual-grammar-method.md` |
| 原创迁移、局限和外部补充 | `modules/transfer-originality-and-limitations.md` |

## 首次上手

先请用户提供项目目录（或允许建立最小项目壳）、reference_id、实际材料路径和分析目标。开跑前提示用户查看 `templates/用户核查清单.md`。如果只有 transcript，立即说明完整视听分析不可用，但可继续 Content、Narrative 与部分 Engagement。

## 通用指令

| 指令 | 行为 |
|---|---|
| Next | 确认当前 Gate 后进入下一站 |
| Back | 回最近磁盘 checkpoint；受影响 DRAFT 标 STALE，不删除文件 |
| Edit | 修改未锁字段；LOCKED 变更创建 Change Request |
| Skip | 仅跳可选 External Supplements；关键 Gate 不可跳 |
| Status | 输出完整 HUD 和 READY/MISSING/STALE/BLOCKED |
| Export | 列出全部落盘产物与版本 |
| Continue `{project_ref}` | 通过 Adapter 从 manifest/state/LOCKED/CR 恢复 |

## 续传与锁定纪律

- P0 读取或建立 `00_project_manifest.yaml`、`00_project_state.md` 与 reference manifest。
- 每站更新同一 DRAFT 和 state，保留 Evidence Anchors。
- P6 保留 DRAFT，另写 LOCKED；冻结后计算 SHA-256，只登记在 manifest/state。
- LOCKED 不原地覆盖。上游材料或分析重开时，依赖状态标 STALE。
- `afp-shared-continuation` 不是 v0.1 运行依赖；本 Skill 使用 `modules/project-contract.md` 的本地兼容协议。

## Gate

- G-RA-01：材料、modality、observed/missing 和 scope 一致。
- G-RA-02：所有结论在可观察范围内且有锚；ANCHOR_LIMITED 降级置信度。
- G-RA-03：迁移规则抽象、专有元素隔离、不以换词代替原创。
- P6 是最终 Hard Gate；不自动触发 Narrative Designer。

## 禁止

- 不伪造时间码、帧号、平台留存数据或外部核验。
- 不把“视频声称”升级成事实。
- 不从 transcript 推断视听维度。
- 不复制独特表达、角色、事件顺序、段落或镜头组合。
- 不生成最终剧本、Storyboard、Seedance Prompt 或视频。

## 合规目标与版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-reference-analyzer`，版本只读 metadata/发行 manifest。

AFP-SPEC Silver 目标；真实用户门槛完成前为 provisional。v0.1.1，partner `wenjing`。
