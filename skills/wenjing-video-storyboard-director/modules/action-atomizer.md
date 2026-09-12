# Action Atomizer

## 原子格式

`actor + observable verb + object + direction/spatial relation + start_state + end_state + completion_cue`。

复杂动作拆为：准备/启动 → 位移或操作 → 接触/变化 → 结果/反应。每 atom 只保留一个主动作；并发动作显式 `simultaneous_with`，因果动作显式 `precedes/follows`。

禁用不可观察心理词作为动作，如“意识到、感到震惊”；应绑定 Script 允许的可见行为或标 `PERFORMANCE_CHOICE_REVIEW`。动作物理上不可能、时间不足或主体不明时不得硬编，返回 REVIEW/BLOCK。

局部重跑单位优先 `atom_id`，其次 shot；只有 identity/space 等公共依赖变化才扩大范围。
