# Knowledge Evidence Policy

每个 claim 具有 `claim_id`、exact claim、source/evidence locator、status（VERIFIED / USER_PROVIDED / UNVERIFIED）、qualifier、misconception risk。UNVERIFIED 不得作为确定事实进入 Script；可标注不确定性或阻断。

每个 knowledge point 有 `knowledge_id`、learning objective、prerequisite、example/metaphor、do-not-distort。钩子不得与锁定 claim 冲突。知识范围超过时长时，请用户缩小目标或扩展时长。

