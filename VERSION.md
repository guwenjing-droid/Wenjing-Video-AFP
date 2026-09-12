# Version

- 发行名称：Wenjing-Video-AFP-Portable
- 发行版本：1.1.0
- 创建日期：2026-09-12
- 编排基线：视频生产编排方案 v0.8 + Portable Runtime Contract v1.1
- 架构：1 Orchestrator + 11 Independent Skills
- 正式 Skill 数量：12
- 支持路线：CASE、SOURCE_LOCKED、KNOWLEDGE、STORY；REFERENCE_DRIVEN 为可选分支

## 验证状态

- 核心体系：无成本结构、契约、路由、Gate、状态与 Dry Run 已验收。
- 三个扩展入口：P9 已通过；联合回归 128/128（SOURCE_LOCKED 19、KNOWLEDGE 19、STORY 20、联合 70）。
- FIX-01–08：Truth Lock 原子 hash 同步、统一 state schema、Reviewer integrity、Storyboard asset closure/canonical refs、canonical Skill 名、路线依赖检测、路径归一化和 shell-free fallback 已通过。
- RECHECK-01：两个模板源文件均非空，未修改；YouMind 问题归类为 CDN/read/fetch 限制。
- RECHECK-02：关键中文指令随包本地展开并要求 UTF-8，不依赖运行时 CDN 外链。
- 回归：27 个既有 Skill 测试套件通过；新增跨平台动态回归 15/15，通过 Microsoft CASE 与沉没成本 KNOWLEDGE 既有样本。
- 真实媒体生成：未执行。
- 真实图像/视频质量：未验证。
- 外部积分消耗：0。

## 已知限制

Seedance Producer 是当前唯一正式后端适配器；其他模型需兼容 adapter。Mock POSTGEN 只能验证契约、状态、restart/resume，不能证明画面、表演、声音或跨镜一致性的真实质量。Commercial、Book、Series/IP 和长期资产管理尚未形成正式 Independent Skill。YouMind/WorkBuddy 的平台内安装与 UI 行为仍需各平台重新导入 v1.1 后验证。
