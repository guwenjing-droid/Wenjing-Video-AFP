# Module · Anti-patterns

> 供 P5 按需读取，也可在 Back/Edit/Review 时定位返工原因。每条都包含检测信号与修复动作。

## 1. 事实与证据

### AP-01 为戏剧性编事实

- 信号：新增人物、冲突、数字、因果或结局没有 fact_id/boundary。
- 修复：删除；若确需补充，创建 Case Planner CR。

### AP-02 强化不确定性

- 信号：上游“可能/相关”在 Draft 变成“确定/导致”。
- 修复：恢复限定词，降低 Hook/Payoff 强度。

### AP-03 用 Reference 替代 Truth Lock

- 信号：当前案例节点只引用 transfer_rule，没有 fact/knowledge anchor。
- 修复：先建立本项目锚；无法建立则淘汰该规则。

## 2. Hook 与结构

### AP-04 空头 Hook

- 信号：Hook 没有 Payoff Node，或 Payoff 不能兑现承诺。
- 修复：缩小 Promise 或重排有效 Payoff。

### AP-05 固定爆款公式

- 信号：不看案例气质就强制前三秒、60 秒、三段式、大反转。
- 修复：回到 Teaching Goal、事实强度和目标时长重新比较策略。

### AP-06 伪方案

- 信号：A/B/C 只换名称或语气，功能结构相同。
- 修复：只保留实质不同的 2–3 个；没有差异时不凑数。

### AP-07 节点越界成剧本/分镜

- 信号：出现逐字台词、场次、镜头编号、机位、运镜或模型参数。
- 修复：改写为 narrative function 与 downstream writing task。

## 3. 情绪、知识与参与

### AP-08 任意情绪数字

- 信号：强度没有 node 和 change_trigger。
- 修复：绑定事实/认知变化；无法解释则删除数字。

### AP-09 强造高潮

- 信号：低刺激案例被写成 10/10 冲突或虚构反派。
- 修复：改用共鸣、观察、治愈或小幅重估路线。

### AP-10 知识点讲义插播

- 信号：知识解释与 node/fact 无关，只是理论段落。
- 修复：把知识映射为问题、比较、选择、后果、发现或反思。

### AP-11 无关互动诱饵

- 信号：评论/点赞动作不改变理解，也不服务教学。
- 修复：换成预测、选择、比较、代入或反思；无必要则删除。

## 4. Reference Analysis 专项

### AP-12 Transcript 视听幻觉

- 信号：只有 transcript，却评价景别、构图、运镜、表演、字幕、音乐、音效、转场、色彩或光影。
- 修复：该维度标 `NOT_OBSERVABLE`，移除相关 transfer rule。

### AP-13 把外部补充当视频内容

- 信号：行业玩家、政策、趋势没有视频锚，却被写成“原视频指出”。
- 修复：移到 External Supplements 并核验；Narrative 不自动继承。

### AP-14 换词式复制

- 信号：保留原视频独特角色、事件顺序、段落结构和转折，仅替换词语或主题名。
- 修复：回到抽象机制，重新从本项目 Truth Lock 构造节点。

### AP-15 Source-specific 越权

- 信号：采用 `source_specific_elements` 或 `do_not_copy` 中的内容。
- 修复：立即 BLOCK 并删除；不能通过用户偏好绕过原创底线。

### AP-16 参考成功即本项目成功

- 信号：把原视频播放量、名气或“爆款”标签当成本项目传播保证。
- 修复：只记录机制适配度与风险，不承诺结果。

## 5. Gate、状态与落盘

### AP-17 DRAFT 冒充 LOCKED

- 信号：下游读取 DRAFT，或无批准记录即生成 LOCKED。
- 修复：回到 P5 Gate，保留 Draft，批准后另生成 LOCKED。

### AP-18 可选输入错误阻断

- 信号：Reference 未提供便阻断 CASE Narrative。
- 修复：写 `NOT_PROVIDED/N/A` 并继续；只有 REQUIRED_BUT_INVALID 才阻断。

### AP-19 REQUIRED 被静默降级

- 信号：用户明确要求参考分析，但 Artifact 无效仍忽略后继续。
- 修复：标 REQUIRED_BUT_INVALID，回用户 Review。

### AP-20 STALE 后继续生产

- 信号：上游或实际采用 Reference 已升版，Narrative 仍标 READY。
- 修复：按依赖关系标 STALE，回最早受影响阶段重审。

### AP-21 完整性自引用

- 信号：把 LOCKED 文件的整文件 SHA-256 写回文件本体后反复变化。
- 修复：完整性值只登记 manifest/state，不回写本体。

### AP-22 只在对话交付

- 信号：方案已展示但 Draft/state 没有落盘。
- 修复：写入具名文件，回报绝对路径，再 Hard Stop。

## 6. 快速拦截顺序

先查 AP-01/02/03/12/14/15/17/20；这些命中即 BLOCK。再查 Hook、教学、参与与格式项。不得用“整体质量不错”抵消单项硬违规。
