# State and Resume Rules

推荐状态文件为 `00_project_state.md`，其中包含一个可机器读取的 JSON/YAML 区块。

## 最小状态

- project ID、route、run mode、guidance mode；
- current stage、current artifact、last legal checkpoint；
- 各 Artifact 的 `artifact_id/type/version/status/content_ref/storage_backend/sha256/integrity_status/upstream_refs/upstream_integrity/approved_by/updated_at`；
- Gate 结果、失败代码、允许的 restart scope；
- 外部调用次数、后端、成本和授权状态；
- 最近更新时间与 continuation 指令。

## 状态转换

`DRAFT -> APPROVED -> LOCKED` 是正常路径。`LOCKED -> STALE` 只在上游有效版本改变时发生；不得直接把 STALE 改回 LOCKED，必须重新执行受影响节点并产生新版本。

## 恢复算法

1. 只读加载 manifest、state 和 last legal checkpoint。
2. 通过 Adapter 校验现存 LOCKED Artifact 的 content_ref、版本、完整性与依赖；本地可 hash 时必须 VERIFIED，无能力时显式 NOT_OBSERVABLE。
3. 若全部一致，从 `next_skill` 继续。
4. 若局部失败，计算最小影响域，仅重跑失败镜头、Artifact 或阶段。
5. 若上游变化，向下游传播 STALE，停止在第一个需要人工决定的 Gate。
6. 记录恢复原因、起点、重跑范围和新状态。

禁止每次恢复重新读取全部历史资产或从头执行整条产线。并发平台应使用原子更新、版本号或 compare-and-swap 防止状态覆盖。

报告状态另保存 `current_preflight_report_ref` 和版本关系；RECHECK 创建新版本，不覆盖旧报告。Local File 与 Document/Board 的解析规则见 [../runtime/runtime-contract.md](../runtime/runtime-contract.md)。
