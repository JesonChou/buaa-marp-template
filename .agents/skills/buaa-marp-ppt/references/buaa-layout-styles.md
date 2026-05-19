# BUAA Marp 布局排版风格参考

> 从 `presentation-template.md` 与多个实际项目 PPT 中提炼的结构化排版规范。
> 生成新 PPT 时，所有内容页必须从以下布局模式中选择，不得使用裸 `<div>` 自由发挥。

---

## 一、页面骨架（5 种 page type）

每个 PPT 必须按以下顺序组织页面类型：

```
封面(cover) → 目录(catalog) → 过渡(transition) → 正文(chapter)×N → 过渡 → 正文×N → ... → 结尾(end)
```

| 类型 | Marp 指令 | 页码 | 说明 |
|------|-----------|:---:|------|
| 封面 | `<!-- _class: cover -->` | ✗ | Logo + 主副标题 + 汇报人/日期 |
| 目录 | `<!-- _class: catalog -->` | ✗ | 大字"目录" + 编号列表，`ul { left: 730px }` |
| 过渡 | `<!-- _class: transition -->` | ✗ | 深蓝全幅 + 章节大数字 + 中/英文标题 |
| 正文 | `<!-- _class: chapter -->` | ✓ | badge 编号 + `##` 标题 + 内容体 + footer-bar |
| 结尾 | `<!-- _class: end -->` | ✓ | badge"结语" + 感谢 + Q&A |

---

## 二、正文页布局模式（9 种）

### 模式 A：文左图右（split-2）⭐ 图文默认布局

**适用：** 所有文字+图片左右并排场景的<strong>默认布局</strong>（50:50）。包括：
- 散文段落（无 bullet，任意长度）+ 任意图片 → **永远用 split-2**
- bullet 列表（≤5 条）+ 任意图片 → **首选 split-2**，通过缩小字号解决溢出
- 3 条短要点（每条 ≤40 字），配一张示意图
- 照片/渲染图/封面图 + 任意文字 → **split-2（50% 宽对照片足够）**

> ⚠️ 经验证：split-2 是图文左右并排场景中<strong>覆盖最广、视觉最优</strong>的选择。

**模板：**
```html
<div class="chapter-body layout-center">
<div class="split-2 split-center">
<div>
- 要点一
- 要点二
- 要点三
</div>
<div class="hm-fig">
<img src="...">
<div class="hm-cap">图注</div>
</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 概念介绍 + 证据图、技术概述 + 示意图、散文段落 + 重要图表

---

### 模式 B：文宽图窄（split-right）⚠️ 最后手段

**适用：** <strong>仅作为最后手段</strong>，同时满足以下 ALL 条件时才使用（68:32）：
1. 内容是 **bullet 列表**（不是散文段落）
2. 列表条目 **≥4 条**，且多条 **>60 字**
3. 图片是 **辅助示意图**（不是核心证据图），在 32% 宽度下仍可辨认
4. 已尝试 split-2 + 缩小字号至 **19px**，文字仍然溢出

**以下情况绝对不用 split-right：**
- 散文段落 → 永远用 split-2
- 图片是核心证据/需要大尺寸 → 用 split-2
- 图片是技术原理图/曲线图 → 用 split-tb（上下布局）
- 列表条目 ≤3 条 → 用 split-2
- 照片/渲染图 → 用 split-2（50% 宽足够）

> ⚠️ 经验证：绝大多数图文左右并排场景用 split-2 均能完美胜任；split-right 仅在极端密集 bullet 列表 + 辅助示意图时作为最后手段使用。

**模板：**
```html
<div class="chapter-body layout-center">
<div class="split-right split-center">
<div>
- 要点一（可较长）
- 要点二（可较长）
- 要点三（可较长）
</div>
<div class="hm-fig">
<img src="...">
<div class="hm-cap">图注</div>
</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**决策规则（多步判断，从优先到降级）：**
1. 先看内容形态：散文段落 → **split-2**（无条件，50:50）
2. 再看图片权重：核心证据图 / 照片 / 需大尺寸 → **split-2**（不牺牲图片空间）
3. 图片是技术原理图/曲线图/框图 → 考虑 **split-tb**（上下布局，全宽展示）
4. bullet 列表 ≤3 条 → **split-2**
5. bullet 列表 3~5 条，部分 >40 字 → **split-2 + 字号降至 20px**
6. bullet 列表 >5 条 → **优先拆分页面**；仍不行才考虑 split-right

