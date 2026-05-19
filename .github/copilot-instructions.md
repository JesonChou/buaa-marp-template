# BUAA Marp PPT 项目规范

## 适用范围

本文件适用于 `buaa-marp-template/` 目录下所有 `.md` 文件的 Marp 幻灯片生成和编辑。

## 核心规则

### 从大纲生成 PPT 的铁则

当用户提供大纲文档（HTML 或 Markdown 格式）并要求生成 PPT 时：

1. **文件命名**：以大纲主题名称新建 `.md` 文件，与大纲文件名保持一致（如大纲为 `主题名称-大纲.html`，则生成 `主题名称.md`）
2. **内容忠实**：严格按大纲逐页生成，大纲中没有的内容（如图片、表格、额外文字、副标题）一律不添加
3. **图片占位**：仅当大纲明确标注了图片文件名时才插入图片，不自行推测或添加图片占位符
4. **图片下载**：若大纲中指明了图片的网络链接（URL），需下载图片并保存至项目 `figures/` 文件夹，按大纲中的命名规则命名，格式统一为 `.png`；在 `.md` 文件中以相对路径 `./figures/xxx.png` 引用
5. **章节编号与标题**：若大纲文件中明确给出了章节编号和标题（如"1.1 什么是静电放电"），则<strong>严格沿用</strong>大纲中的编号和标题，不得自行修改或重新提炼；若大纲未提供，则按编号规则自行提炼标题，格式为 `## 主标题——副标题`（副标题仅在必要时添加，20 字以内）
6. **图注判定** ⚠️：仅当大纲中明确以<strong>"图注："</strong>（或"图注"后跟冒号）标注的文字才是图注，使用 `.hm-cap` 放置。大纲中图片前后未标注"图注："的文字均为正文内容，不得放入 `.hm-cap`。若大纲中该图片无任何"图注："标注，则 `.hm-fig` 内<strong>不添加</strong> `.hm-cap`。严禁自行根据图片内容推断、编造图注文字。

### 页面类型（5 种）
生成 PPT 时必须按此顺序组织：
```
封面(cover) → 目录(catalog) → 过渡(transition) → 正文(chapter)×N → ... → 结尾(end)
```

### 正文布局（10 种模式）
所有内容页必须从以下模式中选择，详见 `.agents/skills/buaa-marp-ppt/references/buaa-layout-styles.md`：
- A: 文左图右 (split-2) — 3 条短要点 / 散文段落+重要证据图（50:50 均衡）⭐ **图文默认布局**
- B: 文宽图窄 (split-right) — 3 条长 bullet 要点（>40 字）+ 辅助示意图（68:32）⚠️ **仅限明确触发条件**
- C: 三卡+图廊 (card-grid + img-gallery) — 3 概念并列
- D: 三卡+单图 (card-grid + hm-fig) — 3 方法对比
- E: 三卡+双图 (card-grid + img-pair) — 3 趋势展示
- F: 时间轴 (timeline + callout) — 历史演进
- G: 图标总结 (icon-list + split-right) — 总结页
- H: 双栏对比 (split-2 + callout) — 两类并列内容各 3~5 条目 + 底部总结
- **补充：文上图下 (split-tb)** — 图片为技术原理图/曲线图/框图，需要大尺寸才能看清细节
- **I: 流程图 (flow-chart)** — 3~9 个串行步骤，大纲以 `buaa-diagram:flowchart` 代码块标注
- **J: 系统框图 (block-diagram)** — 中心枢纽 + 四向节点链，大纲以"系统框图"缩进格式标注。生成时参照 `.agents/skills/buaa-marp-ppt/references/buaa-block-diagram-example.md`

### ⚠️ 图文布局决策铁律（必读，优先于一切旧规则）

> 以下规则经大量页面视觉验证确定，**严格按此执行**。
> 经验证：split-2 可覆盖绝大多数图文并排场景，split-tb 专用于技术大图，**split-right 仅在极端条件下使用**。

#### 第一铁律：split-2 是图文左右并排的默认布局

**split-2（50:50）适用于所有文字+图片左右并排场景，除非触发 split-tb 或 split-right 的硬性条件。**

