---
name: buaa-marp-ppt
description: >
  Generate BUAA-themed Marp PPT from an outline file. Given any outline `.md`,
  the agent parses headings, selects one of 15 layouts per slide, fills HTML
  templates, and writes a complete, self-contained Marp markdown file.
  Supports 6 BUAA color themes and 15 layout templates (A–M + C‑split + Fglass).
  No external dependencies beyond the themes/ directory.
metadata:
  version: "5.1.0"
compatibility: Trae / Cursor / VS Code with Marp. Requires themes/ directory.
---

# BUAA Marp PPT Skill

Given **any** outline `.md`, produce a complete, self-contained Marp presentation.
No other input is needed — no example files, no project-specific paths.

---

## §0 大纲格式速览

一份大纲的结构如下（`#` `##` `###` 为 Markdown 标题层级）：

```
# 展示文稿总标题

## Slide 1: 封面
{主标题}
汇报人：{姓名}

## Slide 2: 目录
- 01 章节一
- 02 章节二

## Slide 3: 01 章节一          ← 过渡页（## 行有标签 = transition）
### 第一章：章节一

## Slide 4:
### 1.1 页面主标题——副标题     ← 正文页（### 含编号）
排版：纯文字                   ← 可选：自然语言布局提示
{正文内容 — 散文 / 列表 / 表格 / 图片}
```

**关键规则：**
- `#` — 文件总标题，仅出现一次
- `## Slide N: {可选标签}` — 分页标识。标签非空 → 过渡页；空标签 → 正文页
- `### {编号} 标题——副标题` — 正文页主标题。编号提取到 badge
- `####` — 同一编号拆多页的子页标记（编号沿用上级 `###`）
- `排版：{提示词}` — 可选的 NL 布局提示，见 §2 决策表
- `> 布局：X  |  class：xxx  |  密度：xxx` — 备选提示格式，同样生效

---

## §1 生成流水线

```
Step 0 — 写 YAML frontmatter：
  ---
  marp: true
  theme: {buaa|buaa-red|buaa-gold|buaa-dark|buaa-green|buaa-purple}
  paginate: false
  ---

Step 1 — 解析标题层级：
  #   → 全局文件标题
  ##  → 每页分界；标签非空 = 过渡页，标签空 = 正文页
  ### → 正文主标题；编号提取到 badge，标题文字放到 ## 行
  #### → 子页标记（同一编号拆多页）

Step 2 — 逐页匹配布局：
  先检查大纲中的 NL 触发词（"排版：xxx" / "布局：X" / "class：xxx"），
  命中则直接用；否则按优先级回退规则（§2 末尾）推断。

Step 3 — 从 layout-templates.md 复制对应的 body 内容模板，
  填入大纲中的文字、图片路径、表格数据。

Step 4 — 套用 §4 的页面外套（badge + heading + footer + page-num），
  将 Step 3 的 body 内容嵌入 `buaa-chapter__body` 容器。

Step 5 — 编号与组装：
  封面/目录/过渡页 → 无页码
  正文页 → 从 1 连续递增
  结尾页 → 最后页码
  单页 → 单数字；≥2 页 → X.Y；拆子页 → X.Y.Z（最多三级）

Step 6 — 命名输出文件：
  {outline-filename-stem}.md（去掉 "-outline" 后缀）
```

---

## §2 布局决策系统

### 2.1 决策优先级

按顺序匹配，命中即停：

1. 大纲显式标注（`排版：xxx` / `布局：X` / `class：xxx`）→ 直接用
2. 有图？→ A / F / I / K
3. 有流程图/框图关键词？→ G / H
4. 有表格？→ C / C‑split / D / E
5. 有嵌套列表或 strong+ul？→ B / J
6. 纯文字 → B

### 2.2 决策表

