# Gate Policy

## Gate 类型

- **Hard Gate**：锁、来源、契约、真实生成授权或无法自动判断的架构冲突不满足时立即停止。
- **Review Gate**：需要人类判断的方向、风格、高成本或高连续性选择。
- **Auto Gate**：schema、引用、哈希、覆盖、命名、状态转换等可确定校验。

## 模式

| 模式 | 确认密度 | 不可取消项 |
|---|---|---|
| FAST | 合并预授权的低风险 Review | 全部 Hard Gate |
| GUIDED | 普通 CASE/KNOWLEDGE 约 1–2 个关键确认点；异常时升级 | 全部 Hard Gate |
| STRICT | 更密集的阶段与 Artifact 审查 | 全部 Hard Gate |

低风险文件创建、填充冻结接口、常规校验、测试、文档补全和不改架构的修正可在同一阶段连续执行。

## 强制停止条件

修改冻结 Artifact Contract、改变 Skill 职责边界、增删核心 Skill、改变主链 Stage、大规模返工、删除验收文件、无法自动裁决的架构冲突，以及真实数据或内容方向需要人工决策时，必须等待明确授权。

本地可计算 hash 时 `FAIL` 必须 BLOCK。无 hash 能力时为 `NOT_OBSERVABLE`：V0_1_DRY_RUN 不因此自动 BLOCK；STRICT/REAL PRODUCTION 可要求 `VERIFIED`。禁止伪造 SHA-256。

## 媒体 Gate

- `DRY_RUN_GREEN`：仅允许生成 Prompt、参数、资产清单、generation plan 和 Mock 返回。
- `GREEN`：在项目明确授权真实生成且前置条件满足后才可签发。
- Dry Run 不得调用图像/视频模型，也不得把 Mock 结果称为真实质量验证。

## Duration Sanity Gate

- 缺少逐镜时长依据、对白/复杂动作明显超过创作时长、固定档位无依据套用或超载未拆镜：RED/HARD BLOCK。
- 大量等长但内容依据不同、简单镜头异常冗长：YELLOW，需解释或回 Storyboard Director。
- Producer 只有在后端档位不短于 creative duration 时可 READY；否则 SPLIT_REQUIRED，不得 clamp。
