# Character Reference Method

## 最小充分参考集

- 核心角色：正面、侧面、背面；只有下游确需时增加 3/4 角、表情或动作参考。
- 次要角色：按 Script 可见角度和连续性风险裁剪，不机械生成全套。
- 同一 sheet 使用同一身份锚、比例、服装状态与背景基准；视图标签必须明确。

## 角色 sheet spec

包含 `character_id`、identity invariant、wardrobe/state variants、required views、expression/action references、style link、negative constraints、source/provenance、file map、readiness。

## 生成与审查

有合法工具与成本授权才提交真实生成；记录 provider/model/recipe/version/task_id 仅用于审计，不能代替输出文件。生成后检查脸型/体型/标志特征、服装状态、视图覆盖、文件可读与 hash。

## 局部重跑

失败时以 `character_id + variant/view` 为最小单位重跑；身份锚变化才扩大到该角色全部依赖，禁止默认重跑其他角色。
