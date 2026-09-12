# OpenClaw / WorkBuddy Adapter

不同发行版的 Skill 根目录、frontmatter 支持和刷新命令可能不同，应以目标安装的实际配置为准。本包不假设固定路径。

## 原样安装检查

1. 确认平台支持“一目录一 Skill”，能扫描 `SKILL.md`。
2. 确认 Markdown/frontmatter 可解析，Skill 名称不会被重写。
3. 确认运行时可读取 Skill 内的相对路径及 `stages/`、`modules/`、`templates/`。
4. 把 `skills/<skill-name>` 复制到已配置的 Skill 根目录，避免再套一层发行包目录。
5. 重新加载注册表或重启会话，核对 12 个名称。
6. 为项目工作区提供读写权限，并验证 LOCKED 文件不可被静默覆盖。

## v1.1 WorkBuddy 实测修复点

- 目录和调用均使用 canonical `wenjing-video-<name>`；版本不进目录名。
- 有本地文件能力时启用 [Local File Adapter](../runtime/local-file-adapter.md)，Truth Lock 最终落盘后再算 hash，并同步 manifest/state 后读回验证。
- manifest/state 每个 Artifact 使用 v1.1 完整字段；expected/actual hash 不一致必须 BLOCK。
- 路径以逻辑 `content_ref` 表达，由 Adapter 归一化；不得硬编码 Windows/Unix 分隔符。
- shell 不是必需能力：平台原生文件工具优先，Python 可选，否则由 Adapter 提供读写/列举/hash。
- 若无 hash 能力，改用明确 `NOT_OBSERVABLE` 的 Document/Board 语义，不伪造 SHA-256。

## 兼容性不足时

若平台不能解析原生 Skill 结构，不要合并 Prompt。改用 [../MIGRATION_GUIDE.md](../MIGRATION_GUIDE.md) 的非原生映射方法，保留 Artifact、Gate、State 和路由语义。

OpenClaw 与 WorkBuddy 需要重新安装/刷新 v1.1 才会获得修复。安装成功仍应在目标环境做只读可见性检查；本发行包不宣称已在所有发行版注册。
