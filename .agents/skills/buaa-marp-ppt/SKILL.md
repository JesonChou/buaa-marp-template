---
name: buaa-marp-ppt
description: >
  Create, edit, and manage BUAA (Beihang University) themed Marp presentations.
  Self-contained v3: all layout templates inlined, zero file references, pure template-driven.
  Use when user asks for PPT/slides/presentation with BUAA/北航 theme,
  or mentions Marp, buaa-css, academic presentation, thesis defense.
  Supports 6 color themes (blue/red/gold/dark/green/purple) and 11 layout patterns (A-K).
metadata:
  version: "3.1.0"
compatibility: Designed for Trae/Cursor/VSCode with Marp. Requires themes/buaa.css.
---

# BUAA Marp PPT Skill

> 自包含设计：所有页面骨架和布局模板均已内置于本文档或 references/。仅需提供一份大纲 `.md` 文件即可生成完整 PPT。

## 页面结构

```
封面(buaa-cover) → 目录(buaa-catalog) → 过渡(buaa-transition) → 正文(buaa-chapter)×N → 结尾(buaa-end)
```

**页码规则**：封面/目录/过渡页无页码；正文从1递增；结尾页有页码。

**编号层级**：单页→数字(如`1`)；≥2页→X.Y；子节→X.Y.Z；最多3级禁四级。

---

## 16 条硬约束

### 致命级（违反即崩溃）

| # | 规则 |
|:---:|------|
| 1 | `<style scoped>` 放在 `buaa-chapter__badge` 之前，绝不可放在 `page-num` 后面 |
| 2 | `.buaa-text-block` 内禁止 `<p>` 标签。裸写文字，Marp 自动生成 `<p>`（支持 `$...$`） |
| 2.1 | **列表生成规则**：遇到大纲中有序/无序列表时，<br>**✅ 优先**：Markdown 原生语法 `1. ` / `- `（当列表是 body 容器的直接子元素时）<br>**❌ 禁止**：在可用原生语法时却用 HTML `<ol><li>` / `<ul><li>` 包装<br>**⚠️ 例外**：列表嵌入在 `<div>` 内（如 `buaa-split--2 > div`、`.buaa-text-block`）时，Marp 无法解析原生语法，只能用 HTML `<li>` + `<strong>`，公式用 `<i>x</i><sub>1</sub>` |
| 3 | 目录 `ul` 必须带完整 inline style（见下方骨架模板） |
| 4 | 公式 `$...$` 在两类上下文中行为不同：<br>**✅ 可用**：裸文本段落、Markdown 原生列表（`1. ` / `- ` / 嵌套 `- `）、`##` 标题<br>**❌ 不可用**：HTML `<li>` 标签、`<td>` 表格单元格、`.buaa-hm-cap` 图注 → 需用 `<i>x</i><sub>1</sub>` 替代 |
| 5 | 图注仅在大纲明确标注"图注："时添加。不自行为图片编造 `.buaa-hm-cap` |
| 6 | 生成 `.buaa-hm-cap` 时，去掉大纲中 `**图注：**` 标记本身，只保留后续的纯文本内容 |
| 7 | `buaa-block-diagram` 中 Hub 只在 `center` 出现一次，链中不重复渲染 |
| 8 | 封面必须有 `buaa-cover__date` |

### 严重级（影响正确性）

| # | 规则 |
|:---:|------|
| 9 | 大纲已有标题 → 严格沿用，一字不改。AI 不得修改、提炼或"优化" |
| 10 | 同一编号多页 → 自动细化为 X.Y.Z（如 1.4 连续3页 → 1.4.1 / 1.4.2 / 1.4.3） |
| 11 | `.adj-*` 仅作为 CSS 注释占位，不在 HTML 元素上激活（class 选择器在 scoped 中 specificity 常低于全局规则） |
| 12 | 加粗：Markdown 原生列表和裸文本中 `**text**` ✅；HTML `<li>`/`<td>`/`.buaa-hm-cap` 中用 `<strong>` |
| 17 | Scoped 样式必须用 `section { --var: val; }` 注入 CSS 变量。禁止直接写选择器覆盖（全局 `section.buaa-chapter xxx` specificity 更高，必定无效） |

