# Asset Taxonomy

## 类型与 ID

| 类型 | ID 前缀 | 例 |
|---|---|---|
| character | `CHR-` | `CHR-001` |
| character_state / wardrobe | `CST-` | `CST-001` |
| scene | `SCN-` | `SCN-001` |
| zone / spatial anchor | `ZON-` | `ZON-001` |
| prop | `PRP-` | `PRP-001` |
| style/pattern/recipe | `STY-`/`PAT-`/`RCP-` | `STY-001` |

ID 创建后不因改名改变。变体用 `parent_asset_id + variant_id`，不复制成无关系的新资产。

## 必填字段

`asset_id`、`type`、`canonical_name`、`required`、`script_evidence`、`dependencies`、`status`、`source`、`version`、`sha256`、`rights_status`、`file_paths`、`notes`。

## 盘点标准

- Script 中会被看见且需跨镜保持一致的实体必须登记。
- 群演/背景物只有影响叙事或连续性时才独立建项。
- required 由剧情和下游依赖决定，不因制作方便擅降为 optional。
- 可复用项先标 `REUSE_CANDIDATE`，通过 identity/style/rights/hash/readiness 检查后才 `READY`。
