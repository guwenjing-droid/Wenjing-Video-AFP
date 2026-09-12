# Change Request · {{request_id}}

| Field | Value |
|---|---|
| request_id | CR-{{YYYYMMDD}}-{{NNN}} |
| status | OPEN / APPROVED / REJECTED / APPLIED / CLOSED |
| requested_at | {{iso_datetime}} |
| requested_by | {{user_or_role}} |
| target_artifact | {{absolute_path}} |
| target_version | {{version}} |
| target_sha256 | {{hash}} |

## 1. Reason

{{为什么必须修改；新证据、事实错误、教学方向变化或边界变化。}}

## 2. Evidence

| source_id | source_anchor | what_it_changes |
|---|---|---|
| {{...}} | {{...}} | {{...}} |

## 3. Proposed Changes

| section_or_id | current_value | proposed_value | change_type |
|---|---|---|---|
| FACT_001 / KP_01 / FORBID_01 / section | {{...}} | {{...}} | FACT / TEACHING / BOUNDARY / METADATA |

## 4. Impact Analysis

- Affected downstream artifacts: {{...}}
- Artifacts to mark STALE: {{...}}
- Required rerun stages: {{...}}
- Cost/schedule risk: {{...}}
- If rejected: {{...}}

## 5. User Decision

| decision | decided_by | decided_at | rationale |
|---|---|---|---|
| APPROVE / REJECT / REQUEST_EDIT | USER | {{...}} | {{...}} |

## 6. Application Record

- New draft/version: {{...}}
- Old LOCKED retained at: {{...}}
- Rerun completed: {{...}}
- New LOCKED path/hash: {{...}}
- Closed at: {{...}}
