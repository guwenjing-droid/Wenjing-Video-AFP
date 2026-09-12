# P0 · Resume & Modality Validation

> 只恢复状态、盘点材料并冻结本轮可观察范围；不开始五层分析。

## 执行

1. Read `modules/project-contract.md` 与 `modules/modality-observability-policy.md`。
2. 解析 `Continue {absolute_project_path}`；读取 manifest、state、reference manifest、LOCKED/DRAFT 和开放 CR。
3. 若项目壳不存在，按模板建立最小壳；不得伪造参考材料。
4. 为每个材料登记真实路径、可读性、时码/行号能力；确定 `TRANSCRIPT_ONLY | VIDEO | FRAMES_AUDIO | MIXED`。
5. 生成 observed/missing modalities 与 analysis_scope。声明与材料不一致为 BLOCK。
6. 创建或更新 `<reference_id>_DRAFT.md` 的 Contract Header，更新 state。

## 判断

- PASS：来源可定位，modality、observed/missing、scope 一致。
- REVIEW：材料可读但时间码、抽帧或音轨不完整；明确降级后可继续。
- BLOCK：路径不可读、来源不明，或声称观察未提供模态。

## 输出 schema 与落盘

`00_project_manifest.yaml`、`00_project_state.md`、`stage-outputs/00_reference_analysis/reference_analysis_manifest.yaml`、`<reference_id>_DRAFT.md` Header。

## Hard Stop

```text
╭─ Reference Analyzer · P0 完成 ─╮
│ reference_id / modality / scope
│ G-RA-01：PASS | REVIEW | BLOCK
│ 下一步：P1 Content Intelligence
│ NEXT：Next / Back / Edit / Status
╰──────────────────────────────╯
```

即使材料看起来完整，也不自动进入 P1。不得 Skip。

## 反模式

- 凭文件名猜模态；把摘要当 transcript；用描述替代实际视频；丢失 material path。

---
*P0 确认后加载 `stages/01-content-intelligence.md`。*
