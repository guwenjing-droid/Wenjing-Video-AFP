# Case Truth Lock · {{project_id}}

## 0. Document Metadata

| Field | Value |
|---|---|
| schema_version | `case-truth-lock/v0.2` |
| project_id | {{project_id}} |
| content_route | CASE |
| document_version | {{document_version}} |
| status | DRAFT / APPROVED / LOCKED |
| created_at | {{created_at}} |
| updated_at | {{updated_at}} |
| source_draft_path | {{source_draft_path_or_na}} |
| sha256_registry | manifest/state（LOCKED 文件本体不内嵌自身整文件 hash） |

> 本文件锁定案例事实、教学目标和视频改编边界。它不是叙事方案、正式剧本或分镜。

## 1. Source Registry

| source_id | source_type | title_or_description | absolute_path_or_url | version_or_date | role | access_status |
|---|---|---|---|---|---|---|
| SRC_001 | USER_FILE / USER_TEXT / PUBLIC_SOURCE / INTERNAL_NOTE | {{...}} | {{...}} | {{...}} | PRIMARY / SECONDARY / SUPPLEMENT | READY / UNREADABLE |

## 2. Final Fact Table

| fact_id | claim | source_id | source_anchor | classification | importance | confidence | lock_status |
|---|---|---|---|---|---|---|---|
| FACT_001 | {{单一、可核对的声明}} | SRC_001 | {{稳定定位}} | FACT | CORE / SUPPORTING / CONTEXT | HIGH / MEDIUM / LOW | DRAFT / LOCKED |

## 3. Interpretations

| interpretation_id | statement | interpreter | supporting_fact_ids | source_anchor | teaching_use |
|---|---|---|---|---|---|
| INT_001 | {{...}} | {{作者/受访者/教师}} | FACT_001 | {{...}} | {{...}} |

## 4. Inferences

| inference_id | inference | basis_fact_ids | reasoning | alternatives | permission |
|---|---|---|---|---|---|
| INF_001 | {{...}} | FACT_001 | {{...}} | {{...}} | DO_NOT_PRESENT_AS_FACT |

## 5. Unknowns and Unresolved Issues

### Unknowns

| unknown_id | missing_or_ambiguous_item | impact | downstream_rule |
|---|---|---|---|
| UNK_001 | {{...}} | HIGH / MEDIUM / LOW | {{不得如何使用}} |

### Unresolved Issues

| issue_id | related_ids | conflict_or_gap | options | user_decision | status |
|---|---|---|---|---|---|
| ISSUE_001 | FACT_001 / SRC_001 | {{...}} | A 保持未知 / B 补来源 / C 排除核心集 | {{pending}} | OPEN / RESOLVED |

### Excluded Claims

| claim | exclusion_reason | original_source | retained_for_audit |
|---|---|---|---|
| {{...}} | NO_ANCHOR / CONTRADICTED / OUT_OF_SCOPE | {{...}} | YES |

## 6. Target Audience and Teaching Goal

- Target audience: {{角色、已有知识、使用场景}}
- Teaching goal: 学习者完成后能够{{识别/比较/判断/解释/选择……}}
- Teaching direction decision ID: {{DECISION_ID}}
- Deferred teaching angles: {{...}}

## 7. Core Knowledge Points

> 限 1–3 个。

| knowledge_id | plain_language_definition | supporting_fact_ids | role | evidence_note |
|---|---|---|---|---|
| KP_01 | {{...}} | FACT_001 | PRIMARY / SUPPORTING | CASE_SUPPORTED / TEACHING_INTERPRETATION |

## 8. Fact–Knowledge Mapping

| knowledge_id | fact_ids | what_the_case_demonstrates | what_the_case_does_not_prove |
|---|---|---|---|
| KP_01 | FACT_001 | {{...}} | {{...}} |

## 9. Dramatization Space

### ALLOWED

| rule_id | allowed_action | protected_fact_ids | condition |
|---|---|---|---|
| ALLOW_01 | {{...}} | FACT_001 | {{...}} |

### CONDITIONAL

| rule_id | proposed_action | affected_ids | approval_condition | decision_id | status |
|---|---|---|---|---|---|
| COND_01 | {{...}} | FACT_001 | {{...}} | {{pending}} | PENDING / APPROVED / REJECTED |

### FORBIDDEN

| rule_id | forbidden_change | protected_ids | downstream_check |
|---|---|---|---|
| FORBID_01 | {{不得改变或发明的具体事项}} | FACT_001 / KP_01 | {{可机器检查的规则}} |

## 10. Forbidden Fabrication List

1. {{具体人物/关系/时间/行为/因果/数量/结局限制}}
2. {{...}}

## 11. Sensitivity and Anonymization Notes

| item | risk | required_action | approval_status |
|---|---|---|---|
| {{人物/组织/隐私/未成年人/声誉}} | HIGH / MEDIUM / LOW | {{匿名化/授权/保留未知}} | {{...}} |

## 12. Initial Narrative Mode Suggestions

> 只供 Narrative Designer 选路，不是最终叙事。

| option | mode | fit_with_teaching_goal | usable_fact_ids | risk | boundary |
|---|---|---|---|---|---|
| A | SCQA / 决策—后果 / 共鸣观察 / 对比复盘 | {{...}} | FACT_001 | {{...}} | {{...}} |

## 13. Consistency Declaration

- [ ] 核心事实均有 STRONG source anchor。
- [ ] FACT / INTERPRETATION / INFERENCE / UNKNOWN 已分开。
- [ ] 知识点为 1–3 个且均有事实映射。
- [ ] 未决问题没有被静默润色掉。
- [ ] 改编边界具体且可检查。
- [ ] 未混入最终叙事、剧本、视觉设定、分镜或模型 Prompt。
- External verification status: SOURCE_INTERNAL_PASS / EXTERNALLY_VERIFIED / UNVERIFIED_EXTERNALLY

## 14. Self-Audit and Remaining Risks

- Review status: READY_FOR_APPROVAL / REVIEW_REQUIRED / BLOCKED
- Remaining risks: {{...}}
- Required user decisions: {{...}}

## 15. Approval Log

| decision_id | stage | decision | decided_by | decided_at | affected_sections |
|---|---|---|---|---|---|
| DEC_001 | P3 / P4 / P5 | {{...}} | USER | {{...}} | {{...}} |

## 16. Downstream Handoff

- next_station: `wenjing-video-narrative-designer`
- formal_input: {{absolute_path_to_this_LOCKED_file}}
- required_reads: `00_project_manifest.yaml`, `00_project_state.md`, this LOCKED file
- immutable_sections: Final Fact Table, Teaching Goal, Core Knowledge Points, FORBIDDEN rules
- open_risks: {{...}}
- change_protocol: create `change-requests/CR-{id}.md`; do not edit this LOCKED file