### 注意级（影响质量）

| # | 规则 |
|:---:|------|
| 13 | 图片：`<div class="buaa-hm-fig">` → 空行 → `<img src="...">` → 空行 → `</div>`（前后空行防 `<p>` 包裹） |
| 14 | 禁止：`<footer>`、内容中用 `---`、`<img class/style>` |
| 15 | 标题层级：`#`仅用于文件总标题；`##`仅用于`Slide N:`分页标识；`###`为正文主标题；限三级（X/X.Y/X.Y.Z） |
| 16 | 序号与标题分离：大纲`###`中的编号提取填入 badge；`##`标题栏中不得出现序号 |
| 18 | 图片下载：大纲指明图片 URL 时，必须下载至 `figures/` 目录，`.md` 中以相对路径 `./figures/xxx.png` 引用 |
| 19 | 图注定位：图注 `<div class="buaa-hm-cap">` 必须紧跟其所解释的图片，与图片位于同一父容器内、放置在图片正下方。无论单图、双图还是混合布局，图注均通过父容器（`buaa-hm-fig` / `buaa-img-pair`）的 CSS 与图片保持居中对齐 |
| 20 | 双图并排：仅使用 `buaa-img-pair` + `buaa-hm-cap` 组合，禁止使用 `buaa-img-gallery`（不兼容图注） |

---

## 页面骨架模板

### 封面 (buaa-cover)

```html
<!-- _class: buaa-cover -->
<img class="buaa-cover__logo" src="./assets/logo.png">
# {主标题}
## {副标题，≤20字；无副标题则不写此行}
<div class="buaa-cover__presenter">汇报人：{姓名}</div>
<div class="buaa-cover__date">{日期}</div>
<div class="buaa-cover__decor">BEIHANG UNIVERSITY</div>
```

### 目录 (buaa-catalog) — ⚠️ inline style 不可省略

```html
<!-- _class: buaa-catalog -->
<style scoped>
ul { left: 730px !important; display: flex !important; flex-direction: column !important; gap: 28px !important; }
li { font-size: 24px !important; margin-bottom: 0 !important; }
</style>
<div class="buaa-catalog__title">目录</div>
<div class="buaa-catalog__line"></div>
<div class="buaa-catalog__eng">Contents</div>
<ul style="position:absolute;left:730px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:28px;list-style:none;z-index:2;padding:0;margin:0;">
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">{序号}</span> {章节标题}</li>
</ul>
```

### 过渡 (buaa-transition)

```html
<!-- _class: buaa-transition -->
<div class="buaa-transition__num">{章节号，如 01}</div>
# {中文标题}
## {英文标题}
```

### 正文通用骨架 (buaa-chapter) — ⚠️ `<style scoped>` 在 badge 之前

```html
<!-- _class: buaa-chapter -->
<style scoped>
/* === 图片尺寸 === */                          ← 有图时必写
/* .buaa-hm-fig img { max-height: XXXpx !important; } */
/* === 文本密度调节 === */
section { --text-p-size: XXpx; --text-p-line-height: X.X; }
/* === 图片最大高度 === */
/* .adj-img { max-height: XXXpx !important; } */
/* === 文本块：字号、行距 === */
/* .adj-txt { font-size: XXpx; line-height: X.X; } */
</style>
<div class="buaa-chapter__badge"><span>{编号}</span></div>
## {主标题}——{副标题}          ← 不写编号，编号已在 badge
<div class="buaa-chapter__body {布局类名}">
  <!-- 正文内容，使用 references/layout-templates.md 中的布局模板 -->
</div>
<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{页码}</div>
```

