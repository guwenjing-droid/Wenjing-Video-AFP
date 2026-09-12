# Generation Execution and Logging

## 提交前原子检查

核对 request status、prompt sha256、ordered/planned references、capability profile、当前模式对应的 PREFLIGHT decision 和 authorization。任一变化即停止该 request。

## Attempt 记录

每次 attempt 追加：shot_id、attempt_no、request_id、submitted_at、provider/model、参数快照、prompt hash、reference order、status、output refs、error code/message、duration/cost（若可得）。Mock attempt 另强制 `is_mock=true, media_generated=false, external_cost=0`，且 request_id/output refs 为空。不得覆盖旧 attempt。

## 重试

瞬时网络/配额类错误可在授权轮次内局部重试；内容安全、能力不支持、Dialogue/asset mismatch 或 POSTGEN 连续性问题不自动重试。每次从 P3 或 P5 最近合法 checkpoint 恢复，并列出 unaffected outputs。

## 接棒

`SUCCEEDED` 且 output path/link 可访问只代表生成完成；随后把实际视频/帧/音频证据和 generation manifest 交给 Reviewer POSTGEN。Mock 结果只可交 Reviewer MOCK_POSTGEN 验证工程控制。DRY_RUN、MOCK、SUBMITTED、FAILED 均不可宣称真实 POSTGEN ready。
