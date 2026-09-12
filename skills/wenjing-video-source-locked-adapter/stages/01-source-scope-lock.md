# P1 · Source Scope Lock

*P1 加载：source-fidelity-policy。*

枚举用户选定范围的全部 source_span_id，标记原对白、叙述、动作、顺序、不可变事实与禁止项，生成 `01_source_lock_DRAFT.md`。展示范围与覆盖基数。

输出 schema：header、source registry、selected scope、span ledger、verbatim dialogue ledger、immutables、exclusions、approval。

Hard Stop：这是内容真值 HARD Gate；用户批准后另写 LOCKED。不得自动缩小范围或进入 P2。

