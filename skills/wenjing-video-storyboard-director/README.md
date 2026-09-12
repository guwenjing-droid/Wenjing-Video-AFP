# wenjing-video-storyboard-director

Pattern 5 Independent Skill。读取已锁定 Script 与条件性 Visual Bible，输出模型无关 `05_storyboard_LOCKED.json`，供 Continuity Reviewer 做 Preflight。

## 最小输入

- `00_project_manifest.yaml`
- `00_project_state.md`
- `stage-outputs/03_script_LOCKED.md`
- manifest 明确要求/选择时：`04_visual_bible/asset_manifest_LOCKED.yaml` 与相关 READY 文件

## 关键保证

Script/Dialogue/知识点不增不删；复杂动作原子化；每镜按 SPEECH/ACTION/CAMERA/COMPREHENSION 推导可解释的最短充分时长，不默认 10/12/15 秒，超载优先拆镜；资产引用可验证；分镜不包含 Seedance 参数、Prompt 或视频调用。恢复从最近合法 checkpoint 开始，单镜失败不默认重跑整片。

## 输出

`stage-outputs/05_storyboard_DRAFT.json`、`05_storyboard_audit.md`、`05_storyboard_LOCKED.json`，并更新 manifest/state。

版本 v0.1.2；真实用户案例完成前为 AFP-SPEC provisional Silver。
