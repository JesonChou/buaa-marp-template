---
name: buaa-marp-ppt
description: >
  Generate BUAA-themed Marp PPT from an outline file. Agent reads the outline,
  picks layout per slide, and writes a complete Marp markdown file.
  Supports 6 themes (buaa/buaa-red/buaa-gold/buaa-dark/buaa-green/buaa-purple)
  and 12 layout templates (A-K + C-split). Zero external dependencies.
metadata:
  version: "4.0.0"
compatibility: Trae / Cursor / VS Code with Marp. Requires themes/ directory.
---

# BUAA Marp PPT Skill

Given an outline `.md`, produce a complete Marp presentation. No other input needed.

## §1 生成流水线

```
Step 0: Parse headings — # file title; ## Slide N: [tag]; ### {num} title——subtitle; #### sub-page marker
Step 1: For each body slide, pick layout by matching content against the decision table below
Step 2: Copy the matching HTML template from references/layout-templates.md, fill {placeholders}
Step 3: Number pages: cover/contents/transition unnumbered; body 1..N; end-page last
Step 4: Assemble: cover → contents → transition → body×N → transition → … → end
Step 5: Name output as {outline-filename-stem}.md  (strip "-outline" suffix)
```

## §2 布局决策表

Select ONE layout per body slide. Match in order: first check `NL triggers` against outline text, then fall back to `Content pattern`.

| 自然语言触发 | 布局 | body class | 密度变量 |
|---|---|---|---|
| `纯文字` / `文字段落` / `散文` | **B**-flow | `buaa-layout--flow` | `--text-p-size:26px; --text-p-line-height:2` |
| `居中` (带公式/表格) | **C** | `buaa-layout--center` | `--text-p-size:26px; --text-p-line-height:1.7` |
| `居中，双栏` / `窄表格` (≤3列) | **C-split** | `buaa-split--2 buaa-split--top` | `--text-size:22px; --text-line-height:1.8` |
| `双栏对比` / `左右对比` | **D** | `buaa-split--2 buaa-split--top` | `--text-size:19px; --text-line-height:2.4` |
| `左文右图` `各半` / `文左图右` | **A1** (split-2) | `buaa-layout--center` + `buaa-split--2` | `--text-p-size:26px; --text-p-line-height:2` |
| `左图右文` / `图左文右` | **A2** (A 对称) | same as A1, swap divs | same as A1 |
| `文三图七` / `左文右图，文三图七` | **A** + split-1-2 | `buaa-split--1-2` | `--text-p-size:26px; --text-p-line-height:2` |
| `图七文三` / `左图右文，图七文三` | **A** + split-2-1 | `buaa-split--2-1` | `--text-p-size:26px; --text-p-line-height:2` |
| `文上图下` + 技术图 | **F** | `buaa-layout--center` + `buaa-split-tb` | `--text-p-size:28px; --text-p-line-height:1.5-2` |
| `流程图` / `步骤` | **G** | `buaa-layout--center` + buaa-flow-chart | `--fc-font-size:24px` |
| `系统框图` | **H** | `buaa-layout--center` + buaa-block-diagram | — |
| `双图并排` + 图注 | **I** | `buaa-layout--center` + img-pair | — |
| `分类列表` / `strong标题+列表` | **J** | `buaa-layout--flow` | `--text-size:22px; --text-line-height:2` |
| `满页大图` / `纯大图` | **K** | `buaa-layout--center` + hm-fig | — |
| `居中表格` / `居中混排含列表` | **E** | `buaa-layout--center` + text-block | `--text-p-size:26px; --text-p-line-height:1.7` |
| `毛玻璃卡片` | **B**-flow | `buaa-layout--flow` + buaa-am--fglass | `--text-size:22px; --text-line-height:1.8` |

**Decision priority**: (1) Has image? → A/F/I/K. (2) Has flowchart/diagram keyword? → G/H. (3) Has table? → C/C-split/D. (4) Has nested-list or strong+ul? → B/J. (5) Plain text → B.

### 密度变量速查

| 场景 | 变量 |
|---|---|
| 段落 | `--text-p-size` (default 26px) · `--text-p-line-height` (default 1.7) |
| 列表 | `--text-size` (default 24px) · `--text-line-height` (default 1.8) · `--text-item-gap` (default 8px) |
| 代码块 | `--pre-font-size` (default 22px) · `--pre-font-family` · `--pre-bg` · `--pre-color` · `--pre-code-color` (回退到 `--pre-color`) · `--pre-line-height` · `--pre-font-weight` · `--pre-padding` · `--pre-border-left` · `--pre-border-radius` · `--pre-border` · `--pre-margin` · `--pre-letter-spacing` |
| 行内代码 | `--code-font-size` (0.9em) · `--code-color` (var(--buaa-primary)) |
| 流程图 | `--fc-font-size` · `--arr-length` · `--line-width` · `--arr-color` |

