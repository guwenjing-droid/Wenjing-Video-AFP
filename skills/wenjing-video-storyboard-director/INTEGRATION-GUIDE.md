# Integration Guide · wenjing-video-storyboard-director

## 生态位置

- Pattern 5 Independent；partner `wenjing`。
- 上游：Script Studio；条件性 Visual Bible。
- 下游：Continuity Reviewer 的 PREFLIGHT。

## 输入

必需：manifest/state + path/version/hash 有效的 `03_script_LOCKED.md`。条件输入：manifest 选中或要求时，`04_visual_bible/asset_manifest_LOCKED.yaml` 与当前 shots 使用的 READY 文件。

## 输出

`05_storyboard_DRAFT.json`、`05_storyboard_audit.md`、`05_storyboard_LOCKED.json`。LOCKED 需 audit GREEN，Script/Dialogue/knowledge coverage 完整，资产引用可验证，且不含模型专属字段。

## 状态影响

只写 storyboard 本站、输入 refs、affected shots/sequences、锁定 hash 与 `next_station=wenjing-video-continuity-reviewer:PREFLIGHT`。

## 错误处理

输入失效或冻结接口冲突则 BLOCK/CR；单 shot 失败局部重跑；Visual Bible 可选但未选择时显式 TEXT_ONLY，若连续性风险要求资产则 BLOCK，不静默降级。

契约版本 v0.1.0；继承编排 v0.4。
