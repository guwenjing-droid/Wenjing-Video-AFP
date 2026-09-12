# P4 · 模式专项评估

## 边界
只执行所选模式专项 checks；不跨模式作结论。

## 执行
- PREFLIGHT：Read `modules/preflight-checks.md`，检查提交包完整、引用顺序/用途可映射、Dialogue、场景/角色/道具状态，并执行 Duration Sanity Check（异常等长、对白超时、复杂动作不足、简单镜头冗长、超载未拆镜），再判断比例/音频策略和限制项是否足以交给 Producer。
- POSTGEN：Read `modules/postgen-observability.md`，以视频时间码/帧/音频证据查实际身份漂移、穿帮、动作完成、口型/对白、字幕水印、声画与连续性。无相应模态不得 PASS。
- MOCK_POSTGEN：Read `modules/postgen-observability.md`，只检查模拟成败、状态更新、局部 rerun scope、成功记录保留和 resume checkpoint；实际视听维度全部 NOT_OBSERVABLE。

## 输出 schema
报告 DRAFT 写 `mode_checks[]`、`duration_sanity_checks[]` 和 evidence anchors；每项时长问题记录 shot_id、severity、expected floor、observed duration、basis 与 owner_stage。PREFLIGHT 不出现实际画面 PASS，POSTGEN 不复用 preflight GREEN 代替观察，MOCK_POSTGEN 不产生任何媒体质量 PASS。

## Gate
```
╭─ Continuity Reviewer · P4 完成 ───────────╮
│ mode checks：PASS {N} / FAIL {N} / N/O {N}
│ 下一步：P5 严重度与补救
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不在 PREFLIGHT 声称成片正常；不以任务成功代替媒体审查；不从少量帧判断全时段。

---
*P4 完成后加载 `stages/05-severity-and-remediation.md`。*
