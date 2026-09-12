# Installation Checklist

## 1. Repository Integrity

- [ ] 已完整 clone 仓库，而不是只下载 Orchestrator。
- [ ] `VERSION.md` 为 `1.1.0`。
- [ ] `checksums/SHA256SUMS.txt` 校验通过。
- [ ] 未把 `runs/`、临时测试或本机配置混入安装目录。

## 2. Skills 12/12

- [ ] `wenjing-video-orchestrator`
- [ ] `wenjing-video-case-planner`
- [ ] `wenjing-video-reference-analyzer`
- [ ] `wenjing-video-narrative-designer`
- [ ] `wenjing-video-script-studio`
- [ ] `wenjing-video-source-locked-adapter`
- [ ] `wenjing-video-knowledge-pov`
- [ ] `wenjing-video-story-studio`
- [ ] `wenjing-video-visual-bible`
- [ ] `wenjing-video-storyboard-director`
- [ ] `wenjing-video-continuity-reviewer`
- [ ] `wenjing-video-seedance-producer`

每个目录必须直接包含 `SKILL.md`。frontmatter `name` 必须与以上 canonical 名称完全一致；目录名不得附加 `-v1.0`、`-v1.1` 等版本后缀。

## 3. Orchestrator Dependency Discovery

- [ ] CASE 路线能发现 case-planner、narrative-designer、script-studio 和四个通用下游执行件。
- [ ] SOURCE_LOCKED、KNOWLEDGE、STORY 能发现各自入口及通用下游。
- [ ] 选择 Reference 分支时能发现 reference-analyzer。
- [ ] 故意隐藏一个必需 Skill 时，总控明确列出 `missing_skills` 并 BLOCK，而不是模拟该 Skill。

## 4. Artifact Contract

- [ ] 每个 Artifact 有 `artifact_id/type/version/status/content_ref/storage_backend`。
- [ ] state 同时保留 `sha256/integrity_status/upstream_refs/upstream_integrity/approved_by/updated_at`。
- [ ] Local File 下 hash 不一致会 BLOCK。
- [ ] 无 hash 能力时使用 `NOT_OBSERVABLE`，不伪造 SHA-256。
- [ ] LOCKED 文件变更生成新版本并传播 STALE。
- [ ] PREFLIGHT/RECHECK 使用 `preflight_report_v{n}`，不覆盖历史。

## 5. Runtime Adapter

- [ ] Codex/OpenClaw/具备本地文件能力的 WorkBuddy：选择 `runtime/local-file-adapter.md`。
- [ ] YouMind/无本地文件系统平台：选择 `runtime/document-board-adapter.md`。
- [ ] `content_ref` 由 Adapter 解析，不把本机绝对路径当跨平台协议。
- [ ] 业务 Skill 不依赖 ls、grep、which 或 bash。
- [ ] 中文文件使用 UTF-8 或等价 Unicode，不依赖运行时 CDN。

## 6. Post-install Smoke Test

- [ ] 重新扫描、重新加载或新开会话后，12 个 Skill 均可见。
- [ ] 运行一次 CASE 或 KNOWLEDGE Dry Run。
- [ ] 外部媒体调用次数保持 0。
- [ ] Orchestrator 选择最短合法路径，并可从最近合法检查点恢复。
