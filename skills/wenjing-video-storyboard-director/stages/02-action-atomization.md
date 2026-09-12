# P2 · Action Atomization

## 边界

只将复杂动作拆成可观察、可排序、可完成的 action atoms；不决定 Seedance Prompt。

## 执行

1. Read `modules/action-atomizer.md`。
2. 将每个复杂动作拆成 `start_state → motion → contact/change → end_state`，写主体、对象、方向、空间与完成标志。
3. 同一 atom 只保留一个主动作；并行动作明确 simultaneous，因果动作明确顺序。
4. 动作无法在约束时间内清晰执行时，给“拆镜/延长/删减非 Script 内容”合法方案；不得擅删 Script 动作。

## 输出 schema

回填 DRAFT 中 `action_atoms[]`，每条含 `atom_id/source_refs/actor/verb/object/start/end/spatial_relation/completion_cue`；更新 state。

## Gate

```
╭─ Storyboard Director · P2 完成 ───────────╮
│ action atoms：{N} · ambiguous：{N}
│ 可执行性：{PASS|REVIEW|BLOCK}
│ 下一步：P3 Shot Grammar & Blocking
╰───────────────────────────────────────╯
```

即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式

- 不用“激烈争执/认真思考”代替可见动作；不把多个连续动作塞入一个 atom；不虚构动作结果。

---
*P2 完成后加载 `stages/03-shot-grammar-and-blocking.md`。*
