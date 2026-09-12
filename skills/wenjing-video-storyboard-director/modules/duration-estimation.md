# Dynamic Shot Duration Estimation

## 目标

为每个 shot 推导可解释的“最短充分时长”，而不是套用统一时长。Storyboard 只定义创作需求，不绑定后端生成档位。

## 输入与估算

1. `speech_time`：使用项目配置的语速区间；中文可记录 `characters_per_second_range`、所选语速及标点/情绪停顿。没有配置时给出区间和选择理由，不写死单一语速。
2. `action_time`：按 action atoms 的顺序/并行关系、复杂度、位移和 completion cue 估算；多阶段事件不得压成一次未完成动作。
3. `camera_time`：静态建立、推拉、摇移、跟拍、焦点迁移和多角色调度分别估算完成所需时间。
4. `comprehension_floor`：数据、屏幕文字、手机信息、关键知识点、情绪反转和空间建立必须给观众足够识别时间。
5. `transition_buffer`：为自然停顿、动作收束和剪辑衔接增加少量缓冲。只有明确登记的跨镜 overlap credit 才可抵扣，且不得使最终值低于 speech/action/camera/comprehension 任一硬下限。

概念计算：

```text
core_required = max(speech_time, action_time, camera_time, comprehension_floor)
creative_required_duration = core_required + transition_buffer - justified_overlap_credit
```

若采用“减 transition buffer”的记法，必须把该字段解释为 `justified_overlap_credit`，不能把本应保留的自然停顿直接减掉。

## 每镜输出

```json
{
  "estimated_duration": 6.5,
  "creative_required_duration": 6.5,
  "duration_seconds": 6.5,
  "duration_driver": "MIXED",
  "duration_basis": {
    "speech_time": {"seconds": 5.8, "rate_range": "3.5-4.5 zh_chars_per_second", "selected_rate": 4.0},
    "action_time": {"seconds": 4.5, "atoms": 2, "sequence": "SEQUENTIAL"},
    "camera_time": {"seconds": 3.0, "behavior": "SLOW_PUSH"},
    "comprehension_floor": {"seconds": 5.5, "reason": "KEY_KNOWLEDGE"},
    "transition_buffer": 0.7,
    "justified_overlap_credit": 0,
    "explanation": "对白与知识理解共同决定，留 0.7 秒收束"
  },
  "producer_duration_mapping": "REQUIRED"
}
```

`duration_driver` 只能为 `SPEECH | ACTION | CAMERA | COMPREHENSION | MIXED`。多个候选值接近或共同构成硬下限时用 MIXED。`duration_seconds` 是 v0.1 兼容镜像，不是模型参数。

## 拆镜与异常

- 超过 `constraints.creative_single_shot_ceiling`、包含不可并行的长对白与复杂动作，或模型无关语义已经过载时，优先沿 beat/action completion cue 拆镜。
- 拆镜不得改写、删除或新增 LOCKED Script；每个新 shot 保留原 source refs、Dialogue range 与 continuity entry/exit。
- 无后端 profile 时不猜固定档；写 `PRODUCER_MAPPING_REQUIRED`。
- 极短插入、反应或单一信息镜头可短于主镜头；复杂动作、长对白和多阶段事件不得为省积分过度压缩。
- 大量完全等长镜头只有在逐镜依据确实相同时才合法；否则审计为异常。