| 内容形态 | 布局 | 理由 |
|----------|:---:|------|
| 散文段落（无 bullet）+ 任意图片 | **split-2** | 散文在 50% 列宽下自然换行即可填满，不需要 68% 宽列 |
| bullet 列表（≤3条，每条≤40字）+ 图片 | **split-2** | 短要点 50% 宽足够，图片有充足展示空间 |
| bullet 列表（3~5条，部分>40字）+ 图片 | **split-2** | 优先微调字号（22→20px）而非切换 split-right |
| bullet 列表（>5条，多条>80字）+ 辅助示意图 | 考虑拆分页面，仍不行才用 split-right | 最后手段 |
| 图片为照片/截图/封面图 | **split-2** | 照片在 50% 宽度下视觉效果良好 |

#### 第二铁律：split-right 是最后手段

**仅当同时满足以下 ALL 条件时才使用 split-right（68:32）：**

1. ✅ 内容是 **bullet 列表**（不是散文段落）
2. ✅ 列表条目 **≥4 条**，且多条 **>60 字**
3. ✅ 图片是 **辅助示意图**（不是核心证据图），在 32% 宽度下仍可辨认
4. ✅ 已尝试 split-2 + 缩小字号至 20px，文字仍然溢出

**以下情况绝对不用 split-right：**
- 散文段落 → 永远用 split-2
- 图片是核心证据/需要大尺寸 → 用 split-2（不因文字长牺牲图片空间）
- 图片是技术原理图/曲线图 → 用 split-tb（上下布局）
- 列表条目 ≤3 条 → 用 split-2

#### 第三铁律：split-tb 仅用于"图需全宽"场景

**仅当图片为以下类型且需要大尺寸展示细节时才用 split-tb（上下布局）：**

| 图片类型 | 典型场景 | 文字量上限 |
|----------|------|:---:|
| 技术原理图（含标注、箭头、多组件） | TLP 脉冲产生电路、测试系统框图 | ≤180 字 |
| 数据曲线图（含多曲线、坐标轴） | I-V 特性曲线、时域波形 | ≤150 字 |
| 流程图/框图（非用 I/J 模式生成的） | 系统工作流程图 | ≤120 字 |
| 对比图（并排双图各有图注） | 波形采集 vs 漏电流测量 | ≤100 字 |

**以下情况不用 split-tb：**
- 图片是照片/渲染图 → 用 split-2（50% 宽度足够）
- 文字 > 200 字 → 用 split-2（文字需要更多垂直空间与图片并排）
- 文字是 bullet 列表形态 → 优先 split-2

#### 横竖排版快速决策矩阵

```
输入：有文字 + 有图片的一页
│
├─ 图片是照片/渲染图/封面？
│   └─ YES → split-2（无条件）
│
├─ 图片是技术原理图/曲线图/框图（含细节标注）？
│   ├─ 文字 ≤ 180 字（散文）→ split-tb（图需全宽展示细节）
│   └─ 文字 > 180 字 → split-2（文字多时并排更高效）
│
├─ 文字是散文段落（无 bullet）？
│   └─ YES → split-2（无条件，散文在 50% 列自然换行）
│
├─ 文字是 bullet 列表？
│   ├─ ≤3 条，每条 ≤40 字 → split-2
│   ├─ 3~5 条，部分 >40 字 → split-2 + 微调字号（22→20px）
│   ├─ >5 条，多条 >60 字 → 优先拆页；不拆页则 split-2 + 字号降至 19px
│   └─ >5 条，多条 >80 字，且图片为辅助示意图 → split-right（最后手段）
│
└─ 只有文字（无图）？
    ├─ 散文段落/表格/公式 → layout-center
    └─ 列表为主 → layout-flow
```

