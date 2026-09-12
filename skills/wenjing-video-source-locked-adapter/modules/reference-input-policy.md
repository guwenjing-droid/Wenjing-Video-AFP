# Optional Reference Analysis Policy

仅当 manifest 明确 selected ref 时读取 Reference Analysis LOCKED，并校验 status、version、sha256、input_modality、observed_materials。未提供为 NOT_PROVIDED，不阻断。

只采纳 Transfer Engine 中非 source-specific、originality risk 可接受的机制。每条记录 `transfer_rule_id`、ADOPTED/REJECTED、理由和落点。任何冲突由来源原文与用户约束优先。transcript-only 规则不得被解释为镜头、运镜、表演、字幕、音乐或音效证据。

