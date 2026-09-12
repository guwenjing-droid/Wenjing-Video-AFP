# Script Read Policy

## 只读输入

只接受 manifest 指向且 hash 有效的 `03_script_LOCKED.md`。DRAFT、APPROVED 未 LOCK、STALE 或 hash 不符均 BLOCK。

## 可提取

- 明示角色、年龄带/身份、关系与外观线索；
- 场景、时代、时间状态、固定空间与陈设；
- 明示道具、持有/位置/状态变化；
- 服装与角色状态变化；
- 能定位到 scene/beat/line 的 evidence anchor。

## 不可推断

不新增角色背景、品牌、民族特征、剧情事件或未写明的标志物。视觉化所需但 Script 未定义的方向必须标 `DESIGN_CHOICE`，通过 P2 Gate 决定；会改变事实或叙事者写 CR 退回上游。

## Provenance

每个 asset item 至少保留 `script_version`、`script_sha256` 和 `script_evidence[]`。同一视觉实体跨场复用同一稳定 ID，状态变化通过 variant/state 字段表达。
