# Portable Runtime Contract v1.1

业务 Skill 只读写逻辑 Artifact，不感知平台安装目录、绝对路径、Board API 或 shell。Runtime Adapter 必须实现：解析 `project_ref`；按 `content_ref` 读取/写入版本化内容；读写 manifest/state；报告能力；在可用时计算 SHA-256；以原子写、事务或 compare-and-swap 保证登记一致性。

Artifact locator 固定字段：`artifact_id`、`artifact_type`、`version`、`status`、`content_ref`、`storage_backend`、`integrity_status`。状态登记再包含 `sha256/upstream_refs/upstream_integrity/approved_by/updated_at`。

能力枚举：`native_file_tools`、`python`、`shell`、`sha256`、`transactional_update`。业务 Skill 不得要求 shell；优先平台原生文件能力，其次可选 Python，再由 Adapter 实现。中文文本必须以 UTF-8 或平台等价 Unicode 保存。

Local File 使用逻辑 `/` 路径，由 Adapter 转换为宿主分隔符并限制在 project root。Document/Board 使用 document_id/object_ref；两者业务语义相同。
