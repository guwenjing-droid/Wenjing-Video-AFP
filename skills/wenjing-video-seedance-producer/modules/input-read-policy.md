# Input Read Policy

## 最小闭包

1. Manifest/state 的当前路线、control mode、scope、cost policy。
2. `05_storyboard_LOCKED.json` 中当前 shot 与 continuity neighbors。
3. Storyboard 对应的 Script 引用；只有核对 Dialogue Lock 时读取相关段落。
4. 仅当 Storyboard 选择 Visual Bible 时，读取相关 asset manifest 行和被引用文件。
5. 真实模式读取当前有效 GREEN PREFLIGHT；DRY_RUN 可读取仅放行 DRY_RUN 的 DRY_RUN_GREEN。两者都校验 input hashes。
6. 当前 capability profile。

## 禁止默认加载

不默认读取全部历史 Prompt、旧 Skill、所有分镜、全部素材库、Reference Analysis 或已跳过的 Skill。历史资产只在施工期提炼方法，不是运行时依赖。

## 复用

真实轨资产 path/version/sha256/readiness 均合法且无开放 CR 时标记 `REUSE`。Dry Run 轨只读取 `planned_asset_refs` 和规格路径，真实 reference array 必须为空。Producer 不重新生成视觉资产。
