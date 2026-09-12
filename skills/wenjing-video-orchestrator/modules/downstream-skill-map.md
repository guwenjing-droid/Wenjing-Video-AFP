# Downstream Skill Map

| 顺序 | Skill | 必需输入 | 正式输出 | 放行 |
|---:|---|---|---|---|
| 0A | wenjing-video-reference-analyzer | 四条路线可选参考材料 | `00_reference_analysis/{id}_LOCKED.md` | optional contract valid |
| 1C | wenjing-video-case-planner → narrative-designer → script-studio | CASE 原料 | `03_script_LOCKED.md` | 三个 CASE 锁 valid |
| 1S | wenjing-video-source-locked-adapter | 指定来源与忠实范围 | `01_source_lock` + `02_adaptation_plan` + `03_script_LOCKED.md` | fidelity/script valid |
| 1K | wenjing-video-knowledge-pov | 知识材料、受众、教学目标 | `01_knowledge_truth_lock` + `02_knowledge_narrative_plan` + `03_script_LOCKED.md` | truth/script valid |
| 1T | wenjing-video-story-studio | 原创单视频/单集故事意图 | `01_story_brief` + `02_story_plan` + `03_script_LOCKED.md` | canon/script valid |
| 4 | wenjing-video-visual-bible | Script | `04_visual_bible/asset_manifest_LOCKED.yaml` | REAL_GREEN 或当前合法 DRY_RUN_GREEN |
| 5 | wenjing-video-storyboard-director | Script + conditional Visual | `05_storyboard_LOCKED.json` | audit GREEN |
| 6 | wenjing-video-continuity-reviewer | locks + evidence scope | `06_qa/preflight_report_v{n}.md` | GREEN 或 DRY_RUN_GREEN |
| 7 | wenjing-video-seedance-producer | Storyboard + eligible Preflight | prompts + generation manifest/log | DRY_RUN_VALIDATED/MOCK_VALIDATED 或真实结果 |
| 8 | wenjing-video-continuity-reviewer | generation evidence | mock/postgen report | MOCK_PASS 或真实 POSTGEN decision |

未实现路线 `COMMERCIAL/BOOK_FASTLANE/SERIES_IP` 一律返回 `NOT_IMPLEMENTED/BLOCKED`。四条已实现路线的入口均可选择合法 Reference Analysis；入口之后只通过 `03_script_LOCKED.md` 合流，不重建通用下游。

## Route Dependency Registry

以下均为 canonical skill id；不得附加版本后缀，也不得按目录名调用：

| route | required skills（按执行顺序） |
|---|---|
| CASE | `wenjing-video-case-planner`, `wenjing-video-narrative-designer`, `wenjing-video-script-studio`, `wenjing-video-visual-bible`, `wenjing-video-storyboard-director`, `wenjing-video-continuity-reviewer`, `wenjing-video-seedance-producer` |
| SOURCE_LOCKED | `wenjing-video-source-locked-adapter`, `wenjing-video-visual-bible`, `wenjing-video-storyboard-director`, `wenjing-video-continuity-reviewer`, `wenjing-video-seedance-producer` |
| KNOWLEDGE | `wenjing-video-knowledge-pov`, `wenjing-video-visual-bible`, `wenjing-video-storyboard-director`, `wenjing-video-continuity-reviewer`, `wenjing-video-seedance-producer` |
| STORY | `wenjing-video-story-studio`, `wenjing-video-visual-bible`, `wenjing-video-storyboard-director`, `wenjing-video-continuity-reviewer`, `wenjing-video-seedance-producer` |

当用户/manifest 选择参考分支时，在对应入口前另要求 `wenjing-video-reference-analyzer`。启动检查只验证当前 route 加已选可选分支；缺一项就列入 `missing_skills` 并 BLOCK，不自行模拟。