### 强制格式
- 加粗: `<strong>text</strong>`（禁止 `**text**`，HTML 块内 Marp 不解析 Markdown）
- **HTML 块内禁用所有 Markdown 语法** ⚠️: 包括 `**加粗**`、`*斜体*`、`$公式$` 等——只要在 `<div>` / `<p>` / `<li>` / `<td>` 等 HTML 标签内，Marp 一律不解析。必须转用纯 HTML 替代：加粗用 `<strong>`，公式用 `<i>x</i><sub>1</sub>` 等。仅 Markdown 自然段落（不用 HTML 标签包裹的纯文本行，之间以空行分隔）中的 `$...$` 和 `**...**` 可被 Marp 正常解析。
- 图注: `<div class="hm-cap">text</div>`（16px/#000/bold/微软雅黑）
- 图片: `<div class="hm-fig">` 容器，`<img>` 前后各空行
- 双图+图注: 用 `img-pair` + `hm-cap`（不用 `img-gallery`，后者不支持图注；不用 `.img-caption` 类）
- 目录: `ul { left: 730px }`，不设 `width`，`li { font-size: 24px }`，`gap: 28px`；调整间距只改 gap（20px 紧凑 / 28px 标准 / 36px 舒展）
- 结尾: 结束语固定为 `感谢您的观看与收听，敬请批评指正`（禁止"感谢聆听"等变体）
- 禁止: `<footer>`, 内容中 `---`, `<img class>` 或 `<img style>`
- **样式微调** ⚠️: 字号、行距、图片大小等调节一律在 `.md` 文件中通过 `<style scoped>` 完成，**禁止**修改 `buaa.css`。buaa.css 已内置 CSS 变量（`--text-size`/`--text-line-height`/`--text-item-gap`/`--text-p-size`/`--text-p-line-height`），在 scoped 中覆写 `section { --text-size: 22px; ... }` 即可全局生效
- **文本密度块** ⚠️: 每个 chapter slide 必须附带 `/* === 文本密度调节 === */` scoped 块，优先用 CSS 变量方式
- **注释规范** ⚠️: 所有 CSS 注释放在被描述代码的**上一行**，禁止行尾注释（`/* comment */ code` 视为行尾注释）
- **元素调整 class** ⚠️: 从大纲生成 PPT 时，每个 chapter 页的每个正文元素（文本块、列表、图片、表格、callout）必须添加独立调整 class（参见 `buaa-block-diagram-example.md` 第十一章），并在 scoped CSS 中附带注释掉的调整代码块

### ⚠️ 空间预评估（每页生成前必须执行）

`.chapter-body` 可视区域：**宽 1246px × 高 634px**（1366×768 减去边距）。生成每页前逐项估算：

#### 各布局模式空间预算

| 布局 | 文字区可用空间 | 图片区可用空间 | 检查重点 |
|------|:---:|:---:|------|
| split-2（50:50） | ~603px 宽 × ~580px 高 | ~603px 宽 × ~500px 高 | 列宽是否容纳最长 bullet 行 |
| split-right（68:32） | ~827px 宽 × ~580px 高 | ~379px 宽 × ~500px 高 | 图片在 379px 宽下是否可辨 |
| split-tb（文上图下） | 全宽 × 自适应高 | 全宽 × 剩余高 | 文字高度 + 图片 max-height + 图注 ≤ 580px |
| layout-flow（纯文字） | 全宽 × ~580px 高 | — | 条目数 × 字号 × 行距 ≤ 550px |
| layout-center（居中） | 全宽 × ~580px 高 | 全宽 × ~500px 高 | 表格行数 × 行高 ≤ 400px |

#### 溢出快速判定

| 检查项 | 公式 | 安全阈值 | 超标处理 |
|--------|------|:---:|------|
| 列表条目总高 | `条目数 × (字号 × 行距 + item-gap)` | ≤ 520px | 缩小字号/行距或拆分页面 |
| 散文段落高 | `估算行数 × 字号 × 行距` | ≤ 500px | 缩小 --text-p-size |
| 图片+图注 | `max-height + 30px(图注)` | ≤ 分配区高度 | 减小 max-height 或切换布局 |
| 表格行数 | `行数 × 44px + 表头 48px` | ≤ 400px | 缩小表格字号 |
| 双列每列宽度 | `最长条目字数 × 50%字号` | ≤ 列宽 - 40px | 缩小字号或换短表述 |

**超标时优先调 CSS 变量，不换布局；调完仍超标才切换布局模式。**

### 排版参数速查

以下参数为经过视觉验证的推荐值，生成新 PPT 时直接套用。

#### scoped CSS 区块内部排序

每个 chapter slide 的 `<style scoped>` 内部按此顺序组织：

```
1. /* === 图片尺寸 === */         （有图时必写，无图则跳过）
2. /* === 文本密度调节 === */     （每个 chapter slide 必写）
3. 逐元素 CSS 规则               （仅 CSS 变量不够用时才写）
4. /* === 图文间距 === */         （仅 split-tb 布局）
5. .adj-* 注释占位块              （每个 chapter slide 必写）
```

#### 文本密度参数速查