| NL 触发词 | 布局 | body class | 密度变量 |
|---|---|---|---|
| `纯文字` `文字段落` `散文` | **B**‑flow | `buaa-layout--flow` | `--text-p-size:26px; --text-p-line-height:2` |
| `居中`（带公式/表格） | **C** | `buaa-layout--center` | `--text-p-size:26px; --text-p-line-height:1.7` |
| `居中，双栏` `窄表格`（≤3列） | **C‑split** | `buaa-split--2 buaa-split--top` | `--text-size:22px; --text-line-height:1.8` |
| `双栏对比` `左右对比` | **D** | `buaa-split--2 buaa-split--top` | `--text-size:19px; --text-line-height:2.4` |
| `左文右图` `各半` `文左图右` | **A1** (split‑2) | `buaa-layout--center` + `buaa-split--2` | `--text-p-size:26px; --text-p-line-height:2` |
| `左图右文` `图左文右` | **A2** (A 对称) | 同 A1，交换 div 位置 | 同 A1 |
| `文三图七` | **A** + split‑1‑2 | `buaa-split--1-2` | `--text-p-size:26px; --text-p-line-height:2` |
| `图七文三` | **A** + split‑2‑1 | `buaa-split--2-1` | `--text-p-size:26px; --text-p-line-height:2` |
| `文上图下` + 技术图 | **F** | `buaa-layout--center` + `buaa-split-tb` | `--text-p-size:28px; --text-p-line-height:1.5-2` |
| `流程图` `步骤` | **G** | `buaa-layout--center` + buaa-flow-chart | `--fc-font-size:24px` |
| `系统框图` | **H** | `buaa-layout--center` + buaa-block-diagram | (见模板内变量) |
| `双图并排` + 图注 | **I** | `buaa-layout--flow` + img-pair | — |
| `双栏图文` `分栏图文` `图文双栏` `两列图文` | **L** | `buaa-layout--center` + split-2-top + strong+ul+hm-fig | `--text-p-size:24px; --text-p-line-height:1.8` |
| `三列图文` `三图并排` `三栏图文` | **M** | `buaa-layout--flow` + buaa-row-3 + strong+hm-fig | `--text-p-size:24px; --text-p-line-height:1.8` |
| `分类列表` `strong标题+列表` | **J** | `buaa-layout--flow` | `--text-size:22px; --text-line-height:2` |
| `满页大图` `纯大图` | **K** | `buaa-layout--center` + hm-fig | — |
| `居中表格` `居中混排含列表` | **E** | `buaa-layout--center` + text-block | `--text-p-size:26px; --text-p-line-height:1.7` |
| `毛玻璃卡片` `毛玻璃` | **Fglass** | `buaa-layout--flow` + buaa-am--fglass | `--text-size:22px; --text-line-height:1.8` |

### 2.3 密度变量速查

| 场景 | CSS 变量（通过 `section { }` 注入） | 默认值 |
|---|---|---|
| 段落 | `--text-p-size` · `--text-p-line-height` | 26px · 1.7 |
| 列表（原生 `1.` / `-`） | `--text-size` · `--text-line-height` · `--text-item-gap` | 24px · 1.8 · 8px |
| 代码块 `pre` | `--pre-font-size` · `--pre-font-family` · `--pre-bg` · `--pre-color` · `--pre-code-color` · `--pre-line-height` · `--pre-font-weight` · `--pre-padding` · `--pre-border-left` · `--pre-border-radius` · `--pre-border` · `--pre-margin` · `--pre-letter-spacing` | 22px · Cascadia Code · #f5f7fa · #333 · 回退 --pre-color · 1.6 · 400 · 20px 28px · 4px solid var(--buaa-primary) · 8px · 1px solid #d0d6e0 · 14px 0 · normal |
| 行内代码 | `--code-font-size` · `--code-color` | 0.9em · var(--buaa-primary) |
| 流程图 | `--fc-font-size` · `--arr-length` · `--line-width` · `--arr-color` | 24px · 30px · 2px · var(--buaa-primary) |

### 2.4 可用 scoped 选择器（安全列表）

全局 CSS 对以下元素**没有**高-specificity 规则，scoped 中可直接写选择器：

