# Document / Board Adapter

适用 YouMind 和无本地文件系统的平台。

`project_ref` 映射 workspace/board id，`content_ref` 映射 document_id/object_ref。每次 LOCK 产生不可静默覆盖的新版本；manifest/state 通过结构化字段或平台数据库维护。

若平台能提供可信内容 digest，则写 `sha256` 并在匹配后标 `VERIFIED`。若不能，保留空 `sha256`，写 `integrity_status=NOT_OBSERVABLE`；不得删除字段或制造摘要。V0_1_DRY_RUN 可继续，STRICT/REAL PRODUCTION 可要求外部版本证明或 `VERIFIED`。

报告以 `preflight_report_v{n}` 独立对象保存；state 记录 current ref 与 supersession 关系。Board 列位置不能代替 Artifact status/version/Gate。
