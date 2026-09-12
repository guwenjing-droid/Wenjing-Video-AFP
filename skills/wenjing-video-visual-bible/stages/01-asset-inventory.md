# P1 · 资产盘点

> Visual Bible · Stage 01

## 边界

只从 Script Lock 提取视觉实体与需求，建立 DRAFT 清单；不决定镜头、不生成图片。

## 执行

1. Read `modules/asset-taxonomy.md` 与 Script 中相关段落。
2. 逐项登记角色、角色状态/服装、场景、区域、关键道具及跨场连续性依赖。
3. 分配稳定 ID，记录 Script evidence anchor、必需/可选、首次出现与依赖。
4. 将已选现有资产按 `REUSE_CANDIDATE` 登记；此时只候选，不提前判 READY。
5. 检查 coverage：每个具象 Script 实体恰有清单项；抽象叙事概念不得伪装成实体。

## 输出 schema

使用 `templates/asset-manifest-template.yaml`，落盘：

- `{project_path}/stage-outputs/04_visual_bible/asset_manifest_DRAFT.yaml`
- 更新 `{project_path}/00_project_state.md`

每项至少含 `asset_id/type/name/script_evidence/required/status/dependencies/source`。

## Gate

P1 是 AUTO coverage Gate；有遗漏、重复 ID 或无证据实体则保持 DRAFT 并修正。

即使结果明确，适用的 Hard Gate 未满足也不允许自动推进。

```
╭─ Visual Bible · P1 完成 ─────────────────╮
│ 角色/场景/道具：{C}/{S}/{P}
│ Script coverage：{PASS|FAIL}
│ 产出：asset_manifest_DRAFT.yaml
│ 下一步：P2 风格与身份锚
╰───────────────────────────────────────╯
```

## 反模式

- 不凭常识新增角色；不把同一实体随意拆成多个 ID；不遗漏服装/状态变化；不把 URL 当资产。

---
*P1 完成后加载 `stages/02-style-and-identity-anchors.md`。*