**补充：上下布局（split-tb）— 文上图下，图需全宽**

当图片为技术原理图/曲线图/框图，需要全宽展示细节时，使用 `split-tb`。文字在上方自适应高度，图片在下方填满剩余空间。

**触发条件（必须满足）：**
- 图片类型为以下之一：技术原理图（含标注/箭头/多组件）、数据曲线图（含多曲线/坐标轴）、流程图/框图（非 I/J 模式生成）
- 文字量不超过对应上限：技术原理图 ≤180 字、曲线图 ≤150 字、流程图 ≤120 字
- 内容自然顺序为"先说明，再看图"

**以下情况不用 split-tb（用 split-2 代替）：**
- 图片是照片/渲染图/封面图 → split-2（50% 宽足够）
- 文字 > 200 字 → split-2（文字多时并排更高效，文图各占一半）
- 文字是 bullet 列表形态 → 优先 split-2

**模板：**
```html
<div class="chapter-body layout-center">
<div class="split-tb">
<div>
  <p>简短说明文字（≤180 字，全宽 2~4 行）。</p>
</div>
<div class="hm-fig">
<img src="...">
<div class="hm-cap">图注</div>
</div>
</div>
</div>
```

**实例：** 技术原理说明 + 电路图、波形分析 + 数据曲线图、数据采集说明 + 曲线图

**split-tb 完整 scoped CSS 模板（必须同时包含以下三块）：**

```html
<style scoped>
/* === 图片尺寸 === */
/* 图片最大高度 */
.hm-fig img { max-height: XXXpx !important; }
/* === 文本密度调节 === */
section {
  /* 段落/文本块字号 */
  --text-p-size: XXpx;
  /* 段落/文本块行距 */
  --text-p-line-height: X.X;
}
/* === 图文间距 === */
/* 文字与图片之间的间距 */
.split-tb { gap: 1px; }
/* 图片：最大高度 */
/* .adj-img { max-height: XXXpx !important; } */
</style>
```

| 内容形态 | --text-p-size | --text-p-line-height | 图片 max-height | 典型场景 |
|----------|:---:|:---:|:---:|------|
| 短文字(≤100字) + 技术大图 | 28px | 2 | 300px | 技术原理页：电路图、测试系统图 |
| 中等文字(100~180字) + 图 | 28px | 1.5 | 250px | 波形分析页：波形图、数据曲线 |
| 短文字 + 特大图（图占主导） | 26px | 1.5 | 480px | 核心图表页：I-V 曲线、频谱图 |

---

### 模式 C：三卡片 + 图廊 — 概念并列

**适用：** 3 个并列概念，每个配 1 句说明，底部 3 张图（无图注）

**模板：**
```html
<div class="chapter-body layout-flow">
<div class="card-grid">
<div class="card card-3">
<div class="card-icon">🔬</div>
<div class="card-title">标题</div>
<div class="card-body">一句话描述。</div>
</div>
<!-- ×3 -->
</div>
<div class="img-gallery gal-3">
<img src="...">
<img src="...">
<img src="...">
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 三大技术方向并列展示、三阶段方案对比

---

### 模式 D：三卡片 + 单图 — 方法对比

**适用：** 3 个技术方法并列对比，底部一张总结图

**模板：**
```html
<div class="chapter-body layout-flow">
<div class="card-grid">
<div class="card card-3">
<div class="card-icon">🎯</div>
<div class="card-title">方法名</div>
<div class="card-body">简短描述 [ref]</div>
</div>
<!-- ×3 -->
</div>
<div class="hm-fig">
<img src="...">
<div class="hm-cap">图注</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 三种方法对比 + 总结示意图

---

### 模式 E：三卡片 + 双图并排 — 趋势展示

**适用：** 3 个挑战/趋势卡片，底部 2 张图并排（各有图注）

