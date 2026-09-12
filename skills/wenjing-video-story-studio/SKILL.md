---
name: wenjing-video-story-studio
version: 0.1.1
description: >
  STORY 视频入口：把原创故事、剧情或单集短剧意图，先锁定人物欲望、冲突、世界边界
  与创作开放区，再设计钩子、升级、转折、回报和结尾，输出兼容通用下游的
  03_script_LOCKED.md。【触发词覆盖】：原创一个故事视频 / 写单集短剧剧本 /
  做剧情短视频 / 从零设计故事和对白 / story studio / 生成 STORY Script。
  【触发隔离】：已有文章小说案例原剧本的忠实改编交给
  wenjing-video-source-locked-adapter；纯知识讲解交给 wenjing-video-knowledge-pov；
  管理/经济案例交给既有 CASE 线；系列世界观和多集资产管理尚未施工；逐镜、视觉资产、
  模型 Prompt 与媒体生成由通用下游处理。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# wenjing-video-story-studio

为原创单视频/单集故事建立清晰创作边界，再写成可拍 Script。

## 原则

1. 先区分 CONFIRMED、CREATIVE_OPEN、PROHIBITED；不得把开放创作伪装为用户事实。
2. Hook、Setup、Escalation、Turning Point、Payoff、Ending 服务同一人物欲望与因果链。
3. 动作可观察、对白可表演；不以旁白替代关键戏剧行动。
4. Reference 可选，优先级 `用户/故事 Canon 约束 > Reference Analysis`；只迁移机制，禁止复制人物、世界观、台词、独特情节或镜头表达。
5. 本版只负责原创单集。已有来源要忠实改编时转 SOURCE_LOCKED；多集连续性/长期 IP 资产转 NOT_IMPLEMENTED。
6. 只到 Script，不写逐镜、运镜、字幕、音乐、音效、模型 Prompt 或生成参数。

## HUD

```json
{"content_route":"STORY","current_station":"P0","story_brief":"MISSING","story_plan":"MISSING","script":"MISSING","scope":"SINGLE_EPISODE","reference_analysis":"NOT_PROVIDED","continuity":{"canon_items":0,"open_breaks":0},"gate":"PENDING","next_station":"P0"}
```

## Stage 路由

| Stage | Read | 结果 |
|---|---|---|
| P0 | `stages/00-resume-scope-and-routing.md` | 输入/分流快照 |
| P1 | `stages/01-story-brief-and-canon-lock.md` | Story Brief Lock |
| P2 | `stages/02-story-plan.md` | Story Plan Lock |
| P3 | `stages/03-script-draft.md` | Script DRAFT |
| P4 | `stages/04-character-plot-dialogue-lock.md` | 连续性覆盖 |
| P5 | `stages/05-originality-and-shootability-audit.md` | 审计决定 |
| P6 | `stages/06-lock-and-handoff.md` | Script LOCKED |

模块按需读取：`project-contract.md`、`story-craft-and-canon.md`、`reference-input-policy.md`、`script-output-contract.md`。

## 指令与运行

`Next / Back / Edit / Skip / Status / Export / Continue {project_ref}`。Skip 只适用于可选 Reference/非关键装饰；Canon、方向和 Script Gate 不可跳。FAST 可少停，GUIDED/STRICT 提高确认；只读必要依赖，局部失败局部重跑。v0.1 仅 DRY_RUN/MOCK。

## 版本

Artifact 使用 `content_ref + storage_backend` 由 Runtime Adapter 解析；不要求绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。Canonical id 为 `wenjing-video-story-studio`，版本只读 metadata/发行 manifest。

v0.1.1；AFP-SPEC Silver 目标，本地证据 provisional。
