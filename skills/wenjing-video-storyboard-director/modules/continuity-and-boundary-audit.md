# Continuity & Boundary Audit

## 必查

1. Script scene/beat/action/Dialogue/VO/knowledge coverage 与 source refs；
2. sequence/beat/shot/atom ID 唯一，JSON schema 可解析；
3. 每镜存在 `estimated_duration/creative_required_duration/duration_basis/duration_driver`，兼容 `duration_seconds` 与 creative 值一致；总和与项目约束兼容；
4. Duration sanity：禁止无依据的大量等长镜头；对白朗读不超过镜头时长；复杂动作/运镜/理解内容不被压缩；简单插入或反应镜头不异常冗长；超载内容已经拆镜而非 clamp；
5. screen direction、eyeline、blocking、entry/exit、action match；
6. identity、wardrobe、scene/light、prop ownership/state；
7. 真实轨检查 Visual assets 的 LOCKED/READY/content_ref/integrity；`V0_1_DRY_RUN` 检查 LOCKED manifest、规格级 readiness 与 `planned_asset_refs`，并确认没有伪造真实媒体路径；
8. required asset binding closure：每个 `required=true` asset_id 至少被一个镜头引用；每个 `asset_refs/planned_asset_refs` 元素只能含一个独立 canonical asset_id，禁止 `CHR-001/002`、`CST-001/002` 等组合简写；任一失败不得 GREEN；
9. 不含新增剧本内容、canonical asset 修改、Preflight 结论、Seedance 参数/Prompt/API。

GREEN 才可 LOCK。YELLOW 需方向/歧义复核，RED 立即 BLOCK。失败记录 `affected_shots` 与 continuity neighbors；不受影响 sequence 保留，禁止默认整片重跑。
