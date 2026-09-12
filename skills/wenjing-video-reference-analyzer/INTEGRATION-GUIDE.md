# Integration Guide · wenjing-video-reference-analyzer

## 生态位置

- 类型：Pattern 5 Independent Skill。
- 路由：`auxiliary_route=REFERENCE_ANALYSIS`，不新增 content_route。
- 核心主链地位：可选分支，不是七件核心主链必经站。
- 主要消费方：`wenjing-video-narrative-designer`。

## 输入/输出

输入 transcript/video/frames/audio/mixed；输出遵循 `reference-analysis/0.1`：reference manifest、DRAFT、LOCKED。Narrative Designer 只读 LOCKED，并重算 SHA-256。

## 点将与隔离

- “拆解参考视频/学习爆款机制/分析节奏叙事镜头语言” → 本 Skill。
- “把 Truth Lock 设计成 Narrative Plan” → Narrative Designer。
- “写正式剧本” → Script Studio。
- “把现有文本改成逐镜分镜” → Storyboard 类 Skill。
- “参考生视频/生图”且目标是直接调用模型 → 生成 Skill。
- “完整做一条视频” → 未来薄总控。

## 接棒

本 Skill 完成后只提供直击口令，不自动运行下游。Narrative 采用优先级固定为：

`Case Truth Lock > 用户/项目约束 > Reference Analysis`

Reference 缺失或被 EXCLUDED 时，标准 CASE 流程不阻断；REQUIRED_BUT_INVALID 才回用户 Review。

## 安装

安装根：`{configured_skill_root}/wenjing-video-reference-analyzer`。历史素材留在独立资产库，不复制进 Skill package。

## 当前发布级别

先走 Bronze Local Ready；Silver 在 P9 工程测试、3 位真实用户及运行验收完成前保持 provisional。Committee 备案/积分不在本地施工中伪造。
