# Integration Guide · wenjing-video-visual-bible

## 生态位置

- 类型：Pattern 5 Independent Skill
- partner / namespace：`wenjing`
- 上游：`wenjing-video-script-studio`
- 下游：`wenjing-video-storyboard-director`
- 核心路径：`CASE → Narrative → Script → Visual Bible → Storyboard`
- 条件性：FAST 且无身份/场景连续性需求时可由路由跳过；一旦 manifest 要求 Visual Bible，下游只消费 READY/LOCKED 项。

## 输入契约

必需：manifest/state + `stage-outputs/03_script_LOCKED.md`（路径、版本、hash、LOCKED 均有效）。可选：manifest 明确选择且权利状态可审计的 style/identity/scene/prop assets。

## 输出契约

`stage-outputs/04_visual_bible/asset_manifest_LOCKED.yaml` 及其中列出的实际 READY 文件。DRAFT、规格文本、任务 ID、外部 URL 或未审查生成物不能充当 READY 资产。

## 状态影响

只写 `visual_bible` 本站、锁定产物、复用决策、最小重跑范围与 next_station。Script 改版时传播到相关资产 STALE，不改其他站内容。

## 错误处理

- Script/Hash/权利失败：BLOCK，回上游或走 CR。
- 单资产失败：从该 asset checkpoint 局部重跑。
- 工具或成本未授权：保留 spec，状态 `SPEC_READY_ASSET_MISSING`，不冒充 READY。
- 冻结接口冲突：停线并提交 Change Request。

契约版本：v0.1.0；编排继承：v0.4。
