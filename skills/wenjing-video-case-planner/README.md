# wenjing-video-case-planner

管理学、经济学和教学案例的视频生产前置规划器。它把原始材料整理为可审计的 Case Truth Lock，让后续叙事和剧本创作知道哪些是事实、哪些是解释、哪些可以戏剧化、哪些绝不能改。

## 能做什么

- 建立来源清单和逐条 source anchor。
- 区分 FACT、INTERPRETATION、INFERENCE、UNKNOWN。
- 提炼 1–3 个知识点并锁定教学目标。
- 定义 ALLOWED、CONDITIONAL、FORBIDDEN 改编边界。
- 生成 Draft，经人工 HARD Gate 后生成 LOCKED 正式继承物。
- 从 `00_project_state.md` 跨对话恢复。

## 不做什么

不写最终钩子、情绪曲线、正式剧本、视觉资产、分镜、Seedance Prompt，也不生成视频。开放式事实调查应交给专门研究/核验流程。

## 精确触发示例

- “解析这个管理案例的视频化方向。”
- “锁定这个案例的事实与教学目标。”
- “生成案例 Truth Lock。”
- “审查这个案例哪些内容可以戏剧化。”

“帮我完整做一条视频”“把案例画成漫画”“写正式剧本”“做 Seedance 分镜”等口令不属于本 Skill。

## 两种入口

### 从零开始

提供案例文件或原文、目标受众和课程目标。Skill 会先建立项目 manifest/state，再逐阶段推进。

### 断点恢复

```text
Continue {project_ref}
```

Skill 先扫描磁盘并展示资产状态；不会重问已经确认的内容。

## 核心产物

```text
stage-outputs/01_case_truth_lock_DRAFT.md
stage-outputs/01_case_truth_lock_LOCKED.md
```

只有 LOCKED 文件可交给 `wenjing-video-narrative-designer`。任何修改必须通过 `change-requests/CR-{id}.md`。

## 用户监督

开跑前查看 `templates/用户核查清单.md`。每阶段确认落盘文件和判断标准，再输入 `Next`。

## 包结构

- `SKILL.md`：薄路由与 HUD。
- `stages/`：P0–P6 时序流程。
- `modules/`：项目契约、证据分类、锚点、外部核验边界和反模式。
- `templates/`：Truth Lock、manifest、state、Change Request 和用户核查清单。
- `tests/`：P9 创建测试 Fixture 与期望结果。

## 方法来源

方法机制提炼自用户历史资产 `漫画化.txt`、`生视频.txt` 前半段，并按《编排方案_视频生产.md》重构为事实锁、证据链、HARD Gate、锁与变更协议。历史 Prompt 没有被原样复制进包。

## 版本

- v0.1.0：首件施工版，AFP-SPEC Silver 目标；P9 工程契约测试 22/22 通过，Silver 真实用户与运行时测试待补。
