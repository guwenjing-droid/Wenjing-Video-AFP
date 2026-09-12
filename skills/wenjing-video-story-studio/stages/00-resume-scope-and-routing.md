# P0 · 恢复、范围与分流

*P0 加载：project-contract、reference-input-policy。*

读取 manifest/state、用户故事意图及 selected Reference；校验 `content_route=STORY`、版本、hash、STALE 和 CR。判断是否原创单集：若要求忠实改编现有来源，转 source-locked-adapter；若是多集/IP 长期管理，返回 NOT_IMPLEMENTED。

输出 schema：scope、audience/platform/duration、inputs、Reference status、route decision、checkpoint、blockers、next=P1。

Hard Stop：路线歧义或超出 SINGLE_EPISODE 时留在 P0；否则继续。不得自动吞并系列能力。