**模板：**
```html
<div class="chapter-body layout-flow">
<div class="card-grid">
<div class="card card-3">...</div>
<!-- ×3 -->
</div>
<div class="img-pair">
<div>
<img src="...">
<div class="hm-cap">图注左</div>
</div>
<div>
<img src="...">
<div class="hm-cap">图注右</div>
</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 三大挑战 + 双趋势图、技术进步展示

---

### 模式 F：时间轴 + 提示框 — 历史演进

**适用：** 展示技术发展历程（5 个里程碑 + 总结句）

**模板：**
```html
<div class="chapter-body layout-center">
<div class="split-tb">
<div class="timeline">
<div class="t-node">
<div class="t-dot"></div>
<div class="t-label">年份</div>
<div class="t-desc">事件描述</div>
</div>
<!-- ×5 -->
</div>
<div class="callout">
<strong>关键转折：</strong>总结性说明文字。
</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 技术发展历程（如：1865→1966→1980s→1990s→2020s）

---

### 模式 G：图标列表 + 右侧图 — 总结页

**适用：** 4 条总结要点，每条配图标，右侧一张展望图

**模板：**
```html
<div class="chapter-body layout-flow">
<div class="split-right split-center">
<div>
<ul class="icon-list">
<li><span class="li-icon">✅</span> 总结一</li>
<li><span class="li-icon">⚠️</span> 总结二</li>
<li><span class="li-icon">🧠</span> 总结三</li>
<li><span class="li-icon">🌟</span> 总结四</li>
</ul>
</div>
<div class="hm-fig">
<img src="...">
<div class="hm-cap">图注</div>
</div>
</div>
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

**实例：** 四大总结要点 + 展望图

---

### 模式 H：双栏对比 + 底部总结（split-2 + callout）— 分类对照

**适用：** 两类并列内容（如"通用方法 vs 硬件方法"、"优点 vs 缺点"），各有 3–5 个条目，末尾有一句总结。当单列流式会导致内容溢出时自动触发。

**触发条件：**
- 大纲中出现两类并列分类标题（如"通用… / 硬件…"、"优点 / 缺点"、"理论 / 应用"）
- 每类 ≥3 个条目且有较长描述文字
- 末尾有总结性语句（如"总结：…"、"核心是…"）

**模板：**
```html
<div class="chapter-body layout-center">

<div class="split-2 split-top">

<div>
<strong>分类一标题：</strong>
<ol>
  <li><strong>条目名：</strong>描述文字。</li>
  <!-- ×3~5 -->
</ol>
</div>

<div>
<strong>分类二标题：</strong>
<ol>
  <li><strong>条目名：</strong>描述文字。</li>
  <!-- ×3~5 -->
</ol>
</div>

</div>

<div class="callout">
<strong>总结：</strong>总结性语句。
</div>

</div>
```

**内容密集时**，加 `<style scoped>` 压缩字号和行距（推荐参数见下方 CSS）：

```css
/* 左右两列的分类标题 */
.split-2.split-top > div > strong {
  display: block;
  font-size: 24px;
  color: #004F9E;
  margin-bottom: 8px;
}
/* 两列中的有序列表 */
.split-2 ol {
  font-size: 19px;
  line-height: 2.4;
  padding-left: 26px;
  margin: 0;
}
/* 两列中的列表条目 */
.split-2 ol li {
  font-size: 19px;
  margin-bottom: 5px;
  color: #444;
}
/* 底部总结框 */
.callout {
  font-size: 22px;
  margin-top: 10px;
  margin-bottom: 0;
}
```

**实例：** 通用方法 vs 硬件方法对比、优点 vs 缺点对照

---

### 模式 I：流程图（flow-chart）— 步骤串接

**适用：** 大纲中以 `buaa-diagram:flowchart` 代码块描述的 3~9 个串行步骤。每个步骤渲染为圆角矩形节点，节点间用向下实心三角箭头连接。

**触发条件：**
- 大纲中出现 ` ```buaa-diagram:flowchart` 代码块
- 每行一个步骤，步骤间无额外分隔符
- 也兼容旧格式：大纲行以 `流程图：` 开头，步骤以 `$\rightarrow$` 或 `->` 分隔

