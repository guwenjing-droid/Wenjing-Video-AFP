# Project Manifest Schema

项目 manifest 是路由与恢复的稳定入口，推荐文件名为 `00_project_manifest.yaml`。

```yaml
schema_version: wenjing-video-project/0.8
project_id: example-001
title: Example
content_route: CASE # CASE | SOURCE_LOCKED | KNOWLEDGE | STORY
run_mode: DRY_RUN # DRY_RUN | REAL
guidance_mode: GUIDED # FAST | GUIDED | STRICT
runtime:
  adapter: LOCAL_FILE # LOCAL_FILE | DOCUMENT_BOARD
  project_ref: ./project
  text_encoding: UTF-8
  capabilities: {native_file_tools: true, python: true, shell: false, sha256: true}
constraints:
  duration_seconds: 60
  aspect_ratio: "9:16"
  language: zh-CN
reference_analysis:
  enabled: false
  artifact_id: null
media_policy:
  backend_preference: economical
  allowed_backends: [seedance]
  max_shots: 12
  external_generation_authorized: false
artifacts:
  example:
    artifact_id: example
    artifact_type: example_type
    version: 1.0.0
    status: LOCKED
    content_ref: stage-outputs/example_LOCKED.md
    storage_backend: LOCAL_FILE
    sha256: ""
    integrity_status: DEFERRED
    upstream_refs: []
    upstream_integrity: []
    approved_by: ""
    updated_at: ""
state_file: 00_project_state.md
```

## 必需字段

- `schema_version`、`project_id`、`content_route`、`run_mode`、`guidance_mode`、`runtime.project_ref`。
- `artifacts` 每项必须含 artifact id/type、version、status、content_ref、storage_backend、sha256、integrity_status、upstream refs/integrity、approved_by、updated_at。
- `reference_analysis` 只控制可选分支，不得把它变成四条主链的必经站。
- `media_policy` 必须把后端选择、镜头预算与真实生成授权分开。

## 兼容与扩展

平台可添加命名空间字段，但不得改变枚举语义。未知字段应保留；未知 schema major version 应 Hard Stop。Manifest 的写入必须原子化或具有等效事务保证。