| 选择器 | 典型用途 |
|---|---|
| `ol` / `ol li` / `ol ul` / `ol ul li` | 有序列表密度 |
| `ul` / `ul li` | 无序列表密度 |
| `.buaa-callout` | 总结框样式 |
| `.buaa-text-block` / `.buaa-text-block ul` / `.buaa-text-block ul li` | 文本块内嵌列表 |
| `.buaa-split--2 > div > strong` | 分栏分类标题 |
| `.buaa-split--2 ol` / `.buaa-split--2 ol li` | 分栏内嵌列表 |
| `.buaa-split--2 ul` / `.buaa-split--2 ul li` | 分栏内嵌无序列表 |
| `.buaa-fig-row` | 栏内双图并排容器 |
| `.buaa-row-3` | 三列图文容器 |
| `.buaa-flow-chart` / `.buaa-flow-chart__arrow` | 流程图 |
| `.buaa-block-diagram` | 系统框图 |
| `.buaa-hm-fig` / `.buaa-hm-fig img` | 图片容器 |

**必须用 `section { --var:val }` 注入的选择器**（全局有高-specificity 规则）：
`pre`、`code`、`pre code`、`table`、`p`、`blockquote`

---

## §3 约束（20 条）

### 致命（违反崩溃）

1. `<style scoped>` 放在 `buaa-chapter__badge` **之前**，绝不在 `page-num` 之后
2. `.buaa-text-block` 内禁止 `<p>` — 裸写文字，Marp 自动生成
3. **列表优先 Markdown 原生** (`1.` / `-`) — 仅当列表嵌在 `<div>` 内时才用 HTML `<li>`+`<strong>`+`<i>x</i><sub>1</sub>`
4. 目录 `ul` 必须带完整 inline `style="position:absolute;left:730px;..."` — scoped 选择器对 ul 可用，但 inline style 更可靠
5. `$...$` ✅ 裸文本 / 原生列表 / `##` 标题 / `<div>` 内裸文本；❌ HTML `<li>` / `<td>` / `.buaa-hm-cap` → 用 `<i>x</i><sub>1</sub>`
6. 图注仅在大纲标注「图注：」时添加 — 不自行编造
7. `buaa-block-diagram` Hub 只在 `center` 出现一次
8. 封面必须有 `buaa-cover__date`

### 严重（影响正确性）

9. 大纲标题一字不改
10. 同一编号多页 → 自动细化为 X.Y.Z
11. `.adj-*` 仅作 CSS 注释占位，**不激活**为 class
12. 加粗：原生列表 / 裸文本 `**text**` ✅；HTML `<li>` / `<td>` 中用 `<strong>`
13. **Scoped 样式规则**：`pre` / `code` / `table` / `p` → 必须 `section { --var:val }`；`ol` / `ul` / `.buaa-callout` / `.buaa-hm-fig` 等 → 可用 scoped 选择器（见 §2.4 安全列表）。**为何 pre 选择器失效**：Marp `<style scoped>` 追加 `[data-marpit-scope]`，但全局 `section.buaa-chapter pre` specificity 更高且后加载，必然覆盖 scoped。CSS 变量通过继承穿透，不受 specificity 影响。
14. 图片：`<div class="buaa-hm-fig">` → 空行 → `<img>` → 空行 → `</div>`（前后空行防 `<p>` 包裹）
15. 正文区域内禁止 `---`（会被 Marp 解析为分页符而非分割线）；需要分割线用 `<hr>`

### 注意（影响质量）

16. 标题层级：`#` 仅总标题；`##` 仅 Slide N 分界；`###` 正文主标题；最多三级
17. 序号与标题分离：`###` 中的编号填入 badge；`##` 标题栏不出现序号
18. 图片 URL → 下载到 `figures/` → `.md` 中用相对路径 `./figures/xxx.png`
19. 图注紧跟图片，与图片同父容器、位于图片正下方
20. 双图并排用 `buaa-img-pair` + `buaa-hm-cap`，禁用 `buaa-img-gallery`（不兼容图注）

---

## §4 页面外套（skeleton）