### 代码块字体与字重

默认字体栈：Cascadia Code → JetBrains Mono → Consolas → Courier New。

Cascadia Code 内置字重：300(Light) / 400(Regular) / 600(SemiBold) / 700(Bold)。
无需安装，Windows 自带。

## §3 硬约束

### 致命 (违反崩溃)

1. `<style scoped>` 在 `buaa-chapter__badge` 之前，绝不在 `page-num` 之后
2. `.buaa-text-block` 内禁止 `<p>` — 裸写文字，Marp 自动生成
3. **列表优先 Markdown 原生** (`1.`/`-`) — 仅当列表嵌在 `<div>` 内时才用 HTML `<li>`+`<strong>`+`<i>x</i><sub>1</sub>`
4. 目录 `ul` 必须带完整 inline `style="position:absolute;left:730px;..."` — scoped 中写选择器不可靠
5. `$...$` ✅ 裸文本/原生列表/`##` 标题；❌ HTML `<li>`/`<td>`/`.buaa-hm-cap` → 用 `<i>x</i><sub>1</sub>`
6. 图注仅在大纲标注"图注："时添加 — 不自编
7. `buaa-block-diagram` Hub 只在 `center` 出现一次
8. 封面必须有 `buaa-cover__date`

### 严重 (影响正确性)

9. 大纲标题一字不改
10. 同一编号多页 → 自动 X.Y.Z
11. `.adj-*` 仅作 CSS 注释占位，**不激活**
12. 加粗：原生列表/裸文本 `**text**` ✅；HTML `<li>`/`<td>` 中用 `<strong>`
13. Scoped → 必须 `section { --var:val; }` 注入 CSS 变量。**禁止写选择器** (全局 specificity 更高)

    **为什么选择器会失效**：Marp 的 `<style scoped>` 会给选择器追加 `[data-marpit-scope]` 属性选择器。全局 CSS 中 `section.buaa-chapter pre` 的 specificity=(0,1,2)，scoped 中的裸 `pre` 也是 (0,1,2)，且 Marp 的 CSS 处理顺序导致后加载的全局规则覆盖 scoped。只有通过 `section { --var: val; }` 注入 CSS 变量，才能穿透 specificity 屏障——因为 CSS 自定义属性通过继承流入子元素，不受选择器优先级影响。

14. 图片：`<div class="buaa-hm-fig">` → 空行 → `<img>` → 空行 → `</div>` (防 `<p>` 包裹)
15. 禁止 `<footer>` / 内容中 `---` (用 `<hr>`) / `<img class/style>`

### 注意 (影响质量)

16. 标题层级：`#`仅总标题；`##`仅 Slide N；`###`正文主标题；最多三级
17. 序号与标题分离：`###`中的编号 → badge；`##`不出现序号
18. 图片 URL → 下载到 `figures/` → `.md` 中用 `./figures/xxx.png`
19. 图注紧跟图片同父容器下方
20. 双图并排用 `buaa-img-pair` + `buaa-hm-cap`，禁用 `buaa-img-gallery`

## §4 页面骨架

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
<style scoped>ul { left: 730px !important; display: flex !important; flex-direction: column !important; gap: 28px !important; } li { font-size: 24px !important; margin-bottom: 0 !important; }</style>
<div class="buaa-catalog__title">目录</div><div class="buaa-catalog__line"></div><div class="buaa-catalog__eng">Contents</div>
<ul style="position:absolute;left:730px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:28px;list-style:none;z-index:2;padding:0;margin:0;">
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">{N}</span> {章名}</li>
</ul>
```

### 过渡
```html
<!-- _class: buaa-transition -->
<div class="buaa-transition__num">{如 01}</div>
# {中文标题}
## {English Title}
```

### 正文骨架
```html
<!-- _class: buaa-chapter -->
<style scoped>
/* .buaa-hm-fig img { max-width:XX% !important; max-height:XXpx !important; } */
section { --text-p-size: {段落字号}; --text-p-line-height: {段落行高}; }
</style>
<div class="buaa-chapter__badge"><span>{编号}</span></div>
## {主标题}——{副标题}
<div class="buaa-chapter__body {布局类名}">
  <!-- 从 references/layout-templates.md 复制对应模板填充 -->
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
<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 主题切换

```yaml
theme: buaa           # 默认蓝  #004F9E
theme: buaa-red       # 红     #C41230
theme: buaa-gold      # 金     #C49B2C
theme: buaa-dark      # 深空蓝 #1B2D55
theme: buaa-green     # 银杏绿 #2E7D32
theme: buaa-purple    # 星空紫 #5C2D91
```

---

完整 12 套布局 HTML 模板见 `references/layout-templates.md`。排版设计参考见 `references/typography-design.md`。
