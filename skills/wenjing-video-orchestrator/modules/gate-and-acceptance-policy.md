# Gate and Acceptance Policy

- FAST：减少 REVIEW 频率，可使用已登记预授权；Hard Gate 不取消。
- GUIDED：普通 CASE/KNOWLEDGE 流程以约 1–2 个关键人工确认点为目标，聚焦事实/教学或叙事方向与最终 LOCK；同一方向内的常规填充、校验、测试和文档补全连续执行。事实冲突、叙事方向变化、LOCK 变更、高成本生成或 YELLOW/RED 仍立即确认，不降低 Hard Gate。
- STRICT：关键方向、核心资产、分镜和真实生成逐项确认。

`V0_1_DRY_RUN`：Visual 规格可 dry-run ready；Reviewer 输出 DRY_RUN_GREEN；Producer 只做 Prompt/参数/计划和 Mock；真实媒体为 DEFERRED。

`REAL_MEDIA`：资产必须实际 READY；Preflight 必须 GREEN；真实调用另需当前能力档、成本授权与合法后端。DRY_RUN_GREEN 永远不能升级为真实生成许可。
