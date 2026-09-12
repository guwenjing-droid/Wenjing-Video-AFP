# Reference Analysis · {{reference_id}}

## 1. Contract Header

```yaml
project_id: ""
reference_id: ""
contract_version: "reference-analysis/0.1"
artifact_version: "0.1.0"
status: "DRAFT | LOCKED"
source_paths: []
input_modality: "TRANSCRIPT_ONLY | VIDEO | FRAMES_AUDIO | MIXED"
observed_materials: {}
missing_modalities: []
analysis_scope: []
approval: {actor: "", method: "", approved_at: ""}
```

## 2. Content Intelligence

### Audience
### Core Thesis
### Information Hierarchy & Logic Chain
### Facts, Arguments, Data, Cases & Policies
### Domain / Industry Links

## 3. Narrative Reverse Engineering

### Hook / Setup / Escalation / Turning Point / Payoff / Ending
### Structural Transitions
### Emotional Progression

## 4. Engagement Engineering

### Opening / First 3 Seconds (only when timecoded)
### Curiosity, Conflict, Resonance, Contrast, Humor, Suspense, Healing
### Retention Candidates & Interaction Incentives

## 5. Audiovisual Grammar

`analysis_status: OBSERVED | PARTIAL | NOT_OBSERVABLE`

### Shot / Composition / Camera / Duration
### Action & Blocking
### Subtitle / Music / SFX / Transition
### Color / Lighting / Visual Style

## 6. Transfer Engine

```yaml
transfer_rules:
  - transfer_rule_id: "TR-001"
    mechanism: ""
    source_layer: "content | narrative | engagement | audiovisual"
    observable_basis: []
    confidence: "high | medium | low"
    transferable_to: ["narrative"]
    source_specific_elements: []
    do_not_copy: []
    originality_risk: "low | medium | high"
    conditions: []
    gate_status: "PASS | REVIEW | EXCLUDED"
```

## 7. Evidence Anchors

| anchor_id | source | locator | supports | status |
|---|---|---|---|---|

## 8. Objectivity & Limitations

### Position / Completeness / Timeliness / Sample
### Reasoning Gaps
### Missing Modalities & Anchor Limits
### Applicable / Inapplicable Scenarios

## 9. External Supplements

`status: NONE | PRESENT`

| source | published/accessed | verified | relation to observed analysis |
|---|---|---|---|