以下 5 种页面外套在生成时**直接使用**，`{...}` 占位符填入实际内容。
正文外套的 `<div class="buaa-chapter__body">` 内嵌入 §2 决策表选定的布局模板。

### 封面
```html
<!-- _class: buaa-cover -->
<img class="buaa-cover__logo" src="./assets/logo.png">
# {主标题}
## {副标题，≤20字；无则去行}
<div class="buaa-cover__presenter">汇报人：{姓名}</div>
<div class="buaa-cover__date">{日期}</div>
<div class="buaa-cover__decor">BEIHANG UNIVERSITY</div>
```

### 目录
```html
<!-- _class: buaa-catalog -->
<style scoped>
ul { left: 730px !important; display: flex !important; flex-direction: column !important; gap: 28px !important; }
li { font-size: 24px !important; margin-bottom: 0 !important; }
</style>
<div class="buaa-catalog__title">目录</div><div class="buaa-catalog__line"></div><div class="buaa-catalog__eng">Contents</div>
<ul style="position:absolute;left:730px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:28px;list-style:none;z-index:2;padding:0;margin:0;">
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">{N}</span> {章名}</li>
</ul>
```

### 过渡页
```html
<!-- _class: buaa-transition -->
<div class="buaa-transition__num">{如 01}</div>
# {中文标题}
## {English Title}
```

### 正文外套（所有 A-K / C-split / Fglass 共用）
```html
<!-- _class: buaa-chapter -->
<style scoped>
/* 图片容器 */
.buaa-hm-fig { display: grid !important; place-items: center !important; }
.buaa-hm-fig img { max-width:{XX}% !important; max-height:100% !important; width:auto !important; height:auto !important; }
/* 段落密度 */
section { --text-p-size: {段落字号}; --text-p-line-height: {段落行高}; }
/* 有代码块时追加：
   section { --pre-font-size:XXpx; --pre-font-family:"..."; --pre-color:#...; --pre-line-height:X.X; }
   有列表时追加：
   section { --text-size:XXpx; --text-line-height:X.X; --text-item-gap:XXpx; }
   有流程图时追加：
   section { --fc-font-size:XXpx; --arr-length:XXpx; --arr-color:#...; }
*/
</style>
<div class="buaa-chapter__badge"><span>{编号}</span></div>
## {主标题}——{副标题}
<div class="buaa-chapter__body {布局类名}">
  <!-- 从 layout-templates.md 复制对应 body 模板填充 -->
</div>
<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

### 结尾
```html
<!-- _class: buaa-end -->
<div class="buaa-chapter__badge"><span>结语</span></div>
# 感谢您的观看与收听，敬请批评指正
## Q &amp; A
<!-- 可选：答辩信息区 -->
<div class="buaa-end__info">
  <p>答辩人：{姓名}</p>
  <p>参评项目：{项目名}</p>
  <p>时间：{日期}</p>
</div>
<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## §5 高级修饰符（Advanced Modifiers）

`buaa-am--*` 系列 class 可直接叠加在 `<!-- _class: buaa-chapter -->` 行或 body 容器上，无需额外 CSS。

### 5.1 字号缩放

| class | 效果 | 适用 |
|---|---|---|
| `buaa-am--tinytext` | 整页缩至 80% | 密集数据页 |
| `buaa-am--smalltext` | 整页缩至 90% | 较多内容页 |
| `buaa-am--largetext` | 整页放大至 115% | 强调展示页 |
| `buaa-am--hugetext` | 整页放大至 130% | 标题页 |

用法：`<!-- _class: buaa-chapter buaa-am--smalltext -->`

### 5.2 彩色引用块

叠加在 section 上，blockquote 自动着色：

| class | 颜色 |
|---|---|
| `buaa-am--bq-blue` | #004F9E 蓝 |
| `buaa-am--bq-red` | #dc3545 红 |
| `buaa-am--bq-green` | #28a745 绿 |
| `buaa-am--bq-purple` | #6f42c1 紫 |
| `buaa-am--bq-black` | #333 黑 |

### 5.3 特殊布局

