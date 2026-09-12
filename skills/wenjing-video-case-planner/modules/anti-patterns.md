# Case Planner 反模式与防御

> P5 自审和 P9 测试失败分析时加载。

## A1 · 摘要冒充事实锁

**症状**：输出一段流畅摘要，却没有 fact_id、source anchor 和分类。  
**防御**：核心信息必须进入可逐条核对的 Fact Table。

## A2 · 作者观点客观化

**症状**：把“管理层认为”“研究者解释”为无主体事实。  
**防御**：标 INTERPRETATION 并保留解释主体。

## A3 · 为冲突补造因果

**症状**：为了故事更精彩，加入原材料不存在的动机、对话、阻碍或结果。  
**防御**：所有关键因果必须有 anchor；没有就标 INFERENCE/UNKNOWN，并进入禁止虚构清单。

## A4 · SCQA 反客为主

**症状**：先套“冲突—答案”，再选择性改写事实适配结构。  
**防御**：先完成 Truth Audit；SCQA 只能在事实锁之后作为初步路线建议。

## A5 · 知识点贪多

**症状**：一条案例塞入多个理论，教学目标不可评价。  
**防御**：限定 1–3 个，逐一映射 fact_id 与可观察学习结果。

## A6 · 未决问题被润色消失

**症状**：最终文档看起来完整，但材料矛盾和缺口不见了。  
**防御**：Unknowns/Unresolved Issues 为必填章节；用户裁决必须有 decision log。

## A7 · 边界口号化

**症状**：只写“忠于原文、不要乱编”。  
**防御**：按 ALLOWED/CONDITIONAL/FORBIDDEN 列具体动作并关联 fact_id。

## A8 · 越界生产

**症状**：Case Planner 顺手输出钩子、剧情、台词、角色造型或分镜。  
**防御**：P5 Responsibility Audit；越界内容删除并留修复记录。

## A9 · 外部知识静默混入

**症状**：模型常识或网络信息没有新 source_id 就进入事实表。  
**防御**：加载外部核验边界；外部信息单独登记，失败标 UNVERIFIED。

## A10 · 对话宣布锁定

**症状**：回复“已锁定”，但磁盘没有 LOCKED 文件、hash 或批准记录。  
**防御**：只有 Artifact Contract 四项均通过才算 LOCKED。

## A11 · 原地修改 LOCKED

**症状**：下游发现问题后直接改上游正式文件。  
**防御**：创建 Change Request、传播 STALE、升版本并重新过 HARD Gate。

## A12 · 恢复时从头再问

**症状**：已有 state/产物仍要求用户重述项目。  
**防御**：P0 先扫描，显示资产清单，只询问 MISSING/BLOCKED 项。

## P5 自审清单

- [ ] 核心事实均有 STRONG anchor。
- [ ] FACT / INTERPRETATION / INFERENCE / UNKNOWN 未混写。
- [ ] 1–3 个知识点均映射事实。
- [ ] 教学目标已有用户决策记录。
- [ ] ALLOWED/CONDITIONAL/FORBIDDEN 可执行。
- [ ] 未混入下游业务内容。
- [ ] Draft 已落盘，status 仍为 DRAFT/APPROVED。
- [ ] state 与 Draft 路径、版本、当前 Gate 一致。
