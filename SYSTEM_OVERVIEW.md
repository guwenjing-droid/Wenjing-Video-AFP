# System Overview

## 设计原则

本系统以文件 Artifact 作为跨 Skill 接口。每个 Independent Skill 只拥有一个清晰职责；Orchestrator 不代写业务输出。运行时采用最短合法路径、按需加载、分级 Gate、资产复用、局部重跑和成本感知路由。

## Skill 清单

| Skill | 类型 | 版本 | 核心职责 |
|---|---|---:|---|
| `wenjing-video-orchestrator` | Orchestrator | 0.2.1 | 路由、依赖检测、接棒检查、状态与恢复 |
| `wenjing-video-case-planner` | Independent | 0.1.1 | CASE 事实锁、教学目标、知识点与原子完整性登记 |
| `wenjing-video-reference-analyzer` | Independent | 0.1.1 | 参考材料逆向分析与原创迁移规则 |
| `wenjing-video-narrative-designer` | Independent | 0.1.1 | CASE Narrative Plan、钩子、节点和输入完整性 Gate |
| `wenjing-video-script-studio` | Independent | 0.1.1 | CASE 正式锁定剧本 |
| `wenjing-video-source-locked-adapter` | Independent | 0.1.1 | SOURCE_LOCKED 忠实改编并输出兼容剧本 |
| `wenjing-video-knowledge-pov` | Independent | 0.1.1 | KNOWLEDGE 真值边界、表达方案与兼容剧本 |
| `wenjing-video-story-studio` | Independent | 0.1.1 | STORY 人物、冲突、剧情结构与兼容剧本 |
| `wenjing-video-visual-bible` | Independent | 0.1.2 | 角色、场景、道具、服装与视觉锚点 |
| `wenjing-video-storyboard-director` | Independent | 0.1.3 | 动态创作时长、required asset closure 与 canonical refs |
| `wenjing-video-continuity-reviewer` | Independent | 0.1.3 | 统一完整性口径、版本化报告与独立生成门禁 |
| `wenjing-video-seedance-producer` | Independent | 0.1.3 | Seedance Prompt、后端时长映射、参数与 generation plan |

## 路由

| 路线 | 必需入口 | 可选参考分支 | 统一下游 |
|---|---|---|---|
| CASE | case-planner -> narrative-designer -> script-studio | reference-analyzer -> narrative-designer | Visual Bible -> Storyboard -> Reviewer -> Producer |
| SOURCE_LOCKED | source-locked-adapter | reference-analyzer -> source-locked-adapter | 同上 |
| KNOWLEDGE | knowledge-pov | reference-analyzer -> knowledge-pov | 同上 |
| STORY | story-studio | reference-analyzer -> story-studio | 同上 |

Reference Analysis 的优先级低于来源真值和用户/项目约束。只有 transcript 时只能分析文本可观察维度；镜头、运镜、表演、字幕、音乐与音效必须标为 `NOT_OBSERVABLE`。

## Artifact 链

```text
00_project_manifest.yaml + 00_project_state.md
  optional Reference Analysis LOCKED
  route truth/plan artifacts
  03_script_LOCKED.md
  04_visual_bible_LOCKED.md (按项目需要)
  05_storyboard_LOCKED.json
  06_qa/preflight_report_v{n}.md
  07_generation_manifest.json / prompt package
  08_postgen_report.md
```

路径名可由平台适配，但 Artifact 身份、版本、状态、content_ref、storage backend、完整性状态、依赖和 Gate 语义不得丢失。Local File 与 Document/Board 的差异见 `runtime/`。

### 时长分层

Storyboard 记录逐镜 `estimated_duration`、`creative_required_duration`、`duration_basis` 和 `duration_driver`，不绑定模型时长档。Reviewer 拦截异常等长、对白/动作不足和简单镜头冗长。Producer 从当前 capability profile 选择不短于创作需求的最小合法档并记录裁切；无足够档位返回 `SPLIT_REQUIRED`。

## 能力边界

v1.1 完成的是逻辑生产线、Portable Runtime 和 Dry Run。当前正式媒体后端适配器是 Seedance Producer；Kling、Veo 等仍未开发。真实媒体排队、配额与实际画面一致性属于首次真实生产验证范围。
