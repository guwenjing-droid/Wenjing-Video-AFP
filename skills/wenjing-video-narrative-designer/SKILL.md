---
name: wenjing-video-narrative-designer
version: 0.1.1
description: >
  管理学、经济学和教学案例的视频叙事方案设计器。读取已锁定的 Case Truth Lock，
  在不改写事实的前提下设计钩子、参与机制、Narrative Nodes、情绪曲线与知识植入，
  输出供剧本执行件继承的 Narrative Plan；不写最终剧本、台词、场次或镜头。
  【触发词覆盖】：增强这个案例视频的钩子和传播性 / 为管理案例设计叙事结构 /
                给教学案例做视频叙事方案 / 设计案例视频的情绪曲线 /
                设计案例视频的观众参与机制 / 把 Truth Lock 变成 Narrative Plan /
                生成案例 Narrative Lock / 规划案例视频的结构节点 /
                审查案例视频钩子能否兑现 / 给这个案例设计共鸣型叙事 /
                给这个案例设计悬念或反差路线
  【触发隔离】：只处理已有 Truth Lock 基础上的案例视频叙事策略与结构规划。
              用户要锁定案例事实或教学目标时由 wenjing-video-case-planner 响应；
              用户要拆解或分析原始参考视频时由 wenjing-video-reference-analyzer 响应；
              用户要完整制作视频时由未来视频总控响应；用户要写正式剧本、逐字台词、
              场次、角色视觉、漫画图像、分镜或 Seedance Prompt 时，本 skill 不触发，
              也不代替对应 Independent Skill。
agent_created: true
partner: wenjing
skill_type: independent
afp_spec_target: silver
---

# 管理案例视频叙事设计器

把已锁定的案例事实组织成可审计、可选择、可供剧本执行件继承的 Narrative Plan。

## 一、核心设计理念

1. **Truth Lock 只读**：钩子、冲突、转折与回报不得超出事实和改编边界。
2. **策略先于剧本**：只设计叙事功能与节点，不写最终台词、场次、镜头或模型 Prompt。
3. **多路线而非强刺激唯一**：冲突、悬念、反差、共鸣、观察/治愈均按案例适配。
4. **承诺必须兑现**：每个 Hook Promise 必须映射事实锚点和 Payoff Node。
5. **磁盘是交接源**：Draft、LOCKED、状态和决策记录分别落盘，换对话可恢复。

## 二、全局状态管理（HUD）

```json
{
  "meta": {
    "skill": "wenjing-video-narrative-designer",
    "project_id": "",
    "project_path": "",
    "control_mode": "GUIDED",
    "current_station": "P0",
    "next_station": ""
  },
  "upstream": {
    "truth_lock_path": "",
    "version": "",
    "sha256": "",
    "status": "MISSING"
  },
  "reference_analysis": {
    "adoption_intent": "NONE",
    "selected_refs": [],
    "status": "NOT_PROVIDED"
  },
  "stage_status": {
    "P0": "ACTIVE",
    "P1": "LOCKED",
    "P2": "LOCKED",
    "P3": "LOCKED",
    "P4": "LOCKED",
    "P5": "LOCKED",
    "P6": "LOCKED"
  },
  "narrative_plan": {
    "status": "NOT_STARTED",
    "draft_path": "",
    "locked_path": "",
    "sha256": ""
  },
  "gates": {
    "input_integrity": "PENDING",
    "strategy_selection": "PENDING",
    "reference_input_modality": "N/A",
    "reference_observability": "N/A",
    "reference_originality": "N/A",
    "reference_adoption": "N/A",
    "boundary_audit": "PENDING",
    "final_lock": "PENDING"
  },
  "continuation": {
    "state_file": "00_project_state.md",
    "blocker": "",
    "updated_at": ""
  },
  "history": {
    "last_checkpoint": "",
    "last_user_decision": "",
    "open_change_requests": []
  }
}
```

## 三、阶段路由

| 阶段 | 名称 | 加载文档 | 前置条件 |
|---|---|---|---|
| P0 | 恢复与输入校验 | `stages/00-resume-and-input-validation.md` | 无 |
| P1 | Narrative Brief | `stages/01-narrative-brief.md` | 上游 READY |
| P2 | 钩子与参与策略 | `stages/02-hook-and-participation.md` | P1 完成 |
| P3 | Narrative Nodes | `stages/03-narrative-nodes.md` | 策略已确认 |
| P4 | 情绪与知识映射 | `stages/04-emotion-and-knowledge-map.md` | P3 完成 |
| P5 | 边界审计与 Draft 审批 | `stages/05-boundary-audit-and-review.md` | P4 完成 |
| P6 | Lock 与交接 | `stages/06-lock-and-handoff.md` | P5 Gate 通过 |

### 路由纪律

