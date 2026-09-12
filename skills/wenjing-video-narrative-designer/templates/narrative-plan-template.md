# Narrative Plan · {{project_id}}

## 1. Contract Header

```yaml
schema_version: narrative-plan/v0.2
project_id: "{{project_id}}"
status: "DRAFT | LOCKED"
version: "{{version}}"
source_draft_path: "{{path_or_empty}}"
upstream_truth_lock:
  path: "stage-outputs/01_case_truth_lock_LOCKED.md"
  version: "{{truth_version}}"
  sha256: "{{manifest_registered_value}}"
approval_source: "PENDING | USER | APPROVED_BY_POLICY"
approved_at: ""
```

## 2. Narrative Brief

```yaml
audience: ""
teaching_goal: ""
knowledge_ids: []
content_route: CASE
control_mode: "FAST | GUIDED | STRICT"
platforms: []
duration_constraint: ""
target_emotion: ""
pending_fields: []
blockers: []
```

## 3. Truth & Boundary Inheritance

```yaml
fact_ids: []
knowledge_ids: []
allowed_refs: []
conditional_refs:
  - {boundary_id: "", decision_id: ""}
forbidden_refs: []
inheritance_note: "All items are read-only."
```

## 4. Reference Analysis Provenance（可选）

```yaml
reference_analysis_refs: []
# 非空时每项：
# - reference_id: REF-001
#   path: stage-outputs/00_reference_analysis/REF-001_LOCKED.md
#   artifact_version: 0.1.0
#   sha256: ""
#   input_modality: TRANSCRIPT_ONLY | VIDEO | FRAMES_AUDIO | MIXED
#   analysis_scope: []
#   adoption_intent: OPTIONAL | REQUIRED

adopted_transfer_rule_ids: []
# 非空时每项：
# - transfer_rule_id: TR-001
#   applied_to: [HOOK-01, NOD_02]
#   adaptation_summary: ""
#   truth_lock_check: PASS
#   project_constraint_check: PASS
#   originality_check: PASS
```

未使用 Reference Analysis 时两个数组保持空；不影响标准 CASE 合规。

## 5. Strategy Options

| strategy_id | strategy_name | hook_promise | fact/knowledge refs | participation | emotion path | payoff | advantage | tradeoff | boundary risk | transfer rules |
|---|---|---|---|---|---|---|---|---|---|---|
| STR-A |  |  |  |  |  |  |  |  |  |  |
| STR-B |  |  |  |  |  |  |  |  |  |  |

## 6. Selected Narrative Strategy

```yaml
selected_strategy_id: ""
decision_source: "USER | APPROVED_BY_POLICY"
decision_id: ""
selection_reason: ""
rejected_options_and_reasons: []
```

## 7. Hook Promise & Payoff Map

| hook_id | promise | fact_refs | knowledge_refs | required_payoff_function | payoff_node_ids | risk | status |
|---|---|---|---|---|---|---|---|
| HOOK-01 |  |  |  |  |  |  | PENDING |

## 8. Participation Mechanisms

| participation_id | type | audience_action | node_id | teaching_link | payoff_visibility | safety_notes | transfer_rule_refs |
|---|---|---|---|---|---|---|---|
| PAR-01 |  |  |  |  |  |  |  |

## 9. Narrative Nodes

| node_id | narrative_function | entry_state | content_summary | exit_state | fact_refs | knowledge_refs | boundary_class | conditional_decision_id | hook_payoff_role | downstream_writing_task | transfer_rule_refs | adaptation_summary |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| NOD_01 |  |  |  |  |  |  |  |  |  |  |  |  |

## 10. Emotion, Reaction & Knowledge Map

### Emotion / Reaction / Reflection Beats

| beat_id | node_id | emotion_label | relative_intensity | change_trigger | beat_function | boundary_notes | transfer_rule_refs |
|---|---|---|---|---|---|---|---|
| BEAT-01 |  |  |  |  |  |  |  |

### Knowledge Embedding

| knowledge_id | fact_refs | node_id | narrative_vehicle | audience_learning_action | do_not_say_as_fact |
|---|---|---|---|---|---|
| KP-01 |  |  |  |  |  |

## 11. Boundary / Reference Audit & Review Summary

```yaml
review_status: "PENDING | READY_FOR_APPROVAL | REVIEW_REQUIRED | BLOCKED"
truth_integrity: "PENDING"
forbidden_hits: 0
unresolved_conditionals: 0
unanchored_core_nodes: 0
unpaid_hooks: 0
knowledge_coverage: "0%"
emotion_alignment: "PENDING"
role_boundary: "PENDING"
reference_gates:
  input_modality: "N/A | PASS | REVIEW | BLOCK"
  observability: "N/A | PASS | REVIEW | BLOCK"
  originality: "N/A | PASS | REVIEW | BLOCK"
  adoption: "N/A | PASS | REVIEW | BLOCK"
issues: []
```

## 12. Decision, Approval & Downstream Handoff

### Decision Log

| decision_id | station | question | options | selection | source | decided_at |
|---|---|---|---|---|---|---|

### Approval Log

| gate | status | approved_by/source | approved_at | version_seen | note |
|---|---|---|---|---|---|

### Downstream Handoff

```yaml
next_skill: wenjing-video-script-studio
required_inputs:
  - stage-outputs/01_case_truth_lock_LOCKED.md
  - stage-outputs/02_narrative_plan_LOCKED.md
immutable_sections:
  - Truth & Boundary Inheritance
  - Selected Narrative Strategy
  - Hook Promise & Payoff Map
  - Narrative Nodes
  - Emotion, Reaction & Knowledge Map
  - Boundary / Reference Audit
reference_analysis_direct_dependency: false
handoff_status: "PENDING | READY"
```

> LOCKED 文件冻结后，整文件 SHA-256 只登记到 manifest/state，不写回本文件。
