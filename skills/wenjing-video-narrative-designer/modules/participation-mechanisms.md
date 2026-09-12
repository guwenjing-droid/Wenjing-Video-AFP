# Module · Participation Mechanisms

> 供 P2 与 P4 按需读取。把“互动”定义为观众的认知动作，而不是无关口号。

## 1. 合格条件

Participation Mechanism 必须同时回答：

1. 观众要做什么动作？
2. 该动作发生在哪个 node？
3. 它如何服务 knowledge_id 或 teaching_goal？
4. 它是否提前泄露 Hook Payoff？
5. 它是否会诱导错误事实、泄露隐私或制造无关互动？

## 2. 机制类型

### 预测

让观众基于当前已给事实预测下一状态。适合决策—后果、悬念—发现。预测项必须在后文可验证，不能让观众猜未锁定信息。

### 选择

在真实约束中比较 A/B/C。选项必须来自案例合理空间；不能把明显错误项当假互动。

### 代入

邀请观众识别自己在相似角色/处境中的判断。只代入决策或感受，不虚构真实人物内心。

### 比较

让观众比较两个时间点、方案、指标或解释。比较维度必须一致且由 Truth Lock 支撑。

### 反思

在 Payoff 后让观众重新检查最初判断。适合教学迁移，不应变成说教式标准答案。

### 贡献案例

邀请观众提供自己的经验或反例。须说明隐私边界，不能把评论区当事实核验来源。

## 3. 节点安放

- Hook 后：可用预测，但不立即索要泛化评论。
- Choice/Tension：可用选择、比较、代入。
- Payoff 前：避免泄露答案或打断必要证据链。
- Payoff 后：适合反思、概念迁移、贡献案例。
- Ending：只保留一个与教学目标最相关的动作，不堆叠点赞/关注/评论口令。

## 4. 输出字段

```yaml
participation_id: PAR-01
type: "prediction | choice | identification | comparison | reflection | contribution"
node_id: ""
audience_action: ""
teaching_link: "knowledge_id / teaching_goal"
payoff_visibility: "hidden | partial | revealed"
safety_notes: []
transfer_rule_refs: []
```

## 5. Reference 机制迁移

Reference Analysis 可以说明某种互动为什么在原视频中形成注意力，但 Narrative Designer 只能迁移其认知功能。例如迁移“先让观众作出选择再揭示约束”，不能复制原视频的问题原句、选项、角色或结尾号召。

transcript-only Artifact 无权支持“某音乐卡点带来参与”“某表演使观众停留”等视听结论；此类 rule 必须排除。

## 6. 风险检查

- **事实风险**：观众被引导接受未证明前提。
- **隐私风险**：要求分享敏感经历、组织信息或个人身份。
- **教学风险**：互动热闹但与知识点无关。
- **节奏风险**：过早打断论证或重复索取行动。
- **操控风险**：羞辱、恐吓或制造虚假二选一。
- **原创风险**：照搬参考视频的独特互动话术和顺序。

任一高风险未修复，不得进入 P3/P5。

## 7. 反模式

- 不把“评论区扣 1”作为默认机制。
- 不制造只有一个显然正确答案的伪选择。
- 不把点赞关注当学习动作。
- 不让互动提前泄露 Payoff。
- 不复制参考视频的互动文案。
