# Codex Adapter

## 安装

Windows 默认用户级目录通常为：

```text
%USERPROFILE%\.codex\skills
```

把本包 `skills/<skill-name>/` 的 12 个目录分别复制到该目录，最终应形成 `%USERPROFILE%\.codex\skills\<skill-name>\SKILL.md`。安装前检查同名目录；不要覆盖不相关或内容不同的 Skill。

## 刷新

Codex 的可见 Skill 清单可能在任务/会话开始时加载。复制后优先新开任务或会话；若仍未出现，再重启 Codex。已运行的旧任务可能继续使用启动时的清单。

## 验证

1. 检查 12 个目录和每个 `SKILL.md`。
2. 对照 [../manifest.yaml](../manifest.yaml) 核对名称与版本。
3. 对照 [../checksums/SHA256SUMS.txt](../checksums/SHA256SUMS.txt) 验证复制内容。
4. 新会话中查询 Skill 清单，确认所有名称可见。
5. 以 `run_mode: DRY_RUN` 调用 Orchestrator；确认不发生外部媒体调用。

运行项目使用 [Local File Adapter](../runtime/local-file-adapter.md)。安装目录名必须等于 canonical skill id，不能附加 `-v1.1`；版本由各 `SKILL.md` metadata 与发行 manifest 提供。升级 v1.0 时需用本包同名 12 个目录替换旧版本，再新开任务/会话刷新索引。

项目 Artifact 应写入独立项目工作目录，不要写回 Skill 安装目录。
