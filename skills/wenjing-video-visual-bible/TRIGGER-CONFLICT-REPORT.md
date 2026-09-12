# Trigger Conflict Report

## 结果

`PASS_WITH_ISOLATION`。未发现与已安装 `wenjing-*` 家族完全相同的精确触发词。

## 近邻与隔离

| 近邻 | 可能重叠 | 隔离条件 |
|---|---|---|
| wenjing-video-script-studio | 案例视频生产 | 本件要求 Script LOCKED，绝不写剧本 |
| 未来 wenjing-video-storyboard-director | 视觉/画面 | 本件做 canonical assets，不写逐镜机位/运镜 |
| autoglm-generate-image / vidu-skills | 图片生成 | 本件是项目 Visual Bible 流程；真实生图只是授权后的条件动作 |
| novel visual / comic skills | 人物场景/漫画 | 本件只服务已锁案例视频 Script，不处理小说提炼或漫画成稿 |

## 精确触发锚

`已锁剧本`、`视频视觉圣经`、`角色场景道具资产`、`04_visual_bible`、`Storyboard 可用资产`。

## 结论

Independent 单点领地清晰，无需 Committee 仲裁。若未来新增同名 Visual Bible Skill，按精确度和上游 Artifact Contract 重新预检。