| class | 说明 |
|---|---|
| `buaa-am--fglass` | 毛玻璃效果列表（白色背景 + 投影 + 非对称圆角），叠加在 body 容器上 |
| `buaa-am--navbar` | 顶部导航进度栏 |
| `buaa-am--footnote` | 脚注布局（CSS Grid 分区：正文 + 脚注） |
| `buaa-am--fixedtitle-a` / `b` | 固定标题栏（标题始终在顶部，内容区可滚动） |
| `buaa-am--trans` | 过渡页增强变体 |
| `buaa-am-card` | 增强卡片样式 |
| `buaa-am-icon-list` | 图标列表 |
| `buaa-am--caption` | 图片/表格题注样式 |

### 5.4 多栏列表

| class | 说明 |
|---|---|
| `buaa-am-cols2-ul--sq` / `--ci` | 两栏无序列表（方形/圆形序号） |
| `buaa-am-cols2-ol--sq` / `--ci` | 两栏有序列表（方形/圆形序号） |
| `buaa-am-col1-ol--sq` / `--ci` | 单栏有序列表（方形/圆形序号） |
| `buaa-am-col1-ul--sq` / `--ci` | 单栏无序列表（方形/圆形序号） |

用法：在 `buaa-chapter__body` 容器内嵌入 `<div class="buaa-am-cols2-ul--sq"><ul>...</ul></div>`

### 5.5 箭头尺寸

| class | 效果 |
|---|---|
| `buaa-arrow--sm` | 箭头缩小至 70% |
| `buaa-arrow--lg` | 箭头放大至 140% |

用法：加在流程图或系统框图的箭头 div 上，如 `<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--lg">`

### 5.6 图片尺寸修饰符

同一页中不同图片可能需要不同尺寸时，在 scoped 中定义 `.buaa-hm-fig--a` / `--b` / `--c` / `--d` 修饰符，叠加在 `<div class="buaa-hm-fig">` 上：

```css
.buaa-hm-fig--a img { max-height: 180px !important; max-width: 100% !important; }
.buaa-hm-fig--b img { max-height: 200px !important; max-width: 100% !important; }
```

用法：`<div class="buaa-hm-fig buaa-hm-fig--a"><img src="..."></div>`

---

## §6 主题切换

在 YAML frontmatter 中修改 `theme` 字段：

| theme | 主色 | 适用场景 |
|---|---|---|
| `buaa` | #004F9E 北航蓝 | 默认，日常汇报/答辩 |
| `buaa-red` | #C41230 北航红 | 庆典/党建/竞赛 |
| `buaa-gold` | #C49B2C 北航金 | 学术典礼/荣誉表彰 |
| `buaa-dark` | #1B2D55 深空蓝 | 科技感/深色场景 |
| `buaa-green` | #2E7D32 银杏绿 | 自然/环保/校园 |
| `buaa-purple` | #5C2D91 星空紫 | 创新/探索/太空 |

---

## §7 常见陷阱速查

| 错误 | 正确 | 原因 |
|---|---|---|
| `.text-block` 内用 `<p>` | 裸写文字 | `<p>` 阻断 KaTeX |
| HTML `<li>` 内写 `$...$` | 用原生列表或 `<i>x</i><sub>1</sub>` | HTML `<li>` 不经 KaTeX |
| `## 标题` 缺副标题 | `## 主标题——副标题` | 大纲给了就要用 |
| 目录 `ul` 无 inline style | 必须 `style="position:absolute;..."` | inline 最可靠 |
| 内容中用 `---` | 用 `<hr>` | `---` 是 Marp 分页符 |
| scoped 中 `pre { font-size }` | `section { --pre-font-size:22px }` | specificity 不足 |
| 单页 badge 写 X.Y | 单页 = 单数字 | 多页才细化 |
| 大纲写"感谢聆听" | 结尾用"感谢您的观看与收听，敬请批评指正" | "聆听"是谦词 |

---

> 13 套正文布局完整 HTML 模板见 `references/layout-templates.md`。
> 排版设计参考（字体、字号、颜色）见 `references/typography-design.md`。
