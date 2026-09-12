# Trigger Conflict Report

判定：`PASS_WITH_ISOLATION`。

| 近邻 | 隔离 |
|---|---|
| wenjing-video-script-studio | 本件只接受 Script LOCKED，不写剧本 |
| wenjing-video-visual-bible | 本件只读 READY assets，不建 canonical assets |
| script-to-seedance-storyboard | 该类直接生成 Seedance 描述；本件输出模型无关 AFP JSON |
| commercial-ad-storyboard / pov-science-storyboard | 领域型一次性创作；本件只处理正式产线锁定 Artifact |
| 未来 continuity-reviewer / seedance-producer | 本件不做 Preflight，不写 Seedance Prompt/参数，不生成视频 |

精确锚：`Script LOCKED`、`05_storyboard_LOCKED.json`、`模型无关正式分镜`、`AFP 项目`。未发现完全相同精确触发词，无需仲裁。