**模板：**
```html
<div class="chapter-body layout-center">
<div class="flow-chart">
  <div class="fc-node">步骤一</div>
  <div class="fc-arrow arr-solid arr-solid-down"></div>
  <div class="fc-node">步骤二</div>
  <div class="fc-arrow arr-solid arr-solid-down"></div>
  <!-- ... -->
</div>
</div>
```

**样式变量（在 `<style scoped>` 中覆写）：**
| 变量 | 默认值 | 说明 |
|------|:---:|------|
| `--fc-font-size` | 22px | 节点字号 |
| `--fc-min-width` | 520px | 节点最小宽度 |
| `--arr-color` | #004F9E | 箭头颜色 |

**箭头样式切换：** 流程图默认使用 `arr-solid-down`。如需更换箭头风格，将 `arr-solid arr-solid-down` 替换为：
- `arr-outline arr-outline-down` — 空心 V 形（现代科技风）
- `arr-line arr-line-down` — 细线+小箭头（学术简约风）

**大綱输入示例（新格式）：**
````markdown
```buaa-diagram:flowchart
选择被测回路并确定导通点
设置脉冲宽度
设置TLP幅值范围、增大步进、数字源表偏置电压等
TLP向DUT发送单个脉冲
获得I-V曲线与漏电流曲线
```
````

**大綱输入示例（旧格式，兼容）：**
```
流程图：选择被测回路并确定导通点$\rightarrow$设置脉冲宽度$\rightarrow$设置TLP幅值范围...
```

**实例：** 测试流程——从初始步骤到最终结果的完整步骤链

---

### 模式 J：系统框图（block-diagram）— 中心枢纽式

**适用：** 大纲中以 `buaa-diagram:block` 代码块描述的中心枢纽 + 四向节点链系统框图。中心为深蓝填充的枢纽节点，上下左右四个方向各放置一条节点链（白底蓝边框圆角矩形），链内节点间用箭头连接。

**触发条件：**
- 大纲中出现 `系统框图：` 独占一行，后续为缩进的方向行
- 每行格式：`方向: 节点1 → 节点2 → ...`（链中保留 Hub 节点）
- `center:` 行声明枢纽节点
- 方向词：`left` / `right` / `top` / `bottom`（可选）
- 也兼容旧格式：`系统框图关系：` 开头的方向标注行

**Hub 位置 → 箭头方向规则：**
| Hub 在链中位置 | 语义 | 箭头方向 | 示例 |
|:---:|------|:---:|------|
| 链**末尾** | 从外流入中心（向心） | 指向 Hub | `left: A → B → Hub` |
| 链**开头** | 从中心流向外（离心） | 从 Hub 出发 | `top: Hub → 探针台` |

- `center:` 声明枢纽（必填），AI 自动在各链中去重渲染
- 位置决定链排列方向：`left`/`right` → 横向 flex row；`top`/`bottom` → 纵向 flex column

**模板：**
```html
<div class="chapter-body layout-center">
<div class="block-diagram">
  <div class="bd-top">
    <div class="bd-chain">
      <div class="bd-node">上部节点</div>
    </div>
  </div>
  <div class="bd-left">
    <div class="bd-chain">
      <div class="bd-node">左节点1</div>
      <div class="bd-arrow arr-solid arr-solid-right"></div>
      <div class="bd-node">左节点2</div>
    </div>
  </div>
  <div class="bd-center">
    <div class="bd-hub">中心枢纽</div>
  </div>
  <div class="bd-right">
    <div class="bd-chain">
      <div class="bd-node">右节点</div>
    </div>
  </div>
  <div class="bd-bottom">
    <div class="bd-chain">
      <div class="bd-node">下节点1</div>
      <div class="bd-arrow arr-solid arr-solid-right"></div>
      <div class="bd-node">下节点2</div>
    </div>
  </div>
</div>
</div>
```

**样式变量（在 `<style scoped>` 中覆写）：**
| 变量 | 默认值 | 说明 |
|------|:---:|------|
| `--bd-node-font-size` | 18px | 普通节点字号 |
| `--bd-hub-font-size` | 22px | 枢纽节点字号 |
| `--bd-gap` | 12px | Grid 区域间距 |
| `--arr-color` | #004F9E | 箭头颜色 |