| 内容形态 | CSS 变量 / 规则 | 推荐值 | 适用场景 |
|----------|----------------|:---:|------|
| 散文段落（1~2段，无图/小图） | `--text-p-size` / `--text-p-line-height` | 26px / 1.7 | 纯文本页：概念介绍、背景说明 |
| 散文段落 + 大图（split-2 / split-tb 短文字） | `--text-p-size` / `--text-p-line-height` | 26px / 2 | 图文并排页：案例说明 + 证据图 |
| 短文字(≤100字) + 技术大图（split-tb） | `--text-p-size` / `--text-p-line-height` | 28px / 2 | 技术原理页：电路图、测试系统图 |
| 中等文字(100~180字) + 图（split-tb） | `--text-p-size` / `--text-p-line-height` | 28px / 1.5 | 波形分析页：波形图、数据曲线 |
| 短文字 + 特大图（split-tb，图占主导） | `--text-p-size` / `--text-p-line-height` | 26px / 1.5 | 核心图表页：I-V 曲线、频谱图 |
| 有序/无序列表为主（layout-flow, >5条目） | `ol`/`ul` font-size / line-height | 22px / 3 | 危害列表、发展历程 |
| 列表为主（layout-flow, ≤4条目） | `ol`/`ul` font-size / line-height | 24px / 3.25 | 标准对比、模型对比 |
| 嵌套列表（ol内嵌ul） | `ol ul li` font-size / line-height | 21px / 2 | 分类详述：主条目 + 子说明 |
| 双列密集对比（split-2 split-top，每列≥3条目） | `split-2 ol li` font-size / line-height | 19px / 2.4 | 双栏对比：方法A vs 方法B |

#### 图片最大高度阈值

| 图片角色 | max-height | 典型场景 |
|----------|:---:|------|
| 辅助示意图（文为主，图为辅） | 250–300px | split-tb 长文字、split-right |
| 标准插图 | 480px | buaa.css 默认值 |
| 核心证据图（图为焦点） | 500–520px | split-2 大图、split-tb 图主导 |
| 双图并排（img-pair） | 默认不设，依赖 img-pair 容器约束 | 对比图：波形采集 vs 漏电流测量 |

#### callout 参数默认值

| 场景 | font-size | line-height | padding |
|------|:---:|:---:|:---:|
| 正文底部总结（标准） | 22px | ~1.8 | 默认 |
| 框图底部图例 | 20px | 2 | 12px 22px |

#### split-tb 固定模板

每个 split-tb 页必须同时包含以下三个调节块：

```html
<style scoped>
/* === 图片尺寸 === */
/* 图片最大高度 */
.hm-fig img { max-height: XXXpx !important; }
/* === 文本密度调节 === */
section {
  --text-p-size: XXpx;
  --text-p-line-height: X.X;
}
/* === 图文间距 === */
/* 文字与图片之间的间距 */
.split-tb { gap: 1px; }
/* 图片：最大高度 */
/* .adj-img { max-height: XXXpx !important; } */
</style>
```

#### `<br>` 间距块

在 `layout-center` 幻灯片中，多个文本块、表格之间用 `<br>` 分隔，保持呼吸感：

```html
<div class="text-block adj-txt">...</div>
<br>
| 表格 |
| :--- |
<br>
<div class="text-block adj-txt">...</div>
```

#### Markdown 语法可用范围速查 ⚠️

Marp 的 KaTeX / Markdown 解析铁律：**只要文本被 HTML 标签包裹，其内部的 `$...$`、`**...**`、`*...*` 一律不解析**。

| 上下文 | `$...$` | `**...**` | 替代方案 |
|--------|:---:|:---:|------|
| Markdown 自然段落（空行分隔，无 HTML 标签包裹） | ✅ | ✅ | 直接用 |
| `<li>` 列表项内 | ❌ | ❌ | 公式 → `<i>x</i><sub>1</sub>` 或 Unicode；加粗 → `<strong>` |
| `<p>` 段落标签内 | ❌ | ❌ | 去掉 `<p>`，改用空行分隔的自然段落 |
| `<div>` 容器内但**未被其他 HTML 标签包裹**的纯文本 | ✅ | ✅ | 可直接用（Marp 会先解析再自动生成 `<p>`） |
| `<div class="hm-cap">` 图注内 | ❌ | ❌ | 公式 → `<i>t</i>=0` 或 Unicode；加粗 → `<strong>` |
| `<td>` 表格单元格内 | ❌ | ❌ | 公式 → `<i>x</i><sub>1</sub>`；加粗 → `<strong>` |
| Markdown `##` 标题内 | ✅ | ✅ | 直接用 |

