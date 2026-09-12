# Integration Guide

- direct trigger：提供项目路径和指定来源。
- output：`01_source_lock_LOCKED.md`、`02_adaptation_plan_LOCKED.md`、`03_script_LOCKED.md`。
- next：`wenjing-video-visual-bible`。
- compatible：`script/0.1`，不需要下游理解 SOURCE_LOCKED 专用锁。
- optional：合法 Reference Analysis；缺失不阻断。
- failure：来源/时长冲突返回 BLOCKED，不降级为自由改编。

