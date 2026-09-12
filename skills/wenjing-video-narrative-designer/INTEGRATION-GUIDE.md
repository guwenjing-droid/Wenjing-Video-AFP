# Integration Guide · wenjing-video-narrative-designer

## 1. Skill 身份

- name：`wenjing-video-narrative-designer`
- partner：`wenjing`
- skill_type：`independent`
- Skill release：`v0.1.0`
- afp_spec_target：Silver（P8/P9 完成前不宣称已认证）
- 当前分发：本地个人命名空间
- AFP-ecosystem：尚未提交或通过 Steering Committee 备案，不宣称官方上架、授权或积分记账

## 2. 安装位置

```text
{configured_skill_root}/wenjing-video-narrative-designer/
```

安装目录只保存 Skill package。运行项目、案例材料、状态和正式 Artifacts 保存在 D 盘项目目录，不写入 Skill 包。

## 3. 上游接棒

正式上游：`wenjing-video-case-planner`。

必需输入：

1. `00_project_manifest.yaml`
2. `00_project_state.md`
3. `stage-outputs/01_case_truth_lock_LOCKED.md`

P0 必须验证 Truth Lock 的状态、版本、完整性登记、STALE 和开放 CR；失败即 BLOCKED。

## 4. 可选 Reference Analysis 接棒

可选上游：`wenjing-video-reference-analyzer`。

```text
stage-outputs/00_reference_analysis/<reference_id>_LOCKED.md
```

- 未提供时不阻断标准 CASE 主链。
- 只有 manifest 声明 REQUIRED 且 Artifact 无效时才阻断。
- 采用优先级：`Case Truth Lock > 用户/项目约束 > Reference Analysis`。
- transcript-only 不得支持未观察的视听判断。
- 只有通过模态、可观察性、原创迁移和采用 Gate 的 transfer rule 才能进入 Narrative Plan。

## 5. 下游交接

正式下游：`wenjing-video-script-studio`。

正式输入：

1. `stage-outputs/01_case_truth_lock_LOCKED.md`
2. `stage-outputs/02_narrative_plan_LOCKED.md`
3. manifest/state

Script Studio 不直接依赖原始 Reference Analysis。已批准的抽象机制及 provenance 由 Narrative Plan 携带。

## 6. Artifact 与版本兼容

- Pipeline plan：v0.3
- Project manifest/state：v0.3
- Narrative Plan schema：v0.2
- Reference Analysis Contract：v0.1
- Skill：v0.1.0

文件名、必填字段、枚举、采用优先级或 next station 发生语义变化时，必须先走 CR 和正式编排方案升版。

## 7. 家族触发隔离

- Case Planner：案例事实、知识点、教学目标、改编边界。
- Reference Analyzer：拆解参考视频并输出可迁移机制。
- Narrative Designer：在已锁 Truth 上设计 Hook、Participation、Nodes、Emotion 和 Knowledge Map。
- Script Studio：正式台词、场次与可拍剧本。
- Visual Bible / Storyboard / Reviewer / Producer：分别处理资产、分镜、质检与模型生成。
- Orchestrator：完整视频、视频全流程等宽口令；最后创建。

## 8. 本地验证与验收顺序

1. P7：结构、路径、命名空间、触发词静态预检和本地安装。
2. P8：AFP-SPEC 合规检查并签发自评状态。
3. P9：单件触发/隔离/写盘/续传测试；Case Planner → Narrative 接棒测试。
4. `wenjing-video-reference-analyzer` 建成后：Reference Analysis LOCKED → Narrative 专项接棒测试。
5. 核心产线完成后：真实管理学案例纵向联跑。

## 9. 当前上架状态

- 本地安装：已完成；源包与安装副本 24/24 文件一致。
- AFP 官方备案：待未来用户另行发起，不阻塞本地 v0.1。
- Committee 审议、积分和分成：未启用，不作任何已通过声明。