典型错误与修复：

```html
<!-- ❌ 错误：<li> 内 $...$ 不渲染 -->
<li>脉冲宽度非常窄（$\leq 10\ \text{ns}$）</li>

<!-- ✅ 正确：转 Unicode 或 HTML -->
<li>脉冲宽度非常窄（≤ 10 ns）</li>

<!-- ❌ 错误：<p> 内 $...$ 不渲染 -->
<p>电压为 $u_0/2$。</p>

<!-- ✅ 正确：去掉 <p>，空行分隔 -->
电压为 $u_0/2$。

<!-- ❌ 错误：hm-cap 内 $...$ 不渲染 -->
<div class="hm-cap">步骤：$t=0$ 时刻</div>

<!-- ✅ 正确：转 HTML -->
<div class="hm-cap">步骤：<i>t</i>=0 时刻</div>

<!-- ✅ 正确：<div> 内未被标签包裹的纯文本可用 $...$ -->
<div>
输入电压：$u_0$，传播时间：$\tau = 1/v$。
</div>
```

### Marp 样式生效优先级
1. buaa.css（需 Reload Window 后生效，Marp 扩展会缓存 CSS）
2. `<style scoped>`（Marp 原生支持）
3. inline `style="..."`（最高优先级，Marp 不剥离 ul/li 的 style 属性，可用作兜底）

### 常见陷阱
| 错误 | 正确 | 原因 |
|------|------|------|
| 目录 `ul` 设 `width` | 不设 width，块宽自适应 | 设 width 会偏左，右半区自然居中即可 |
| `**text**` 在 `<div>` 内 | `<strong>text</strong>` | HTML 块内不解析 Markdown |
| `$...$` 在 `<p>` / `<div>` 等 HTML 标签内 | 去掉 `<p>` 标签，用 Markdown 自然段落（空行分隔）；或在 hm-cap 等纯 HTML 容器中用 `<i>x</i><sub>1</sub>` | 同上，KaTeX 不处理 HTML 元素内的 `$...$` |
| 双图+图注用 `img-gallery` | `img-pair` + `hm-cap` | gallery 不支持图注 |
| 图注用 `*text*` 或 `.img-caption` | `.hm-cap` | 图注必须统一 hm-cap 样式 |
| `width:100%` + padding | + `box-sizing:border-box` | 总宽溢出被 overflow 裁掉 |
| 修改 `buaa.css` 来调节字号或行距 | 在 `.md` 对应 slide 中加 `<style scoped>` | 用户偏好：样式微调不碰全局 CSS，保持 buaa.css 稳定 |
| 表格在 `layout-flow` 中不居中 | 改用 `layout-center` + `.text-block` 包裹长文本 | `<style scoped>` 对 Marp markdown 表格无效；只有 `.layout-center table` 规则能居中表格 |

### 图文自动生成：触发语法

当大纲需要生成流程图或系统框图时，使用**自然语言缩进格式**。触发词独占一行，后续以缩进的 `→` 行列出内容：

**流程图：**
```
流程图（纵向）：
  → 步骤1
  → 步骤2
  → 步骤3
```
- `流程图` 独占一行 + 后续缩进 `→` 行 → 触发图表生成
- `（纵向）` 或默认：垂直排列，节点上下堆叠，箭头向下（`arr-solid-down`）
- `（横向）`：水平排列，节点左右并排，箭头向右（`arr-solid-right`）
- 每行 `→` 开头，步骤数 3~9 个；步骤文本自身含 `→` 时用 `\→` 转义
- 无缩进 `→` 行时退化为旧单行格式：`流程图：A→B→C`（仍兼容）

**系统框图：**
```
系统框图：
  center: 枢纽节点
  left: 节点A → 节点B → 枢纽节点
  right: 节点C → 枢纽节点
  bottom: 节点D → 节点E → 枢纽节点
  top: 枢纽节点 → 节点F
```
- `center:` 声明枢纽（必填，渲染为 `.bd-hub` 深蓝填充）
- **链中保留 Hub**：每条链写出完整路径（含枢纽），AI 自动识别并去重渲染
- **Hub 位置决定箭头方向**：Hub 在链**末尾** → 箭头指向中心（向心）；Hub 在链**开头** → 箭头从中心出发（离心）
- **位置决定链方向**：`left`/`right` → 横向链（flex row）；`top`/`bottom` → 纵向链（flex column）
- 链内 `→` 分隔节点；方向词：`left` / `right` / `top` / `bottom`（可选）

