# Local File Adapter

适用 Codex、OpenClaw、具备本地文件能力的 WorkBuddy。

1. `project_ref` 解析为已授权项目根。
2. `content_ref` 使用逻辑 `/`，逐段安全拼接；拒绝越界 `..`、磁盘根和未授权绝对路径。
3. LOCKED 提交按 `finalize → SHA-256 → manifest/state 同步登记 → read-back verify`。
4. 下游核对 status/version/expected hash/actual hash；不一致标 `FAIL` 并 BLOCK。
5. 文件工具优先平台原生接口；Python 可选；不得要求 ls/grep/which/bash。
