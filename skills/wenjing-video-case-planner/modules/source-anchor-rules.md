# Source Anchor 规则

> P1–P2 按需加载。目标：让读者能回到原材料核对 claim，而不是只看到“据资料显示”。

## 1. 最小记录

每个来源：

```text
source_id | source_type | title_or_description | absolute_path_or_url | version_or_date | access_status
```

每个 claim：

```text
fact_id | source_id | source_anchor | claim | classification | confidence
```

## 2. 各类材料锚点

### Markdown / TXT

优先：`文件名 > 标题层级 > 段落首句`。行号只有在读取工具能稳定给出时才使用。

示例：`SRC_001 | “项目转折”节 | 段落首句“第二季度开始……”`

### PDF

记录：页码 + 章节/表图编号 + 段落或短定位语。区分 PDF 页序与印刷页码；不确定时写明采用哪一种。

### DOCX

记录：标题层级 + 段落首句，或稳定表格名称/行列。若渲染页码可能变化，不把页码作为唯一锚点。

### Spreadsheet

记录：工作表名 + 单元格/区域 + 行记录键。示例：`Sheet=绩效数据; Range=B12:F12; Key=EMP_023`。

### 网页

记录：页面标题、直接 URL、页面日期（如有）、访问日期、标题/段落定位。搜索结果页不能作为最终来源。

### 用户粘贴文本

落盘原文后记录：`USER_TEXT_{NNN}` + 消息/会话时间 + 段落首句。不得只写“用户说”。

### 用户口述裁决

记录为 `USER_STATEMENT` 或 `USER_DECISION`，包含时间、裁决对象和原问题；它能解决项目决策，但不能自动证明现实事实。

## 3. Anchor 质量

- `STRONG`：读者可直接定位到支持该 claim 的具体位置。
- `WEAK`：只能定位到章节或长页面，需要人工搜索。
- `MISSING`：没有可复核位置。

核心事实必须 STRONG；WEAK 需要在 P2 标风险；MISSING 不得进入核心 Fact Table。

## 4. 引文纪律

- 优先忠实释义，必要时保留短摘录用于定位。
- 不为提高“证据感”复制大段原文。
- 不修正原文后再把修正版放进引号。
- 不编造页码、段落号、标题、URL 或访问日期。
- 文件更新后原 anchor 可能失效，必须记录版本或修改时间并重新核对。

## 5. 多来源与派生来源

- 同一事实有多个来源时分别列 anchor。
- 二手材料引用一手材料时，当前只读到二手材料就标 `SECONDARY`；不能假装已核对一手来源。
- 文件副本内容相同不算独立交叉验证。
- 外部核验新来源必须使用新的 source_id，不覆盖用户原材料身份。