**区分正文的规则：**
- `流程图` 独占一行 + 后续缩进 → 触发图表
- `流程图` 同行后有正文（如 `流程图：如图所示`）→ **不触发**，视为普通文本
- 旧单行格式 `流程图：A→B→C` 仍兼容

### 箭头样式库（arr-*）

流程图和框图中使用的箭头来自 `buaa.css` 内置箭头样式库：

| 样式 | 类名 | 视觉效果 | 场景 |
|------|------|----------|------|
| 实心三角 | `arr-solid-*` | ▶ 粗壮醒目 | 默认，流程步骤间主连接 |
| 空心 V 形 | `arr-outline-*` | ⪢ 轻盈现代 | 科技风框图 |
| 细线箭头 | `arr-line-*` | → 低调学术 | 学术论文风，尾长24px |
| 长尾细线 | `arr-line-long-*` | —→ 连接跨度大 | 框图远距离连接，尾长60px（可设 `--arr-length`） |
| 双线箭头 | `arr-double-*` | ⇒ 数据流风格 | 技术框图，双线+三角头，线宽可设 `--arr-thick`（默认2px） |

每种样式 4 方向：`-right` / `-left` / `-down` / `-up`。箭头颜色通过 `--arr-color`（默认 `#004F9E`）控制。`arr-line-long` 长度通过 `--arr-length` 自定义（默认 60px）。

**链内箭头自动伸缩：** 在 `.bd-chain` 中给箭头加 `.arr-fill` 类可使箭头自动填充节点间剩余空间，搭配 `bd-spread` 实现均匀分布。

**在 .md 中调节箭头：** 在 scoped 块中覆写 CSS 变量即可全局生效；单箭头覆盖需在 scoped 中定义独立 class（⚠️ Marp 会剥离 div 的 inline style，不能用 `style="..."` 覆盖）：
```html
<style scoped>
.block-diagram {
  --arr-color: #004F9E;   /* 颜色 */
  --arr-length: 80px;     /* 长尾长度 */
  --arr-thick: 3px;       /* 双线线宽 */
}
</style>
```

### 编号规则
- 章节 badge: 仅 1 页正文 → 单数字；≥2 页 → X.Y；子节 → X.Y.Z
- 编号层级: 最多 3 级（如 `1.1.1`），禁止 `1.1.1.1` 等更深层级
- 页码: 封面/目录/过渡无页码；正文从 1 连续；结尾最后

### 主题文件
- `buaa.css` 必须 UTF-8 无 BOM
- 修改 CSS 后需 VS Code → Developer: Reload Window
- 若样式不生效 → 使用 inline style 兜底（Marp 不剥离 `<ul>/<li>` 的 style 属性）

## 技能引用

创建或编辑 BUAA Marp PPT 时，同时加载以下两个技能：

1. **主技能**: `.agents/skills/buaa-marp-ppt/SKILL.md` — 页面结构、布局模式、格式规范（权威）
2. **辅技能**: `.agents/skills/marp-slide/SKILL.md` — 通用设计原则（仅借鉴以下部分）

### 从 marp-slide 借鉴的规则

- 标题简洁：h2 标题控制在 15–25 字，避免冗长
- 要点密度：每页正文 3–5 条要点，过多时拆分页面
- 留白意识：内容不要填满整个 `.chapter-body`，保持呼吸感
- 视觉层次：重要数据（如 2.1 dB、19.2 dB、98.5%）用卡片或 callout 突出

### 明确的禁止（marp-slide 规则不适用）

- ❌ 不使用 marp-slide 的 7 套主题 CSS（始终用 buaa.css）
- ❌ 不使用 `<!-- _class: lead -->` 等 marp-slide 页面类型
- ❌ 不使用 `![bg right:40%]` 等 Marp 原生图片语法（始终用 `.hm-fig` 容器）
- ❌ 不改变 BUAA 的 5 种 page type + 8 种 layout mode 体系
