# wenjing-video-visual-bible

Pattern 5 Independent Skill。把已锁定的正式案例视频 Script 转成可供 Storyboard 继承的 Visual Bible：资产清单、风格规范、身份锚、角色参考集、场景/道具参考集与 readiness 审计。

## 使用

触发后提供项目绝对路径。项目至少需要：

- `00_project_manifest.yaml`
- `00_project_state.md`
- `stage-outputs/03_script_LOCKED.md`

Skill 从 P0 校验开始，只加载当前 Stage 必需内容。核心输出位于 `stage-outputs/04_visual_bible/`。只有实际文件存在、hash 有效、依赖 READY 且通过审计的 required assets 才能进入 LOCKED manifest。

## 不做

不改剧本，不写逐镜 Storyboard/运镜，不写 Seedance Prompt，不调用视频生成。真实参考图生成是有工具与成本授权时的条件动作；没有授权时可完成规格，但资产保持未就绪。

## 恢复

新对话使用 `Continue {project_path}`。恢复以磁盘 state 为准，只重跑受影响资产，不默认从头开始。
