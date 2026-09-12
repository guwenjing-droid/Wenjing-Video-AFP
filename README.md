# Wenjing Video AFP Portable v1.1

这是 `Wenjing-Video-AFP` 的 GitHub-ready 母版仓库。仓库中的 v1.1 Portable 内容是唯一 Source of Truth；平台差异只通过 `runtime/` 与 `adapters/` 处理，不在 Codex、WorkBuddy、OpenClaw 或 YouMind 内维护业务分叉。

## 快速安装

先获取整仓。远端创建后，将 `<YOUR_GITHUB_ACCOUNT>` 替换为实际 GitHub 账号或组织：

```bash
git clone https://github.com/<YOUR_GITHUB_ACCOUNT>/Wenjing-Video-AFP.git
cd Wenjing-Video-AFP
```

安装前先完成 [INSTALLATION_CHECKLIST.md](INSTALLATION_CHECKLIST.md)；不要给 Skill 目录附加版本后缀。

### Codex

将 `skills/` 下 12 个 canonical 目录批量复制到 `%USERPROFILE%/.codex/skills/`。先检查同名目录；升级时备份旧目录，再以本仓库对应目录替换。完成后新开 Codex 任务；若清单仍未刷新，再重启 Codex。详细规则见 [adapters/codex.md](adapters/codex.md)。

PowerShell 示例（只安装不存在的目录，不覆盖）：

```powershell
$skillRoot = Join-Path $env:USERPROFILE '.codex\skills'
Get-ChildItem -LiteralPath '.\skills' -Directory | ForEach-Object {
  $destination = Join-Path $skillRoot $_.Name
  if (Test-Path -LiteralPath $destination) { throw "Name conflict: $($_.Name)" }
  Copy-Item -LiteralPath $_.FullName -Destination $destination -Recurse
}
```

### OpenClaw

整仓 clone 后，把 `skills/` 下全部目录复制到 OpenClaw 实际配置的 Skill 根目录，保持“一目录一 Skill”。重新加载 Skill registry 或重启相应会话；不要把整个仓库当成一个 Skill。路径以目标安装配置为准，见 [adapters/openclaw-workbuddy.md](adapters/openclaw-workbuddy.md)。

### WorkBuddy

若 WorkBuddy 支持本地 Skill 目录，采用与 OpenClaw 相同的批量安装方式，并选择 Local File Adapter。必须验证 Truth Lock hash 同步、canonical 名称和 12/12 依赖可见性；无本地文件/hash 能力时改用 Document/Board Adapter。重新加载工作区或新开会话后复检。

### YouMind

YouMind 不应被假设为原生兼容 Codex Skill。必须导入整个仓库或至少同时导入 `manifest.yaml`、`contracts/`、`runtime/`、`adapters/youmind.md` 及当前路线涉及的 Orchestrator 和全部 Independent Skills。不能只读取 Orchestrator，也不能让总控自行模拟缺失下游。按 [adapters/youmind.md](adapters/youmind.md) 将 Artifact 映射为 Board Document / Agent / Workflow，并用 `DOCUMENT_BOARD` Adapter 保留 LOCK、Gate、State 和版本关系。

### Generic Agent Platform

能扫描 Skill 目录的平台批量注册 `skills/`；不能扫描的平台按 [adapters/generic-agent-platform.md](adapters/generic-agent-platform.md) 把每个 Skill 映射为独立 Agent/Workflow 节点，并先实现 Runtime 与 Artifact Contract。任何平台都不得只导入总控后模拟 Independent Skill。

## 解决的问题

这是文婧 AFP 视频生产系统的平台无关母版发行包。它解决多阶段视频生产中职责混杂、接口断裂、返工范围过大和平台迁移困难的问题，把项目拆成可审计、可接棒、可中断恢复的 Artifact 流程，支持从事实或创作意图到剧本、视觉资产规范、分镜、连续性门禁和生产参数的无成本 Dry Run。

## 当前支持的路线

- `CASE`：管理学、经济学与教学案例。
- `SOURCE_LOCKED`：忠实改编文章、小说、案例或原始剧本。
- `KNOWLEDGE`：知识、科普和课程讲解。
- `STORY`：原创故事、剧情和短剧。
- `REFERENCE_DRIVEN`：作为上述路线的可选分析分支，提炼参考视频的可迁移机制；它不是独立主链，也不直接生成最终剧本或分镜。

Commercial、Book Fast Lane、Series/IP、长期资产管理，以及 Kling/Veo 等非 Seedance Producer 适配器不在本版正式能力内。

## 架构

系统采用 Pattern 5：`1 Orchestrator + 11 Independent Skills`。薄总控只负责读取状态、选择最短合法路径、检查接棒条件、报站和恢复；业务判断由独立 Skill 完成。四条入口路线统一交付兼容的 `03_script_LOCKED.md`，再复用同一条下游：

```text
route entry -> 03_script_LOCKED.md -> Visual Bible -> Storyboard
            -> Continuity PREFLIGHT -> Producer -> Continuity POSTGEN
```