**大綱输入示例（新格式）：**
```
系统框图：
  center: 被测器件DUT
  left: 脉冲发生器 → 传输线 → 被测器件DUT
  right: 直流偏置/漏电流测量单元 → 被测器件DUT
  bottom: 高速示波器 → 电压、电流探头 → 被测器件DUT
  top: 被测器件DUT → 探针台（夹具）
```
- `left`/`right`/`bottom` 链中 Hub 在末尾 → **向心**箭头
- `top` 链中 Hub 在开头 → **离心**箭头
- AI 自动识别 `left`/`right` 为横向链、`top`/`bottom` 为纵向链

**大綱输入示例（旧格式，兼容）：**
```
左侧：脉冲发生器$\rightarrow$传输线$\rightarrow$被测器件DUT
下部：高速示波器$\rightarrow$电压、电流探头$\rightarrow$被测器件DUT
右侧：直流偏置/漏电流测量单元$\rightarrow$被测器件DUT
上部：被测器件DUT$\rightarrow$探针台（夹具）
```

**实例：** 测试系统组成——中心设备 + 四向外围模块

---

## 三、箭头样式库（arr-*）速查

流程图和系统框图中使用的箭头均来自 `buaa.css` 中的箭头样式库。以下为 5 种核心样式：

| 样式类 | 视觉效果 | 适用场景 |
|--------|----------|----------|
| `arr-solid-*` | 实心三角 ▶ | 默认风格，经典粗壮，适合流程步骤间的主连接 |
| `arr-outline-*` | 空心 V 形 ⪢ | 现代科技风，轻盈不喧宾夺主，适合框图节点间连接 |
| `arr-line-*` | 细线+小箭头 → | 学术简约风，尾长24px，适合紧凑型图表 |
| `arr-line-long-*` | 长尾细线 —→ | 长距离连接，尾长60px（可设 `--arr-length` 自定义），适合框图远距离箭头 |
| `arr-double-*` | 双线+三角头 ⇒ | 数据流/技术风格，线宽可设 `--arr-thick`（默认2px） |

每种样式有 4 个方向后缀：`-right` / `-left` / `-down` / `-up`。

尺寸修饰符：`.arr-sm`（缩小 0.7×）和 `.arr-lg`（放大 1.4×，仅 `arr-solid` / `arr-outline`）。

**箭头自动伸缩：** 在 `.bd-chain` 中给箭头添加 `.arr-fill` 类，箭头会 `flex: 1` 自动填充节点间剩余空间。搭配 `.bd-chain.bd-spread`（`justify-content: space-evenly`）可实现节点+箭头的均匀分布。

**CSS 变量调节（在 scoped 中覆写）：**
| 变量 | 默认 | 控制 |
|------|:---:|------|
| `--arr-color` | #004F9E | 所有箭头颜色 |
| `--arr-length` | 60px | `arr-line-long` / `arr-double` 尾长 |
| `--arr-thick` | 2px | `arr-double` 双线宽度 |

颜色通过 CSS 变量 `--arr-color` 控制（默认 `#004F9E`）。

---

## 四、图文自动生成：触发语法规范

当大纲中需要生成流程图或系统框图时，使用**自然语言缩进格式**——触发词独占一行，后续以缩进的 `→` 行列出内容。这比围栏代码块更自然，与大纲书写习惯一致。

### 流程图触发

```
流程图（纵向）：
  → 步骤1文本
  → 步骤2文本
  → 步骤3文本
```

| 标注 | 布局 | 箭头 | 适用 |
|------|------|------|------|
| `流程图（纵向）` | 垂直堆叠 | ↓ `arr-solid-down` | 步骤 ≥4 个，学术默认 |
| `流程图（横向）` | 水平并排 | → `arr-solid-right` | 步骤 ≤3 个，宽屏展示 |
| `流程图`（无标注） | **默认纵向** | ↓ `arr-solid-down` | 最简写法 |

- 触发词独占一行，后续行以 `→ ` 开头（两个空格缩进 + `→` + 空格）
- 步骤数：3~9 个
- 步骤文本自身含 `→` 时用 `\→` 转义
- 若某步骤文本过长（>30字），自动在 scoped 中缩小 `--fc-font-size`

