# Change Request · {{cr_id}}

```yaml
cr_id: "{{cr_id}}"
status: "OPEN | APPROVED | REJECTED | IMPLEMENTED"
requested_at: "{{iso_datetime}}"
requested_by: "{{user_or_policy}}"
target:
  artifact_path: ""
  artifact_version: ""
  registered_sha256: ""
reason: ""
requested_change: ""
affected_objects:
  fact_ids: []
  knowledge_ids: []
  narrative_node_ids: []
  reference_ids: []
  transfer_rule_ids: []
impact:
  earliest_rerun_station: ""
  stale_artifacts: []
  downstream_skills_to_notify: []
decision:
  outcome: "PENDING"
  decided_by: ""
  decided_at: ""
  note: ""
implementation:
  new_version: ""
  replacement_artifact_path: ""
  completed_at: ""
```

## 影响说明

- 为什么不能通过修改未锁字段解决：{{...}}
- 对 Truth Lock / 用户约束 / Reference Analysis 优先级的影响：{{...}}
- 需要重新通过的 Gate：{{...}}
- 不受影响、禁止返工的部分：{{...}}

> 禁止原地覆盖 LOCKED；批准后创建新 Draft/版本，旧 LOCKED 保留。
