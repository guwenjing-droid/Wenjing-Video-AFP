# P0 · 恢复与输入体检

> wenjing-video-case-planner · Stage 00  
> 目的：定位项目、恢复磁盘状态并确认本件所需输入，不重复询问已锁定信息。

## 一、本阶段边界

本阶段只完成项目恢复、最小项目壳和输入清单，不分析案例事实，不提炼知识点，不提出叙事方案。

启动时先 Read `modules/project-contract.md`。磁盘状态优先于对话记忆。

## 二、入口判断

### A. Continue 入口

用户提供 `Continue {项目绝对路径}` 时：

1. 解析并回显规范化绝对路径；禁止把历史资产库根目录当作运行项目目录。
2. 读取 `00_project_manifest.yaml`、`00_project_state.md`、`change-requests/` 和 `stage-outputs/`。
3. 校验 state 中登记的 LOCKED 文件是否存在；如有 hash，核对是否一致。
4. 输出资产清单：`READY / MISSING / STALE / BLOCKED`。
5. 定位 `current_station`、`next_station`、未决 HARD Gate 和开放 Change Request。
6. 已确认字段不得重问；发现文件与 state 冲突时停止并请用户裁决。

### B. Direct Use 入口

没有项目目录时：

1. 收集案例材料或文件绝对路径、项目名称、目标受众、课程/教学目标（可标待讨论）。
2. 建议项目 slug，只能使用字母、数字和连字符；展示建议路径，等待用户确认。
3. 创建最小目录结构，并以 templates 中的最小 schema 写入 manifest/state。
4. 原始材料只登记，不改写、不移动、不覆盖。

### C. Orchestrator Handoff 入口

若已有 manifest/state 且 `next_station=wenjing-video-case-planner`，按 Continue 入口执行；不得要求总控重复传递对话摘要。

## 三、输入体检

检查并分类：

- 必需：至少一份案例/论文/概念材料，或用户直接粘贴的可落盘原文。
- 必需：目标受众；不知道时标记 `PENDING_USER_DECISION`。
- 可延后到 P3：精确教学目标。
- 可选：目标时长、发布平台、既有课程结构。
- 禁止：只给标题却要求系统凭空还原真实案例。

对缺失输入只问当前阶段必要的最小问题。不得因材料长就要求用户重新上传已经存在于指定路径的文件。

## 四、输出 schema 与落盘

写入或更新：

- `{project_path}/00_project_manifest.yaml`
- `{project_path}/00_project_state.md`

state 至少更新：`current_station=P0`、`next_station=P1`、输入材料路径、READY/MISSING 列表、当前 blocker、时间戳。

禁止在本阶段创建 `01_case_truth_lock_DRAFT.md` 的事实内容。

## 五、Hard Stop

输出项目路径、读取到的资产、缺失项和下一站，等待用户确认。即使输入看起来完整，也不允许自动进入 P1。

```text
╭─ 管理案例视频化事实规划器 · P0 完成 ─────╮
│ 📊 项目：{project_id}
│ 📁 路径：{project_absolute_path}
│ 📚 输入：READY {n} / MISSING {n}
│ 💾 状态：已写入 00_project_state.md
│ 📍 下一步：P1 · 来源登记与事实抽取
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 六、反模式

- 不先问问题再扫描磁盘。
- 不把历史资产库作为项目输出目录。
- 不重问 manifest/state 已记录的决定。
- 不在路径未确认时创建宽泛目录。
- 不把“文件存在”误判为“内容已审核”。

---

*P0 完成后，主控加载 `stages/01-source-and-fact-extraction.md`。*
