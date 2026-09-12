# Integration Guide

## 上游接棒

1. Storyboard Director 锁定 `05_storyboard_LOCKED.json`。
2. Continuity Reviewer PREFLIGHT 输出版本化报告，state 登记当前有效 report ref。
3. Producer P0 校验报告为 GREEN、`producer_eligible=true`，且 input hashes 与当前锁一致。
4. Visual Bible 仅在 Storyboard 标记 REQUIRED/SELECTED 时进入最小依赖闭包。

YELLOW/RED、STALE、hash mismatch 或缺失均不进入 Prompt 编译；Producer 不代替 Reviewer 修复。

## Prompt 与请求

每个 shot 一个 LOCKED Prompt Package。`generation_manifest.json.requests[]` 至少记录：

- shot_id / sequence_id
- prompt path 与 sha256
- ordered reference array（order、asset_id、path/url、sha256、purpose）
- provider/model/profile 与完整参数快照
- Dialogue/reference/parameter parity
- authorization scope
- 每次 attempt、request id、status、output refs、error、retry count

## 下游接棒

只有 `SUCCEEDED` 且实际 output refs 可定位的 shot/batch 才交 Reviewer POSTGEN。DRY_RUN 的合法终点是 `DRY_RUN_VALIDATED / WAITING_FOR_REAL_PILOT`，不得形成 POSTGEN 视觉结论。

## 恢复

Continue 时读取 state、manifest 和当前 scope；从 P0/P3/P5 最近合法 checkpoint 恢复。局部失败只把相关 Prompt/request/output 列入 affected，成功镜头与上游 LOCKED Artifact 列入 unaffected。
