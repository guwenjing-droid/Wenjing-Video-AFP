# P2 · 忠实改编计划

*P2 加载：source-fidelity-policy、reference-input-policy。*

为每个 span 指定 treatment、scene destination 和顺序；评估时长可行性。可给 2–3 个不改变内容的节奏/呈现方案。Reference 只提供可迁移机制并记 adopted/rejected。

输出 schema：plan header、span-to-scene map、timing、adopted_transfer_rule_ids、rejected rules、unresolved items、approval。

Hard Stop：任何 omission、改对白、顺序/因果变化或时长冲突即 BLOCK；FAST 可一次 REVIEW，GUIDED/STRICT 等用户批准。不得自动进入 P3。

