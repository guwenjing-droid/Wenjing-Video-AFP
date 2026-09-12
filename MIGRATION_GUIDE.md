# Migration Guide

## A. 原生支持 Skill 包的平台

1. 找到平台配置的 Skill 根目录。
2. 把本包 `skills/` 下的每个目录原样复制为根目录的直接子目录。
3. 确认每个子目录包含 `SKILL.md`，并允许读取其相对引用的 `stages/`、`modules/` 和 `templates/`。
4. 触发平台重新扫描；若平台只在启动时索引，重启应用或新开会话。
5. 用清单查询或一次无副作用的 Dry Run 验证 12 个 canonical 名称均可调用；名称不得带版本后缀。
6. 为项目工作目录配置写权限；Skills 安装目录可保持只读。
7. 选择 [Local File Adapter](runtime/local-file-adapter.md)；若没有文件系统，改用 Document/Board Adapter，不修改业务 Skill。

不要把整个 `skills/` 目录嵌套成一个单独 Skill，也不要合并多个 `SKILL.md`。平台路径和刷新细节见对应 adapter。

## B. 不兼容 AFP/Codex Skill 格式的平台

`SKILL.md` 不是必须照搬安装的 Codex 插件文件，而是可迁移的业务规格。目标平台应读取整个发行包，并保留其中的：

- 职责定义与禁止越界事项；
- 方法和阶段定义；
- 输入输出与 Artifact Contract；
- Hard / Review / Auto Gate；
- DRAFT / APPROVED / LOCKED 生命周期；
- State、检查点、失败传播和恢复规则；
- Orchestrator 路由及 Independent Skill 接棒关系。

| 发行包概念 | 目标平台映射 |
|---|---|
| Independent Skill | 独立 Agent、Workflow 节点或受约束 Prompt |
| Orchestrator | Router Agent 或主 Workflow |
| Artifact | Board 卡片、文档、结构化记录或对象存储条目 |
| Artifact Contract | Schema、模板与节点输入输出约束 |
| Gate | 人工审批节点、条件分支或自动校验器 |
| State | Board 字段、数据库记录或 Workflow checkpoint |
| LOCKED | 不可静默修改的版本化状态 |
| restart/resume | 从最后合法 checkpoint 重启节点 |
| `content_ref` | 文件逻辑路径、document_id 或 object_ref |
| `storage_backend` | Local File 或 Document/Board 运行实现 |

### 推荐迁移顺序

1. 导入 [contracts](contracts/) 与 [runtime](runtime/)；先建立 Artifact/State 数据模型和 Adapter。
2. 建立四条入口和三项通用下游执行件。
3. 建立 Reviewer 双模式与 Producer 的 Dry Run。
4. 建立薄 Orchestrator 路由；不要把各 Skill 的方法重新塞入总控。
5. 用 [examples](examples/) 做无成本接棒、失败、局部重跑和恢复测试。
6. 真实媒体生成应作为单独授权的后端接入阶段。

## 迁移验收

迁移完成至少应证明：四条主路线能产生兼容 Script LOCKED；可选 Reference Analysis 不覆盖高优先级真值；LOCKED 变更会使下游 STALE；Local File 可完成 hash 验证；无 hash 的 Document/Board 明确 `NOT_OBSERVABLE`；报告不覆盖历史；Dry Run 不触发外部媒体调用；Orchestrator 只路由且可从最后合法状态恢复。
