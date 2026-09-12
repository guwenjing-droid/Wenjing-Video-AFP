# P3 请求一致性锁

逐 shot 核对 Prompt 声明与调用对象：对白逐字一致、reference 数量/顺序/用途一致；`creative_required_duration` 与 Storyboard 一致；`selected_generation_duration` 属于当前 profile 且不短于创作需求；trim plan 与 surplus 一致；duration/aspect/audio/quality/mode/model 字段一致；禁止项不冲突。这里仅校验 Producer 自己编译的请求，不重新判定上游内容质量。

全部通过后写 Prompt sha256 并标记 `READY_TO_SUBMIT`；任一 mismatch 标记 `BLOCKED`，定位本件字段或上游责任站。

## 输出 schema

```json
{"requests":[{"shot_id":"","prompt_sha256":"","reference_order":[],"duration_mapping":{"creative_required_duration":0,"selected_generation_duration":0,"mapping":"","trim_surplus_seconds":0},"parameter_parity":"PASS|FAIL","status":"READY_TO_SUBMIT|BLOCKED"}],"next_station":"P4|BLOCKED"}
```

PASS 后保留 DRAFT 审计链并锁定为 `{project_path}/stage-outputs/07_model_prompts/seedance/<shot_id>_LOCKED.md`；请求记录写入 generation manifest。

╭─ Gate ─────────────────────────────────────╮
│ HARD：Dialogue、reference、parameter parity │
│ 必须逐镜全 PASS。                           │
╰────────────────────────────────────────────╯

Hard Gate 未满足也不允许自动推进。

*P3 后加载 P4。*
