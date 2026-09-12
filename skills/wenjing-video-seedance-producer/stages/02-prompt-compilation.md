# P2 Prompt 编译

按当前 scope 逐 shot 生成七段 Prompt Package：输出设置、Dialogue Lock、角色锁、参考资产有序说明、场景/道具状态、逐秒时间轴、Negative Constraints。Output Settings 同时记录 Storyboard 的 `creative_required_duration`、后端 `selected_generation_duration`、映射策略和裁切计划，二者不得混为同一字段。每条声明绑定 source ref；缺失内容写 `NONE/NOT_PROVIDED`，不得补写。

镜头术语只用 Storyboard 已表达的景别、机位、运镜和动作。对同一资产优先复用已锁引用；不读取无关历史 Prompt。

## 输出 schema

```json
{"prompt_packages":[{"shot_id":"","path":"","source_refs":[],"creative_required_duration":0,"selected_generation_duration":0,"duration_mapping":"EXACT|ROUND_UP_AND_TRIM|SPLIT_REQUIRED","status":"DRAFT|BLOCKED"}],"blocked":[],"next_station":"P3|BLOCKED"}
```

每镜落盘为 `{project_path}/stage-outputs/07_model_prompts/seedance/<shot_id>_DRAFT.md`。

╭─ Gate ──────────────────────────────────────╮
│ HARD：不得新增上游未授权的事实、对白或镜头。│
╰─────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P2 后加载 P3。*