### 结尾 (buaa-end)

```html
<!-- _class: buaa-end -->
<div class="buaa-chapter__badge"><span>结语</span></div>
# 感谢您的观看与收听，敬请批评指正
## Q &amp; A
<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局决策树

> 完整 HTML 模板见 [references/layout-templates.md](references/layout-templates.md)。按内容类型选择：

| 内容特征 | 推荐布局 | 说明 |
|----------|----------|------|
| 文字+照片/渲染图 | **A** (split-2) | 文左图右，图片默认 Grid 居中+双向约束保持宽高比 |
| 文字≤180字+技术大图 | **F** (split-tb) | 文上图下，图片默认 Grid 居中+双向约束 |
| 文字>180字+技术图 | **A** (split-2) | 回退到文左图右 |
| 双图并排+各自图注 | **I** (img-pair) | 两张图独立图注 |
| 嵌套列表(ol>ul) | **B** (layout-flow) | 主条目≤4个+callout总结，使用 Markdown 原生列表 |
| 平铺列表(ul/ol>5条) | **B** (layout-flow) | 纯列表流式布局，使用 Markdown 原生列表 |
| 散文段落/公式 | **C** (layout-center) | 居中混排 |
| strong标题+子列表混合 | **J** (layout-flow) | 多组strong+ul，使用 Markdown 原生列表 |
| 双栏对比(各3~5条) | **D** (split-2+top) | 两列ol+底部callout |
| 居中混排含列表+表格 | **E** (layout-center) | 标题+ul+table+图注 |
| **窄表格(≤3列)** | **C-split** (split-2 top) | ⚠️ 必须分栏，居中会溢出滚动条 |
| 宽表格(≥4列)/纯表格 | **C** (layout-center) | 居中即可 |
| 流程图(→步骤) | **G** (flow-chart) | 步骤3~9个，line-long箭头 |
| 系统框图(center/left/right...) | **H** (block-diagram) | Hub仅出现一次 |
| 纯大图(无文字) | **K** (hm-fig) | 全屏图片 |

---

## Scoped 样式覆盖指南

> **核心原则**：scoped 中直接写选择器大概率无效，必须通过 `section {}` 注入 CSS 变量。

### 为什么失效

Marp 的 `<style scoped>` 追加 `[data-marpit-scope]` 属性选择器。全局 `section.buaa-chapter pre` specificity=(0,1,2) ≥ scoped `pre`→(0,1,2)，且 Marp 重处理全局 CSS 导致后加载的全局规则覆盖 scoped。

### ✅ 有效写法（通过 CSS 变量继承穿透 specificity）

| 写法 | 用途 |
|------|------|
| `section { --text-p-size: 20px; }` | 段落字号 |
| `section { --text-size: 20px; }` | 列表字号 |
| `section { --text-line-height: 2; }` | 列表行高 |
| `section { --text-item-gap: 6px; }` | 列表条目间距 |
| `section { --pre-font-size: 22px; }` | 代码块字号 |
| `section { --pre-font-family: "Fira Code", monospace; }` | 代码块字体 |
| `section { --pre-color: #333; }` | 代码块颜色 |
| `section { --pre-code-color: #333; }` | code元素颜色 |
| `section { --pre-line-height: 1.6; }` | 代码块行高 |
| `section { --code-font-size: 1em; }` | 行内代码字号 |
| `section { --code-color: var(--buaa-primary); }` | 行内代码颜色 |
| scoped `.buaa-flow-chart__arrow { margin: }` | 流程图箭头间距(specificity 0,2,1 > 全局 0,1,0) |
| `.buaa-hm-fig { display: grid; place-items: center }` | 图片居中容器，配合 `max-width`/`max-height` 双向约束保持宽高比 |

### ❌ 无效写法

```css
/* 以下全部无效 — specificity 不足或 !important 被 Marp 处理顺序覆盖 */
pre { font-size: 22px; }
pre, pre code { font-size: 22px !important; }
ol { font-size: 20px; }
ol li { margin-bottom: 6px; }
.adj-ol { font-size: 20px; }      /* class 未在 HTML 上激活 */
.adj-code { font-size: 40px; }     /* <pre> 无此 class */
```

---

## 文本密度参数速查

| 内容形态 | --text-p-size | 行高 | 图片缩放 |
|----------|:---:|:---:|:---:|
| 散文（无图） | 26px | 1.7 | — |
| 散文+大图 split-2 | 26px | 2 | max-width: 80-95% |
| 短文字(≤100字)+技术图 split-tb | 28px | 2 | max-width: 80-90% |
| 中等文字(100~180字)+图 split-tb | 28px | 1.5 | max-width: 80-90% |
| 嵌套列表 ol>ul | 22px | 3(ol)/2(ul) | — |
| 平铺列表 ≤4条 | 24px | 3.25 | — |
| 双列密集对比 split-top | 19px | 2.4 | — |

### 代码块专用变量

| 变量 | 默认值 | 示例用法 |
|------|--------|----------|
| `--pre-font-size` | 18px | `22px` / `1.2rem` / `120%` |
| `--pre-font-family` | Consolas, Courier New, monospace | `"Fira Code", "JetBrains Mono", monospace` |
| `--pre-color` | #333 | `#2d3436` / `rgb(45,52,54)` |
| `--pre-code-color` | #333 | 与 --pre-color 保持一致 |
| `--pre-line-height` | 1.6 | — |
| `--code-font-size` | 0.9em | `1em`(等大) / `0.85em`(缩小15%) |
| `--code-color` | var(--buaa-primary) | — |

---

## 多主题色系

### 切换主题

修改 `.md` 文件 YAML 前页中 `theme` 字段即可切换：

```yaml
---
marp: true
theme: buaa-red
---
```

### 主题速查

| 主题名 | 文件 | 主色 | 主色深 | 适用场景 |
|--------|------|:----:|:----:|------|
| `buaa` | `themes/buaa.css` | #004F9E | #003D7A | 北航蓝（默认），日常汇报/答辩 |
| `buaa-red` | `themes/buaa-red.css` | #C41230 | #9A0E24 | 北航红，庆典/党建/竞赛 |
| `buaa-gold` | `themes/buaa-gold.css` | #C49B2C | #9A7A22 | 北航金，学术典礼/荣誉表彰 |
| `buaa-dark` | `themes/buaa-dark.css` | #1B2D55 | #111D38 | 深空蓝，科技感/深色场景 |
| `buaa-green` | `themes/buaa-green.css` | #2E7D32 | #1E5A22 | 银杏绿，自然/环保/校园主题 |
| `buaa-purple` | `themes/buaa-purple.css` | #5C2D91 | #3F1E64 | 星空紫，创新/探索/太空主题 |

### 注册新主题

编辑 `.vscode/settings.json`，将新 CSS 文件路径加入 `markdown.marp.themes` 数组：

```json
{
  "markdown.marp.themes": [
    "themes/buaa.css",
    "themes/buaa-red.css",
    "themes/buaa-gold.css",
    "themes/buaa-dark.css",
    "themes/buaa-green.css",
    "themes/buaa-purple.css"
  ]
}
```

**修改 CSS 后生效**：VS Code 中执行 **Developer: Reload Window**（`Ctrl+Shift+P` 搜索该命令）。

所有主题 CSS 文件位于 `themes/` 目录，以 `buaa.css` 为蓝本通过 `@import-theme 'buaa'` 继承。

---

## 生成流程

```
Step 0: 解析大纲标题层级
   # → 文件总标题（仅一个）
   ## → 分页标识 Slide N: {标签}
   ### → 正文主标题 {编号} 主标题——副标题（编号提取到 badge）
   #### → 同编号拆分子页标识（编号仍为三级）

Step 1: 逐页分析 → {页面类型, 标题, 内容类型, 字数, 有无图片, 有无图注}

Step 2: 按决策树选布局 (A-K / C-split)

Step 3: 按模板生成：
   ├─ <style scoped> 在 badge 前（CSS变量 + .adj-* 注释占位）
   ├─ badge → ## 标题(无编号) → body(套用 layout-templates.md 模板) → footer → page-num
   ├─ 文本块裸写不用<p>；公式 $...$ 在裸文本中
   └─ 目录 ul 带 inline style；图片前后空行

Step 4: 编号：大纲标题一字不改；同编号多页自动细化 X.Y.Z

Step 5: 组装：封面 → 目录 → 过渡 → 正文×N → 过渡 → ... → 结尾

Step 6: 命名输出文件：以 PPT 主题命名，不加「大纲」「outline」等后缀
   例：大纲名为「BUAA_Marp_Template-outline.md」→ 生成「BUAA_Marp_Template.md」
```

---

## Markdown 语法可用范围

| 上下文 | `$...$` | `**...**` | 替代方案 |
|--------|:---:|:---:|------|
| 裸文本段落 | ✅ | ✅ | 直接用 |
| Markdown 原生列表（`1. ` / `- ` / 嵌套 `- `） | ✅ | ✅ | 直接用 — Marp 渲染管线下 KaTeX 正常 |
| `##` 标题内 | ✅ | ✅ | 直接用 |
| `<div>` 内纯文本（未嵌HTML标签） | ✅ | ✅ | 直接用 |
| HTML `<li>` 标签 | ❌ | ❌ | `<i>x</i><sub>1</sub>` / `<strong>` |
| `<td>` 表格单元格 | ❌ | ❌ | `<i>x</i><sub>1</sub>` / `<strong>` |
| `.buaa-hm-cap` 图注 | ❌ | ❌ | `<i>x</i><sub>1</sub>` / `<strong>` |

> **关键区分**：Markdown 原生列表（`1. item` / `- item`）由 Marp 渲染，`$...$` 和 `**text**` 正常生效。只有手工编写的 HTML `<li>`/`<td>` 标签中才禁用。

### 列表语法决策表

| 列表所在上下文 | 推荐语法 | `$...$` | `**text**` |
|:---|:---:|:---:|:---:|
| body 容器直接子元素（`layout--flow` / `layout--center`） | `1. ` / `- ` 原生 | ✅ | ✅ |
| 嵌套在 `<div>` 内（split-2 列 / `.text-block`） | HTML `<ol><li>` / `<ul><li>` | ❌ 用 `<i>x</i><sub>1</sub>` | ❌ 用 `<strong>` |
| `.buaa-callout` 内 | 裸文字 | ❌ 用 `<i>x</i><sub>1</sub>` | ❌ 用 `<strong>` |

> 典型场景：大纲中 `1. **算法鲁棒性**\n   - DDE对初始值...` → PPT 中直接写成 `1. **算法鲁棒性**\n   - DDE对初始值...`（原生语法，`$...$` 和 `**` 均可用）。唯一例外是当列表必须嵌入 `<div>` 内部时才退回 HTML。

---

## 布局模板详情

完整的 11 个布局模板（A-K + C-split）含完整 HTML/CSS 代码，详见：

📎 **[references/layout-templates.md](references/layout-templates.md)**

生成时按决策树选定布局后，从该文件复制对应模板替换 `{...}` 占位符。

---

## Reference 文件索引

| 文件 | 内容 | 用途 |
|------|------|------|
| [layout-templates.md](references/layout-templates.md) | 11 个布局模板（A-K + C-split） | 按决策树选定布局后复制模板 |
| [typography-design.md](references/typography-design.md) | 排版设计参考规范 | 字体、字号、颜色体系、推荐布局、样式优先级、常见错误速查 |

> 当用户要求「参照项目风格」或「符合北航VI规范」时，优先参考 typography-design.md。
