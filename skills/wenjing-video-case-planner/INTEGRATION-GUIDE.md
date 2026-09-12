# Integration Guide · wenjing-video-case-planner

## 1. Skill 身份

- name：wenjing-video-case-planner
- partner：wenjing
- skill_type：independent
- afp_spec_target：silver
- 当前分发级别：本地个人命名空间。
- AFP-ecosystem 状态：尚未提交或通过 Steering Committee 备案，不宣称官方上架或积分记账。

## 2. 安装位置

    {configured_skill_root}/wenjing-video-case-planner/

安装目录只保存 Skill 包。案例原文、状态文件和 Truth Lock 保存在 D 盘独立运行项目目录，不写入 Skill 包。

## 3. 上游入口

Direct Use 输入原始案例、论文、概念或用户文本。没有项目目录时按模板建立最小 manifest/state。

Orchestrator Handoff 必须提供：

- 00_project_manifest.yaml
- 00_project_state.md
- next_station = wenjing-video-case-planner

无论哪种入口，第一动作都是加载 P0 扫描磁盘，不依赖对话摘要。

## 4. 下游交接

正式下游：wenjing-video-narrative-designer。

交接条件：

1. stage-outputs/01_case_truth_lock_LOCKED.md 存在。
2. status 为 LOCKED。
3. 必填章节完整。
4. SHA-256 与 manifest/state 一致。
5. stage_status.case_planner = COMPLETE。
6. next_station = wenjing-video-narrative-designer。

Case Planner 只登记下一站和直击口令，不自动运行未安装或未确认的下游 Skill。

## 5. Artifact Contract

- Draft：stage-outputs/01_case_truth_lock_DRAFT.md
- 正式继承物：stage-outputs/01_case_truth_lock_LOCKED.md
- 状态：00_project_state.md
- 路由配置：00_project_manifest.yaml
- 变更申请：change-requests/CR-{id}.md

下游只读 LOCKED；变更必须通过 Change Request，受影响依赖物标记 STALE。

## 6. 家族触发隔离

- Orchestrator：完整视频、开始视频项目、视频全流程等宽口令。
- Case Planner：案例事实锁、教学目标和视频改编边界。
- Narrative：钩子、冲突、悬念、共鸣和情绪曲线。
- Script：正式视频剧本。
- Visual Bible：人物、场景、道具和参考资产。
- Storyboard：模型无关分镜。
- Continuity：连续性质检。
- Producer：Seedance Prompt、Pilot 和生成记录。

## 7. 本地验证与后续验收

- 静态结构、路径、frontmatter 与内部引用：P7 验证。
- AFP-SPEC 正式自检：P8。
- 主要触发、变体触发、隔离口令、Hard Stop、写盘和 Continue：P9 新会话测试。
- Silver 目标需完成规定的真实案例测试；在测试完成前只标目标等级，不签发通过证书。

## 8. 版本兼容

- video project contract：v0.2
- case truth lock schema：v0.2
- Skill：v0.1.0
- Breaking change：Artifact 字段、枚举、文件名或 next_station 改动时必须先升版正式编排方案并做兄弟同治检查。
