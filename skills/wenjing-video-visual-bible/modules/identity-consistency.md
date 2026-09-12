# Identity & Style Consistency

## 全局 style spec

至少定义：媒介/渲染方式、时代与地域、写实度、形体语言、材质、色彩、光线、纹理、画幅适配、禁止项。分辨率标签不能替代风格定义。

## 身份锚

每个核心角色分两层：

- invariant：脸型与关键比例、年龄带、体型、发型/毛色、稳定标志特征；
- variant：服装、表情、姿势、时间状态、污损或剧情允许变化。

不得把一个角度的偶然细节升格为 invariant。身份锚需有文字 spec；实际 canonical file 存在且 hash 有效后才具备可消费性。

## 复用判定

同时通过 `identity_match + style_match + rights_ok + version_compatible + hash_valid + readiness_ready + no_open_CR` 才 REUSE。否则记录 REGENERATE/REVIEW 与具体原因。复用仅跳过生成，不跳过兼容审计。

## 冲突优先级

`Script Truth/Project constraints > approved identity anchors > historical examples`。历史样例只提供方法，不覆盖当前项目。
