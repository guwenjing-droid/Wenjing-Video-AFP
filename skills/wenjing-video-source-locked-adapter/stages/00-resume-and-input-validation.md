# P0 · 恢复与输入校验

*P0 加载：project-contract、reference-input-policy。*

读取项目路径、manifest/state、用户指定来源及可选 selected Reference。校验文件、版本、hash、STALE、开放 CR 与 `content_route=SOURCE_LOCKED`。已有合法检查点则恢复，不重读无关历史资产。

输出 schema：输入清单、来源 locator/版本、Reference 状态、最近合法 checkpoint、blockers、next=P1。

Hard Stop：来源或范围不明确、输入失效、required Reference 无效时留在 P0；否则自动进入 P1。本阶段不得自动改写来源。

