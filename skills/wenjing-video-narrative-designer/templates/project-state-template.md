# Video Project State · {{project_id}}

> 本文件用于断点恢复；实质内容以 `stage-outputs/` 中的具名产物为准。

```json
{
  "pipeline_version": "0.3",
  "project_id": "{{project_id}}",
  "content_route": "CASE",
  "control_mode": "GUIDED",
  "current_station": "P0",
  "next_station": "P1",
  "stage_status": {
    "narrative_designer.P0": "ACTIVE",
    "narrative_designer.P1": "NOT_STARTED",
    "narrative_designer.P2": "NOT_STARTED",
    "narrative_designer.P3": "NOT_STARTED",
    "narrative_designer.P4": "NOT_STARTED",
    "narrative_designer.P5": "NOT_STARTED",
    "narrative_designer.P6": "NOT_STARTED"
  },
  "gate_status": {
    "input_integrity": "PENDING",
    "narrative_brief": "PENDING",
    "strategy_selection": "PENDING",
    "reference_input_modality": "N/A",
    "reference_observability": "N/A",
    "reference_originality": "N/A",
    "reference_adoption": "N/A",
    "boundary_audit": "PENDING",
    "final_lock": "PENDING"
  },
  "upstream_truth_lock": {"path": "", "version": "", "sha256": "", "status": "MISSING"},
  "optional_reference_analysis": {"adoption_intent": "NONE", "selected": [], "status": "NOT_PROVIDED"},
  "narrative_plan": {"status": "NOT_STARTED", "draft_path": "", "locked_path": "", "version": "", "sha256": ""},
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

| Asset | Absolute path | Status | Version / integrity | Note |
|---|---|---|---|---|
| manifest | {{...}} | READY / MISSING / STALE / BLOCKED | {{...}} | {{...}} |
| Truth Lock | {{...}} | {{...}} | {{...}} | required |
| Reference Analysis | {{...}} | NOT_PROVIDED / AVAILABLE / EXCLUDED / REQUIRED_BUT_INVALID | {{...}} | optional |
| Narrative Draft | {{...}} | {{...}} | {{...}} | {{...}} |
| Narrative LOCKED | {{...}} | {{...}} | {{...}} | {{...}} |

## Resume Note

- Last confirmed decision: {{...}}
- Current blocker: {{none_or_description}}
- Next safe action: {{...}}
- Do not repeat: {{already_confirmed_items}}
