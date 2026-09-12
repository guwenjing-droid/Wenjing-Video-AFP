# Module · Truth Lock Read Policy

> 供 P0–P6 读取。规定 Narrative Designer 如何只读继承 Case Truth Lock，并处理与 Reference Analysis 的优先级。

## 1. 唯一事实权威

`stage-outputs/01_case_truth_lock_LOCKED.md` 是本件唯一上游事实权威。Narrative Designer 不重新调查、补写或强化案例事实。

Reference Analysis 只能提供叙事与参与机制建议，不能成为本项目事实来源。优先级固定为：

```text
Case Truth Lock > 用户/项目约束 > Reference Analysis
```

## 2. P0 完整性检查

只有以下条件全部满足，Truth Lock 才为 READY：

1. 文件存在，正文状态为 LOCKED。
2. path、version、sha256 与 manifest/state 一致。
3. 文件未被标 STALE。
4. 没有影响 FACT、Knowledge、Teaching Goal 或 Boundary 的开放阻断 CR。
5. 下列区域可解析：FACT、Core Knowledge Points、Teaching Goal、Audience、ALLOWED、CONDITIONAL、FORBIDDEN。

任何一项失败都阻断 Narrative P1；不得用 Reference Analysis、网络常识或模型记忆补洞。

## 3. 允许读取的对象

| 上游对象 | Narrative 用法 | 禁止动作 |
|---|---|---|
| fact_id | 绑定 hook、node、payoff、emotion trigger | 改数字、主体、时序、因果或限定词 |
| knowledge_id | 绑定教学动作与知识植入 | 新增未锁理论或把解释升级成事实 |
| teaching_goal | 定义叙事终点 | 为传播性改换教学目标 |
| audience | 校准解释深度与参与方式 | 以刻板印象虚构需求 |
| ALLOWED | 在许可范围内抽象化/压缩 | 把许可理解成任意改编 |
| CONDITIONAL | 仅在 decision_id 已批准时采用 | 模型自行裁决 |
| FORBIDDEN | 全流程排除 | 用“戏剧化”绕过 |

## 4. 事实锚定规则

- Hook Promise 至少绑定一个 fact_id 或 knowledge_id，并写 required payoff。
- 核心 Narrative Node 必须绑定 fact/knowledge/approved boundary。
- 数据、时间、人物关系、结果、归因和引语保留上游限定词。
- 数据类内容同时保留上游 source/source_id、数据期间或发布日期；缺少来源或时间时不得写成当前有效事实。
- “可能、据称、相关、同期发生”不得被强化为“确定、证明、导致”。
- 没有锚的主事件不能进入 Draft；缺少材料时登记 gap 或 CR。

### 无法验证的内容

- 不在 Truth Lock、已批准 Boundary 或有效 Reference Evidence 中的事实性主张一律标记 `unverified`。
- `unverified` 只能进入 Pending/Issue/External Supplement 记录，不得进入 LOCKED Narrative 的 promise、node、payoff 或知识结论。
- 外部补充若缺来源、发布日期/数据期间或 verification status，保持 `unverified`，不得伪装成原视频或当前案例事实。

## 5. Reference 冲突处理

当 transfer rule 与本项目冲突时：

1. 与 Truth Lock 冲突：淘汰规则，记录 `truth_lock_check=FAIL`。
2. 与用户/项目约束冲突：淘汰或回用户 Review，记录 `project_constraint_check=FAIL`。
3. 只与设计偏好不同：可作为备选，但不得自动替用户选择。
4. 规则依赖未观察的视听维度：淘汰，记录 observability failure。
5. 规则包含来源专有内容或 do-not-copy：不得采用；不能靠同义改写规避。

Reference 中出现的新事实、行业玩家、政策或数据不得自动进入 Case Truth Lock；若用户确需纳入，应创建 CR 回到 Case Planner 核验。

## 6. 按阶段复核

- P0：完整性、STALE、CR、schema。
- P1：Brief 中所有继承字段与上游逐 ID 一致。
- P2：每个 Hook/Participation 的事实和知识锚。
- P3：每个核心节点、转折与 Payoff 的依据。
- P4：情绪变化、学习动作与参与机制的事实触发。
- P5：逐项全量审计，并复核 Reference 采用不越权。
- P6：冻结前再次复算输入完整性；任何变化立即 BLOCK。

## 7. 失败处理

- 缺字段：P0 BLOCKED，指出 exact section/ID。
- 条件未裁决：留在当前阶段，创建 decision request。
- 需要改事实：创建上游 Change Request，不在 Narrative 内修。
- 上游已变更：标记 Narrative 及依赖物 STALE，回到最早受影响阶段。

## 8. 禁止项

- 不引用 Reference Analysis 替代 fact_id。
- 不把参考视频的论点当成当前案例结论。
- 不用戏剧效果作为事实成立的理由。
- 不静默删除上游的不确定性或限制条件。
- 不在 P6 锁定时顺手改写事实。
