# Video Project State · {{project_id}}

> 本文件用于断点恢复；实质内容以 `stage-outputs/` 中的具名产物为准。

```json
{
  "pipeline_version": "0.2",
  "project_id": "{{project_id}}",
  "content_route": "CASE",
  "control_mode": "GUIDED",
  "current_station": "P0",
  "next_station": "P1",
  "stage_status": {
    "case_planner.P0": "ACTIVE",
    "case_planner.P1": "LOCKED",
    "case_planner.P2": "LOCKED",
    "case_planner.P3": "LOCKED",
    "case_planner.P4": "LOCKED",
    "case_planner.P5": "LOCKED",
    "case_planner.P6": "LOCKED"
  },
  "gate_status": {
    "truth_audit": "PENDING",
    "teaching_direction": "PENDING",
    "final_lock": "PENDING"
  },
  "source_registry": {
    "count": 0,
    "unresolved": 0
  },
  "artifact_registry": [
    {
      "artifact_id": "case-truth-lock",
      "artifact_type": "case_truth_lock",
      "version": "",
      "status": "MISSING",
      "content_ref": "stage-outputs/01_case_truth_lock_LOCKED.md",
      "storage_backend": "LOCAL_FILE",
      "sha256": "",
      "integrity_status": "DEFERRED",
      "upstream_refs": [],
      "upstream_integrity": [],
      "approved_by": "",
      "updated_at": ""
    }
  ],
  "locked_artifacts": [],
  "stale_artifacts": [],
  "user_decisions": [],
  "open_change_requests": [],
  "current_blocker": "",
  "resume_prompt": "",
  "updated_at": "{{iso_datetime}}"
}
```

## Asset Snapshot

| Asset | Absolute path | Status | Version/hash | Note |
|---|---|---|---|---|
| manifest | {{...}} | READY / MISSING / STALE / BLOCKED | {{...}} | {{...}} |
| case truth draft | {{...}} | {{...}} | {{...}} | {{...}} |
| case truth locked | {{...}} | {{...}} | {{...}} | {{...}} |

## Resume Note

- Last confirmed decision: {{...}}
- Current blocker: {{none_or_description}}
- Next safe action: {{...}}
- Do not repeat: {{already_confirmed_items}}
