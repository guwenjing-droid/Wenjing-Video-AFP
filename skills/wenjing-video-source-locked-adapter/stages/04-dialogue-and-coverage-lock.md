# P4 · 对白与覆盖锁

*P4 加载：source-fidelity-policy、script-output-contract。*

逐字比对全部原对白；核对每个 selected span 恰有一个合法 treatment 与 Script 落点。局部失败只返工对应 scene/line。

输出 schema：dialogue diff（必须 0）、span coverage `mapped/selected`、sequence check、fact check、open issues。

Hard Stop：`mapped=selected`、dialogue diff=0、顺序/事实错误=0 才可进入 P5；校验可自动执行，但不得自动豁免。

