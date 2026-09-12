# wenjing-video-continuity-reviewer

Pattern 5 Independent Reviewer，支持：

- PREFLIGHT：锁定 Script/Storyboard/条件资产的生成前门禁，含动态镜头时长 sanity check；
- POSTGEN：依据实际视频、帧、音频检查连续性和生成结果。

输出版本化 `06_qa/preflight_report_v{n}.md` 或 `postgen_{shot_or_batch_id}_v{n}.md`，并由 state 指向当前有效报告；RECHECK 不覆盖历史。只有 PREFLIGHT GREEN 才允许 Producer 消费；POSTGEN 缺少相应模态时必须 NOT_OBSERVABLE。本 Skill 不修上游、不写 Prompt、不生成视频。

新会话使用 `Continue {project_path}`，只重审变化项与邻接镜头。v0.1.2，provisional Silver。
