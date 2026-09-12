# Evidence & Claim Policy

## Claim 分层

| 类型 | 含义 | 写法 |
|---|---|---|
| OBSERVATION | 材料中可直接定位 | 描述所见/所闻/所读 + anchor |
| VIDEO_CLAIM | 视频创作者提出的事实性主张 | “视频声称……”；不自动背书 |
| ANALYTIC_INFERENCE | 分析者基于观察作出的解释 | 标 confidence 与替代解释 |
| EXTERNALLY_VERIFIED | 用外部可靠来源另行核验 | 只进 External Supplements，含来源与日期 |
| UNVERIFIED | 无法验证或来源不足 | 明示，不进入已核验事实 |

## Evidence Anchor

允许：`transcript:L12-L18`、`T00:00:03-00:00:08`、`frame:F023@00:00:07.2`、`audio:T...`。只有摘要或不可定位材料时用 `ANCHOR_LIMITED`；严禁编造行号、时间码和 frame_id。

每个 anchor 记录 source path、locator、支持的 claim_id。一个锚不能证明其范围之外的因果结论。

## 外部补充

默认不联网、不自动扩展。若用户明确提供/要求，必须记录 source、title、published/accessed date、verification status，并与原视频观察分栏；不得反写为“视频提到”。

