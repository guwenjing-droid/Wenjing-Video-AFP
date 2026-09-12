# Minimal CASE Example

这是结构示例，不是施工 run。用 `00_project_manifest.example.yaml` 启动 Orchestrator 后，应按 CASE 最短合法路径产出 Case Truth、Narrative Plan、Script LOCKED，再进入通用下游。所有媒体步骤保持 DRY_RUN。

验收重点：事实不可被参考风格覆盖；每个 Script 节点可追溯；Producer 外部调用数为 0。