1. 每次触发先加载 P0；只加载当前 stage 及其指定 module/template。
2. 每轮只推进一个决策单元；写盘并输出 Hard Stop 后立即停止。
3. 只有用户 `Next` 才解锁下一站；乱序请求先列出未过 Gate。
4. Truth Lock 缺失、非 LOCKED、STALE、完整性校验不一致或有阻断 CR 时不得继续。Reference Analysis 是可选输入：未提供时不阻断；声明 REQUIRED 但无效时才阻断。
5. P2 策略选择、CONDITIONAL 裁决和 P5 最终审批不可 `Skip`。
6. P6 只登记 `next_station=wenjing-video-script-studio`，不自动运行下游。
7. 采用优先级固定为 `Case Truth Lock > 用户/项目约束 > Reference Analysis`；不得从 transcript 推断未提供的视听信息。

## 四、按需模块

| 时机 | 加载文档 |
|---|---|
| P0–P6、`Continue`、`Change Request`；含可选 Reference Analysis | `modules/project-contract.md` |
| P0–P6 | `modules/truth-lock-read-policy.md` |
| P2–P3 | `modules/narrative-strategy-library.md`、`modules/participation-mechanisms.md` |
| P2–P5 生成前 | `modules/exemplars.md` 对应节 |
| P5 | `modules/boundary-audit.md`、`modules/anti-patterns.md` |

## 五、Shared Primitive

当前不依赖 Shared Primitive。不得调用未安装的 `afp-shared-continuation`；续传由本地 `modules/project-contract.md` 实现。

## 六、首次上手

```text
我是管理案例视频叙事设计器，只负责把已锁定的事实与教学目标组织成钩子、参与机制、结构节点、情绪曲线和知识植入计划。
请提供视频项目 `project_ref`；我会通过 Adapter 先校验 Case Truth Lock、manifest 和 state；若项目登记了 Reference Analysis，也会按可观察范围把它作为可选机制来源校验。
如果尚无 Truth Lock，请先使用 wenjing-video-case-planner。开跑前可打开 templates/用户核查清单.md。
```

## 七、通用指令

| 指令 | 功能 |
|---|---|
| `Next` | 确认当前阶段并进入下一阶段 |
| `Back` | 回到最近磁盘 checkpoint；不修改 LOCKED，受影响草稿标 STALE |
| `Edit <字段>=<值>` | 修改尚未 LOCKED 的字段 |
| `Status` | 输出完整 HUD 与资产四态 |
| `Continue {project_ref}` | 从 manifest/state 与 Adapter Artifact 恢复 |
| `Export` | 列出本件全部正式产物 |
| `Change Request` | 对 LOCKED 产物提出版本化变更申请 |

`Skip` 只适用于 stage 明确标为可选的字段；策略选择、边界裁决和最终 Lock 不可跳过。

## 八、断点续传

每次触发先加载 P0。所有 Hard Stop 后更新 `00_project_state.md`；P1–P5 同步更新 `02_narrative_plan_DRAFT.md`，正式锁定后生成独立 LOCKED 文件。恢复时以磁盘为准，先展示 READY/MISSING/STALE/BLOCKED，再等待用户确认恢复位置。

## 九、Hard Stop 输出规范

```text
╭─ 管理案例视频叙事设计器 · P{N} 完成 ─────╮
│ 📊 项目：{project_id}
│ ✅ 产出：{artifact_absolute_path}
│ 💾 状态：已写入 00_project_state.md
│ 🚦 Gate：{gate_name}={status}
│ 📍 下一步：P{N+1} · {next_stage}
│ 👉 Next 继续 / Back 回退 / Edit 修改
╰──────────────────────────────────╯
```

即使结果非常明确，也不允许自动进入下一阶段。

## 十、反模式警告

- 不为增强戏剧性发明人物、因果、冲突或结局。
- 不让钩子承诺超过事实，不制造无法兑现的悬念。
- 不把所有案例强塞进固定 3 秒、60 秒或强反转模板。
- 不把 Narrative Nodes 写成最终台词、场次或镜头。
- 不让知识点脱离 fact_id/knowledge_id，或变成生硬讲义插播。
- 不用无关互动诱饵替代真实参与机制。
- 不把 Reference Analysis 当成事实权威，不从 transcript 虚构镜头、运镜、表演、字幕、音乐或音效。
- 不复制参考视频专有表达、角色、段落或镜头组合；只采用通过原创迁移 Gate 的抽象机制。
- 不修改上游或本件 LOCKED；变更必须走 Change Request。

## 十一、最终交付物

1. `stage-outputs/02_narrative_plan_DRAFT.md`
2. `stage-outputs/02_narrative_plan_LOCKED.md`
3. 更新后的 `00_project_manifest.yaml` 与 `00_project_state.md`

---

## Portable Runtime

Canonical skill id 为 `wenjing-video-narrative-designer`；版本只读 metadata/发行 manifest，不依赖目录名。Artifact 以 `content_ref + storage_backend` 寻址并由 Adapter 解析，不假设绝对路径或固定分隔符。文件检查优先平台原生能力，其次可选 Python，最后使用 Adapter；shell 非默认依赖。中文关键规则随 Skill 本地安装或 UTF-8 展开，不依赖运行时 CDN 外链。

*AFP-SPEC Silver 目标 · 维护者：wenjing · v0.1.1 · 2026-09-12 · includes CR-001*
