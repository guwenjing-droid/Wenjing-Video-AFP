# P4 · Dialogue, Voiceover & Knowledge Lock

> 只定稿逐字台词、旁白和知识表达，不改场次方向或写镜头。

## 执行

Read dialogue/VO policy。逐句检查 speaker、line_id、exact_text、intent、fact/knowledge refs、delivery note 和预计口播长度。旁白只用于确有必要的时间压缩、转场或知识解释，不补救场次因果漏洞。确保知识点 100% 覆盖或有 APPROVED omission；禁用绝对化、未核验数字和角色不可能知道的信息。

声音人格只写表演/语气提示，不创建视觉资产或选择 TTS 模型。

## 输出 schema 与落盘

更新 DRAFT Dialogue/VO Ledger、Knowledge Map、approved omissions、duration estimate；更新 state。

## Hard Stop

```text
╭─ Script Studio · P4 完成 ─╮
│ lines / speakers / knowledge coverage
│ duration estimate / omissions
│ 下一步：P5 Shootability & Boundary Audit
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────╯
```

不自动进入 P5。

---
*P4 确认后加载 `stages/05-shootability-and-boundary-audit.md`。*

