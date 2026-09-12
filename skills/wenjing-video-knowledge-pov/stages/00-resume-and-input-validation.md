# P0 · 恢复与输入校验

*P0 加载：project-contract、reference-input-policy。*

读取 manifest/state、用户提供的知识材料/目标及 selected Reference；验证 `content_route=KNOWLEDGE`、路径、版本、hash、STALE 和开放 CR。禁止扫描全部历史资产。

输出 schema：audience、learning objective、source registry、Reference status、checkpoint、blockers、next=P1。

Hard Stop：主题/受众/知识来源均不足或 required Reference 无效则留在 P0；否则继续。不得自动编造知识来源。

