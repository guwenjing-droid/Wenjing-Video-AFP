# P0 · 模式与输入校验

## 边界
只确定 PREFLIGHT/POSTGEN/MOCK_POSTGEN 并校验锁、路径、版本和 hash，不开始质检。

## 执行
Read `modules/project-contract.md`、`modules/input-read-policy.md`。PREFLIGHT 必需 Script+Storyboard，按 manifest 条件需要 Visual Bible；POSTGEN 另需 generation manifest 与实际输出证据；MOCK_POSTGEN 需显式 Mock manifest/result。输入失效即 BLOCK；恢复时保留无关已锁报告。

## 输出 schema
更新 `{project_path}/00_project_state.md` 的 mode、input snapshot、selected paths、rerun scope、P0 Gate。

## Gate
```
╭─ Continuity Reviewer · P0 完成 ───────────╮
│ mode：{PREFLIGHT|POSTGEN|MOCK_POSTGEN} · inputs：{状态}
│ 下一步：P1 可观察性范围
╰───────────────────────────────────────╯
```
即使结果明确，适用 Hard Gate 未满足也不允许自动推进。

## 反模式
- 不猜 mode；不接受 DRAFT/STALE；不把 generation status 当实际媒体；不全库读取。

---
*P0 完成后加载 `stages/01-observability-and-evidence-scope.md`。*