### 系统框图触发

```
系统框图：
  center: 枢纽节点名
  left: 节点A → 节点B
  top: 节点C
  right: 节点D → 节点E
  bottom（纵向）: 节点F → 节点G → 节点H
```

**位置自动推断 + 单链独立覆盖：**

| 位置 | 链排列方向 | Hub 在末尾（向心） | Hub 在开头（离心） |
|:----:|:----------:|:---:|:---:|
| `left` | 横向 → | `arr-solid-right` | `arr-solid-left` |
| `right` | 横向 → | `arr-solid-right` | `arr-solid-left` |
| `top` | 纵向 ↑ | `arr-solid-up` | `arr-solid-down` |
| `bottom` | 纵向 ↑ | `arr-solid-up` | `arr-solid-down` |

- `center:` 行指定枢纽（必填）
- 方向行可选（`left` / `right` / `top` / `bottom`），链内节点用 `→` 分隔
- 绝大多数场景**不写方向标注**——位置本身就暗示了自然的链方向
- 仅当某条链需要反常规时才加 `（纵向）`/`（横向）`
- 某方向无链 → 对应 Grid area 自动为空

### 正文区分规则

```
✅ 触发图表：                     ❌ 不触发（普通正文）：
流程图：                          流程图：这是我们系统的工作流程，包括...
  → 步骤1                         （同行有后续正文，视为普通段落）
  → 步骤2
```

- **触发条件**：`流程图` 或 `系统框图` 独占一行，且后续紧跟缩进的 `→` 行
- **不触发**：同行后有正文，或无后续缩进 `→` 行

### 兼容旧格式

以下旧格式仍被识别，但不推荐在新大纲中使用：
- `流程图：A→B→C`（单行，`→` 分隔，退化为纵向流程图）
- `系统框图关系：` + `左侧：A→B→Hub` 等方向标注行（自动映射到新格式）
- `系统框图（横向链）：` / `系统框图（纵向链）：`（全局标注，自动转换为单链独立标注）

---

## 五、强制性排版规则

### 加粗
- ❌ 禁止在 `<div>` 内使用 `**text**`（Marp 不解析 HTML 块内 Markdown）
- ✅ 必须使用 `<strong>text</strong>`，buaa.css 已设 `strong { color: #004F9E; }`

### 图注
- ❌ 禁止 `*斜体图注*` 或 `.img-caption`（灰字，不符合规范）
- ✅ 必须使用 `<div class="hm-cap">图注文字</div>`（16px / #000 / bold / Microsoft YaHei）
- `<img>` 前后必须各留一空行，防止被 `<p>` 包裹

### 分栏
- 短要点 → `split-2`（50:50）
- 长要点 → `split-right`（68:32）
- 图在左文在右 → `split-left`（32:68）
- 垂直排列 → `split-tb`

### 目录
- `ul { left: 730px }` — 条目块在右半区（683→1366px）自然居中
- 不设 `width` — 让块宽由内容决定
- `gap: 28px` 控制纵向间距（条目多→减 gap，条目少→增 gap）
- `li { font-size: 24px }`

### 内容溢出处理
- **每个 chapter slide 必须附带文本密度调节块**，优先用 CSS 变量方式（简洁通用）
- buaa.css 已内置 5 个文本密度变量（`--text-size`/`--text-line-height`/`--text-item-gap`/`--text-p-size`/`--text-p-line-height`），覆写 `section { ... }` 即可全局生效
- 压缩后仍溢出 → 考虑拆分页面或切换到模式 H（双栏对比）
- 模板：`/* === 文本密度调节 === */` + `section { --text-size: 22px; ... }`

### 图片尺寸调节
- 核心证据图需要放大时，在 slide 级 `<style scoped>` 中覆写 `.hm-fig img { max-height: XXXpx !important; }`
- 不改 `buaa.css` 中的全局 `max-height: 320px`

### Marp 陷阱
- `<footer>` → 改用 `<div class="footer-bar">`
- 幻灯片内 `---` → 改用 `<hr>`
- `<img class/style>` → 改用父 div + CSS 选择器
- `width:100%` + padding → 加 `box-sizing: border-box`
