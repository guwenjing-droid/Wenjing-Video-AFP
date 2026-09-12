# P5 · Draft 审阅

> wenjing-video-case-planner · Stage 05  
> 目的：对完整 Case Truth Lock 草稿做 schema、证据链、边界和职责自审，并提交最终人工确认。

## 一、本阶段边界

本阶段只审阅和修复 Draft，不生成 LOCKED 文件，不启动 Narrative，不写下游内容。

开始前 Read：

- `templates/case-truth-lock-template.md`
- `modules/anti-patterns.md`
- `modules/project-contract.md`

## 二、四层自审

### 1. Schema

检查模板所有必填章节、ID 唯一性、枚举值、路径、版本和状态；Draft status 必须仍为 DRAFT。

### 2. Evidence

检查核心事实 source anchor、事实/解释/推断/未知分类、措辞强度、未决问题和外部补充来源隔离。

### 3. Teaching and Boundary

检查知识点数量与事实映射、教学目标决策记录、ALLOWED/CONDITIONAL/FORBIDDEN 的可执行性和敏感风险。

### 4. Responsibility

检查是否混入最终钩子、完整剧情、正式台词、视觉设定、分镜或 Seedance 参数；发现即删除并记录越界修复。

## 三、放行等级

- `READY_FOR_APPROVAL`：必填项齐全，无阻断问题。
- `REVIEW_REQUIRED`：有非核心问题，需要用户选择或编辑。
- `BLOCKED`：核心事实无来源、教学方向未确认、关键边界未裁决或 schema 缺失。

只有 `READY_FOR_APPROVAL` 才能请求用户执行最终 Lock。不得用“基本完成”绕过阻断项。

## 四、输出 schema 与落盘

完成并保存：

`{project_path}/stage-outputs/01_case_truth_lock_DRAFT.md`

在文档末尾增加：

- Consistency Declaration
- Self-Audit Report
- Remaining Risks
- Proposed Downstream Handoff
- Approval Log（保持 PENDING）

同步 state：`current_station=P5`、`next_station=P6|P5`、`final_lock=PENDING`、review_status、blocker。

## 五、向用户展示

不要只说“已完成”。展示：

1. 核心事实与最大不确定性摘要。
2. 教学目标和知识点。
3. 最重要的允许/禁止改编项。
4. 自审等级与剩余风险。
5. Draft 绝对路径。

用户可以 `Edit <字段>=<值>`、`Back` 或确认 `Next`。`Next` 在本阶段明确表示“批准把当前 Draft 冻结为 LOCKED”。

## 六、Hard Stop

这是最终人工 HARD Gate。即使自审全部通过，也不允许自动生成 LOCKED 文件。

```text
╭─ 管理案例视频化事实规划器 · P5 完成 ─────╮
│ 🚦 自审：{READY_FOR_APPROVAL|REVIEW_REQUIRED|BLOCKED}
│ 🧾 核心事实：{core_count}
│ 🧠 知识点：{knowledge_count}
│ ⚠️ 剩余风险：{risk_count}
│ ✅ Draft：{draft_absolute_path}
│ 📍 下一步：P6 · Lock 与交接
│ 👉 Next 批准锁定 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

## 七、反模式

- 不用漂亮摘要遮住未决问题。
- 不在自审时补造缺失证据。
- 不把 REVIEW_REQUIRED 当作可自动放行。
- 不覆盖或删除 Draft 的历史决策记录。
- 不在用户批准前写 LOCKED 文件。

---

*P5 获得用户批准后，主控加载 `stages/06-lock-and-handoff.md`。*
