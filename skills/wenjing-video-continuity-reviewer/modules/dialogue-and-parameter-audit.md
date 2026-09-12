# Dialogue & Parameter Audit

Dialogue/VO 与 Script 按 ID、speaker、文字、标点、语气词和顺序逐字比较。POSTGEN 有音频时再检查可听内容、归属、截断与同步；只有 transcript 时不判口型/音质。

参数链分三层核对：project constraints → Storyboard creative duration → Producer backend mapping/prompt/call/generation manifest。Storyboard 的 `creative_required_duration` 是创作下限，不是后端档位；Producer 的 `selected_generation_duration` 必须取当前 profile 中不短于创作需求的最小合法档，或返回 SPLIT_REQUIRED，不得向下 clamp。duration mapping、aspect ratio、audio policy、reference order/purpose 等必须一致；Reviewer 只报告不改参数。模型专属结构由 Producer 提供后审，不写回 Storyboard。
