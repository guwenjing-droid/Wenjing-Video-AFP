# Trigger Conflict Report

## 结论

风险可控。Producer 的触发词限定为“已锁定分镜 + GREEN PREFLIGHT 后的 Seedance 编译/生成/记录”。

## 邻接隔离

| 邻接 Skill | 易混请求 | Producer 不做 |
|---|---|---|
| storyboard-director | 写分镜、镜头设计 | 不改镜头意图 |
| continuity-reviewer | 生成前/后 QA | 不输出 GREEN/YELLOW/RED |
| script-to-seedance-storyboard | 把原文改分镜描述 | 不从原文直接生成分镜 |
| commercial-ad-storyboard | 广告创意与分镜 | 不做广告创意 |
| video-reference-analyzer | 拆解参考视频 | 不逆向分析参考视频 |

## 隔离句

未提供 AFP LOCKED Storyboard 与 GREEN PREFLIGHT 的普通“写 Seedance 提示词”请求，不应进入本 Skill 的真实生成路径；可提示先完成上游或仅做明确标记的非产线草案。