完整职责和路由见 [SYSTEM_OVERVIEW.md](SYSTEM_OVERVIEW.md)，规范性接口见 [contracts](contracts/)。

## 安装

原生支持 Skill 目录的平台，把 `skills/` 下每个独立目录复制到平台配置的 Skill 根目录，重新扫描或重启会话，再确认每项 `SKILL.md` 可见。Codex 的具体步骤见 [adapters/codex.md](adapters/codex.md)，OpenClaw / WorkBuddy 见 [adapters/openclaw-workbuddy.md](adapters/openclaw-workbuddy.md)。

不兼容 Codex/AFP Skill 格式的平台不要只导入单个提示词；应读取整个发行包，并把职责、Artifact Contract、Gate、State 和 Workflow 映射为平台自己的 Agent / Workflow / Board / Tool / Prompt / State。见 [MIGRATION_GUIDE.md](MIGRATION_GUIDE.md)。

## 调用方式

完整项目可调用 canonical id `wenjing-video-orchestrator`，提供目标、路线或来源材料、期望运行模式和 `project_ref`。`project_ref` 可以是本地目录，也可以是 Document/Board 对象引用；总控通过 Runtime Adapter 解析。总控只检查当前路线需要的 Skill，缺失时列出名称并 BLOCK，不自行模拟。

也可直接调用单个 Skill。例如，已有锁定剧本时可从 `wenjing-video-visual-bible` 或 `wenjing-video-storyboard-director` 开始；直接调用仍必须满足该 Skill 在 `SKILL.md` 中声明的输入锁和 Hard Gate，不能绕过上游契约。

## 运行模式与锁

- `FAST`：保留全部 Hard Gate，合并已授权的低风险 Review。
- `GUIDED`：普通 CASE/KNOWLEDGE 尽量合并为约 1–2 个关键人工确认点；事实冲突、叙事方向变化、LOCK 变更、高成本生成和 YELLOW/RED 仍确认。
- `STRICT`：使用更密集的审查点，适合高风险或高保真项目。

正式 Artifact 依次经历 `DRAFT -> APPROVED -> LOCKED`。LOCKED 文件不可静默覆盖；变更必须创建新版本或 Change Request，并把受影响的下游标为 `STALE`。

## 中断恢复

恢复时通过 Adapter 读取 manifest、state、最近的 LOCKED Artifact 和当前站必要资产。本地有 SHA-256 能力时必须验证；无 hash 能力时显式记录 `NOT_OBSERVABLE`，不得伪造。通过后从最近合法检查点继续；局部镜头或 Artifact 失败时优先局部重跑。规则见 [contracts/state-resume-rules.md](contracts/state-resume-rules.md)。

## Portable Runtime v1.1

业务 Skill 只依赖统一的 Artifact 语义：`artifact_id/type/version/status/content_ref/storage_backend/integrity_status`，不把 Windows/Unix 绝对路径或 shell 当协议。Local File 与 Document/Board 两类 Adapter 见 [runtime](runtime/)；平台差异只在 Runtime/Adapter 层处理。关键中文 stages/modules 随包本地展开并按 UTF-8 读取，不依赖运行时 CDN 外链。

Truth Lock 使用原子提交顺序：`finalize artifact → compute hash → update registry/state → verify`。PREFLIGHT/RECHECK 使用 `preflight_report_v{n}`，保留 supersession 关系，不覆盖历史报告。

## 成本与外部模型

本发行版的结构、路由、接棒、QA、restart/resume 和 Producer 参数输出已通过 Dry Run / Mock 验证；未完成真实人物/场景图像、Seedance/Kling/Veo 视频或最终视听质量验证。`DRY_RUN_GREEN` 只允许无成本 Dry Run，不授权真实生成。

真实媒体生产可能产生积分、排队和配额成本。运行者应在表达完整的前提下选择经济后端与最少必要镜头；任何真实生成前都应显示预计后端、镜头数、轮次和成本，并获得相应 Gate 授权。

Storyboard 不使用全片统一 10/12/15 秒默认值。每镜按对白、动作、运镜和理解成本推导 `creative_required_duration`；Reviewer 检查时长合理性，Producer 再映射为当前后端最小且足够的合法档位。无足够档位时必须拆镜，不得向下压缩。

## 完整性

在发行包根目录运行以下 PowerShell；每一行都应返回 `True`：

```powershell
Get-Content checksums/SHA256SUMS.txt | ForEach-Object {
  if ($_ -match '^([0-9a-f]{64})  (.+)$') {
    (Get-FileHash -Algorithm SHA256 -LiteralPath $Matches[2]).Hash.ToLower() -eq $Matches[1]
  }
}
```

校验清单不包含自身。版本与验证范围见 [VERSION.md](VERSION.md)，历史见 [RELEASES.md](RELEASES.md)。本版未调用真实媒体模型，外部积分消耗为 0。
