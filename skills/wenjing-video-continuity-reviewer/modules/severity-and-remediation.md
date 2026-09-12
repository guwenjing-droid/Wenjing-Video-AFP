# Severity & Remediation

- GREEN：所有 required checks PASS，无开放 blocker。
- DRY_RUN_GREEN：规格、合同、覆盖和参数计划 PASS，只允许 DRY_RUN。
- MOCK_PASS / MOCK_FAIL：只表示模拟工程控制结果通过/失败，不是媒体质量结论。
- YELLOW：人工歧义、required 证据不足、可接受性需用户判断；不得进入自动生成。
- RED：事实/Dialogue/关键身份/资产/空间/参数、安全边界或契约失败。

owner routing：Script 内容→script-studio；canonical asset/spec→visual-bible；shot/continuity plan→storyboard-director；Prompt/参数/单次生成/Mock 状态→seedance-producer；用户内容方向→人工。

每 issue 记录最小 affected shots/assets/prompts/batch 与 `retest_from`。只在根依赖失效时扩大范围；Reviewer 不执行修复或重跑。
