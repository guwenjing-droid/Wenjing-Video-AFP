# Video Project State · Portable Runtime v1.1

```json
{
  "pipeline_version": "0.8",
  "project_id": "",
  "project_ref": "",
  "storage_backend": "LOCAL_FILE",
  "content_route": "CASE",
  "control_mode": "GUIDED",
  "acceptance_profile": "V0_1_DRY_RUN",
  "current_station": "P0",
  "next_station": "P0",
  "required_skills": [],
  "available_skills": [],
  "missing_skills": [],
  "artifact_registry": [
    {
      "artifact_id": "",
      "artifact_type": "",
      "version": "",
      "status": "MISSING",
      "content_ref": "",
      "storage_backend": "LOCAL_FILE",
      "sha256": "",
      "integrity_status": "DEFERRED",
      "upstream_refs": [],
      "upstream_integrity": [],
      "approved_by": "",
      "updated_at": ""
    }
  ],
  "current_preflight_report_ref": "",
  "report_relations": [],
  "stale_artifacts": [],
  "open_change_requests": [],
  "current_blocker": "",
  "resume_prompt": "",
  "updated_at": ""
}
```

`integrity_status` 仅允许 `VERIFIED | NOT_OBSERVABLE | DEFERRED | FAIL`。Document/Board 无 SHA-256 能力时保留空 `sha256` 并写 `NOT_OBSERVABLE`。
