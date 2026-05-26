# BUAA Marp 布局模板库

> 本文件包含 12 个完整布局模板（A-K + C-split），按需加载。使用时从 SKILL.md 决策树选定布局后，复制对应模板替换 `{...}` 占位符。

---

## 布局 A：图文两列 50:50 (buaa-split--2) — ⭐ 图文默认布局

适用：文字 + 照片/渲染图/封面图/散文段落/bullet列表。

**重要**：左文右图与左图右文两种排布方式**随机选择**，不固定使用某一种，以增加版面的视觉多样性。

### 变体 A1：左文右图

```html
<!-- _class: buaa-chapter -->

<style scoped>
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: {80-95}% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
  transform: translateY(0px);
}
/* === 文本密度调节 === */
section {
  --text-p-size: 26px;
  --text-p-line-height: 2;
}
/* 图片缩放比例、垂直偏移 */
/* .buaa-hm-fig img { max-width: 90% !important; transform: translateY(-55px); } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

{散文段落或 bullet 列表 — 裸文字，不用 <p> 包裹}

</div>

<div class="buaa-hm-fig">

<img src="{图片路径}">

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

### 变体 A2：左图右文

与 A1 相同，仅将 `<div class="buaa-hm-fig">` 与 `<div>` 文本块**交换位置**即可。

```html
<!-- _class: buaa-chapter -->

<style scoped>
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: {80-95}% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
  transform: translateY(0px);
}
section {
  --text-p-size: 26px;
  --text-p-line-height: 2;
}
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div class="buaa-hm-fig">

<img src="{图片路径}">

</div>

<div>

{散文段落或 bullet 列表}

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 B：纯文字嵌套列表 (buaa-layout--flow + 原生 Markdown 列表)

适用：ol 主条目内含 ul 子条目，末尾有 buaa-callout 总结。**使用 Markdown 原生列表语法**，`$...$` 公式和 `**加粗**` 均正常生效。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
/* 有序列表 */
ol { font-size: 22px; line-height: 3; }
/* 有序列表条目 */
ol li { font-size: 22px; margin-bottom: 4px; }
/* 嵌套无序列表 */
ol ul { font-size: 21px; line-height: 2; }
/* 嵌套列表条目 */
ol ul li { font-size: 21px; margin-bottom: 3px; }
/* 底部总结框 */
.buaa-callout { font-size: 22px; }
/* 列表：字号、行距 */
/* .adj-list { font-size: 22px; line-height: 2; } */
/* buaa-callout：字号、行距、内边距 */
/* .adj-buaa-callout { font-size: 22px; line-height: 1.8; padding: 14px 24px; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--flow">

{散文段落 — 裸文字，支持 $...$ 公式}

1. **{主条目1}**
   - **{子条目名}：**{描述，支持 $...$ 公式}
   - **{子条目名}：**{描述}
2. **{主条目2}**
3. **{主条目3}**

{散文段落或表格，列表与段落间保留空行}

<div class="buaa-callout">
{总结语，公式用 &lt;i&gt;x&lt;/i&gt;&lt;sub&gt;1&lt;/sub&gt; 替代}
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 C：居中混排 (buaa-layout--center + .buaa-text-block + table)

适用：散文段落 + 表格 + 特点总结，或纯表格居中。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
section {
  --text-p-size: 26px;
  --text-p-line-height: 1.7;
}
/* 文本块：字号、行距、颜色 */
/* .adj-txt { font-size: 24px; line-height: 1.8; color: #333; } */
/* 表格：字号 */
/* .adj-tbl { font-size: 22px; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-text-block adj-txt">
{散文段落 — 裸文字}
</div>

<br>

| 列1 | 列2 | 列3 |
| :--- | :---: | :---: |
| {数据} | {数据} | {数据} |

<br>

<div class="buaa-text-block adj-txt">
{总结性文字，含 <strong>高亮词</strong>}
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 C-split：窄表格分栏 (buaa-split--2 buaa-split--top)

适用：窄表格（≤3列）+ 配套文字/列表。**必须用 split-2 分栏**，居中布局会产生滚动条。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
section { --text-p-size: 22px; --text-p-line-height: 1.6; }
p { font-size: var(--text-p-size); }
/* 分栏内表格 */
.buaa-split--2 table { margin: 0 auto; }
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

<strong>{左侧分类标题}</strong>

| 属性 | 默认值 |
| :--: | :--: |
| {行1} | {值1} |
| {行2} | {值2} |
| {行3} | {值3} |
| {行4} | {值4} |

</div>

<div>

<strong>{右侧分类标题}</strong>

- {配套条目一}
- {配套条目二}
- {配套条目三}
- {配套条目四}

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 D：双栏对比 (buaa-split--2 + buaa-split--top + buaa-callout)

适用：两类并列内容，各 3~5 个条目，末尾一句总结。⚠️ 列表嵌入 `buaa-split--2 > div` 内部，只能使用 HTML `<ol><li>` + `<strong>`，公式用 `<i>x</i><sub>1</sub>` 替代。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* 左右两列的分类标题 */
.buaa-split--2.buaa-split--top > div > strong {
  display: block;
  font-size: 24px;
  color: #004F9E;
  margin-bottom: 8px;
}
/* 两列中的有序列表 */
.buaa-split--2 ol {
  font-size: 19px;
  line-height: 2.4;
  padding-left: 26px;
  margin: 0;
}
/* 两列中的列表条目 */
.buaa-split--2 ol li {
  font-size: 19px;
  margin-bottom: 5px;
  color: #444;
}
/* 列表条目标题 */
.buaa-split--2 ol li strong {
  font-size: 19px;
}
/* 底部总结框 */
.buaa-callout {
  font-size: 22px;
  margin-top: 10px;
  margin-bottom: 0;
}
/* 列表：字号、行距 */
/* .adj-list { font-size: 19px; line-height: 2.2; } */
/* buaa-callout：字号、行距 */
/* .adj-buaa-callout { font-size: 22px; line-height: 1.8; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

<strong>{分类一标题}：</strong>

<ol>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}</strong></li>
</ol>

</div>

<div>

<strong>{分类二标题}：</strong>

<ol>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}：</strong>{描述}</li>
  <li><strong>{条目名}：</strong>{描述}</li>
</ol>

</div>

</div>

<div class="buaa-callout">
<strong>总结：</strong>{总结语}
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 E：居中混排含列表 (buaa-layout--center + .buaa-text-block + ul + table)

适用：目标说明 + bullet列表 + 表格 + 图注。⚠️ 列表嵌入 `.buaa-text-block` 内部时只能使用 HTML `<ul><li>` + `<strong>`，公式用 `<i>x</i><sub>1</sub>` 替代。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
/* 文本块（标题+段落） */
.buaa-text-block { font-size: 24px; line-height: 1.7; }
/* 文本块中的列表 */
.buaa-text-block ul { font-size: 22px; line-height: 1.6; }
/* 文本块中的列表条目 */
.buaa-text-block ul li { font-size: 22px; margin-bottom: 5px; }
/* 文本块：字号、行距 */
/* .adj-txt { font-size: 24px; line-height: 1.8; } */
/* 表格：字号 */
/* .adj-tbl { font-size: 22px; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-text-block">
<strong>{标题性文字}</strong>

<ul>
  <li>{要点一}</li>
  <li>{要点二}</li>
  <li>{要点三}</li>
</ul>
</div>

| 名称 | 级别 | 数值 |
| :--- | :---: | :--- |
| {行1} | {级别} | {值} |
| {行2} | {级别} | {值} |

<div class="buaa-hm-cap">{图注/表注文字}</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 F：文上图下 (buaa-split-tb) — 技术大图专用

适用：文字 ≤ 180字 + 技术原理图/曲线图/框图需全宽展示细节。

```html
<!-- _class: buaa-chapter -->

<style scoped>
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: {80-95}% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
  transform: translateY(0px);
}
/* === 文本密度调节 === */
section {
  --text-p-size: 28px;
  --text-p-line-height: 2;
}
/* === 图文间距 === */
/* 文字与图片之间的间距 */
.buaa-split-tb { gap: 1px; }
/* 图片缩放比例、垂直偏移 */
/* .buaa-hm-fig img { max-width: 90% !important; transform: translateY(-55px); } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split-tb">

<div>

{≤180字的散文段落。公式用 $...$ 裸写，不用 <p> 包裹}

</div>

<div class="buaa-hm-fig">

<img src="{图片路径}">

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 G：流程图 (buaa-flow-chart)

触发：大纲中 `流程图（纵向）：\n  → 步骤1\n  → 步骤2` 独占行 + 缩进 `→` 行。步骤3~9个。

箭头类型：`buaa-arrow--line-long buaa-arrow--line-long-down`（带箭尾线+箭头尖）。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
/* 流程图全局变量 */
.buaa-flow-chart {
  --fc-font-size: {18-22}px;
  --fc-min-width: {280-520}px;
  --arr-length: 30px;
  --line-width: 2px;
  --arr-color: var(--buaa-primary);
}
/* 箭头样式微调：长/粗/颜色 */
/* .adj-fc-arrow { --arr-length: 40px !important; --line-width: 3px !important; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-flow-chart">

<div class="buaa-flow-chart__node">{步骤1}</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">{步骤2}</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">{步骤3}</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">{步骤4}</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">{步骤5}</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

### 箭头参数速查

| 变量/属性 | 控制目标 | 默认值 |
|-----------|:--------:|:------:|
| `--arr-length` | 箭头线长度 | 24px (line) / 60px (line-long) |
| `--line-width` | 线条粗细 | 2px |
| `--arr-color` | 箭头颜色 | var(--buaa-primary) |
| `.buaa-flow-chart__arrow { margin }` | 箭头与节点间距 | 默认 4px 0 |

推荐通过 margin 控制节点间距：`.buaa-flow-chart__arrow { margin: 8px 0 24px 0; }`（上 8px 贴上方节点，下 24px 与下方节点拉开）。

---

## 布局 H：系统框图 (buaa-block-diagram)

触发：大纲中 `系统框图：\n  center: 枢纽\n  left: A → B\n  right: C\n  top: D\n  bottom: E → F`。
⚠️ Hub 只在 `buaa-block-diagram__center` 渲染一次，链中不重复。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
.buaa-block-diagram {
  --bd-node-font-size: 18px;
  --bd-hub-font-size: 36px;
  --bd-gap: 10px;
  --arr-color: #004F9E;
  --arr-length: 40px;
  --line-width: 2px;
  --node-pad-x: 20px;
  --node-pad-y: 10px;
  --arr-gap-x: 20px;
  --arr-gap-y: 10px;
}
.buaa-block-diagram__node { padding: var(--node-pad-y) var(--node-pad-x) !important; }
.buaa-block-diagram__chain:not(.buaa-block-diagram__chain--vertical) .buaa-block-diagram__arrow {
  margin-left: var(--arr-gap-x) !important; margin-right: var(--arr-gap-x) !important;
}
.buaa-block-diagram__chain.buaa-block-diagram__chain--vertical .buaa-block-diagram__arrow {
  margin-top: var(--arr-gap-y) !important; margin-bottom: var(--arr-gap-y) !important;
}

/* 节点微调 */
.n-top   { margin-bottom: 20px; margin-top: 20px; }
.n-gen   { margin-left: 30px;  margin-right: 10px; }
.n-tline { margin-left: 10px;  margin-right: 10px; }
.n-dc    { margin-left: 1px;   margin-right: 30px; }
.n-probe { margin-top: 2px;    margin-bottom: 10px; }
.n-scope { margin-bottom: 20px; }

/* 箭头自定义 */
.a-top     { --arr-length: 30px;  --line-width: 4px; }
.a-l-mid   { --arr-length: 50px;  --line-width: 4px; }
.a-l-end   { --arr-length: 25px;  --line-width: 4px; }
.a-r       { --arr-length: 200px; --line-width: 4px; }
.a-bot-end { --arr-length: 30px;  --line-width: 4px; }
.a-bot-mid { --arr-length: 30px;  --line-width: 4px; }

/* 底部说明 */
.buaa-callout { font-size: 20px; line-height: 2; padding: 12px 22px; margin-top: 6px; }
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-block-diagram">

  <div class="buaa-block-diagram__top">
    <div class="buaa-block-diagram__chain buaa-block-diagram__chain--vertical">
      <div class="buaa-block-diagram__node n-top">{上部节点}</div>
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-up a-top"></div>
    </div>
  </div>

  <div class="buaa-block-diagram__left">
    <div class="buaa-block-diagram__chain buaa-block-diagram__chain--spread">
      <div class="buaa-block-diagram__node n-gen">{左节点1}</div>
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-right buaa-arrow--fill a-l-mid"></div>
      <div class="buaa-block-diagram__node n-tline">{左节点2}</div>
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-right a-l-end"></div>
    </div>
  </div>

  <div class="buaa-block-diagram__center">
    <div class="buaa-block-diagram__hub">{枢纽节点}</div>
  </div>

  <div class="buaa-block-diagram__right">
    <div class="buaa-block-diagram__chain">
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-left a-r"></div>
      <div class="buaa-block-diagram__node n-dc">{右节点}</div>
    </div>
  </div>

  <div class="buaa-block-diagram__bottom">
    <div class="buaa-block-diagram__chain buaa-block-diagram__chain--vertical">
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-up a-bot-end"></div>
      <div class="buaa-block-diagram__node n-probe">{下节点1}</div>
      <div class="buaa-block-diagram__arrow buaa-arrow--line-long buaa-arrow--line-long-up a-bot-mid"></div>
      <div class="buaa-block-diagram__node n-scope">{下节点2}</div>
    </div>
  </div>

</div>

<div class="buaa-callout">
<strong>{组件1}：</strong>{说明1} &nbsp;|&nbsp;
<strong>{组件2}：</strong>{说明2} &nbsp;|&nbsp;
<strong>{组件3}：</strong>{说明3} &nbsp;|&nbsp;
<strong>{组件4}：</strong>{说明4} &nbsp;|&nbsp;
<strong>{组件5}：</strong>{说明5}
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 I：双图并排 (buaa-img-pair + buaa-hm-cap)

适用：正文段落 + 两张图并排，各有图注。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
/* 段落文字 */
p { font-size: 24px; line-height: 1.7; }
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--flow">

{散文段落 — 裸文字，支持 $...$ 公式}

<div class="buaa-img-pair">

<div>

<img src="{图片1路径}">

</div>

<div>

<img src="{图片2路径}">

<div class="buaa-hm-cap">{图注文字}</div>

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 J：含 strong 标题的无序列表 (buaa-layout--flow + 原生 Markdown 列表)

适用：strong 小标题 + 说明文字；多个 strong 块 + ul 子列表混合。**使用 Markdown 原生列表**，`$...$` 和 `**text**` 正常生效。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 文本密度调节 === */
/* 无序列表 */
ul { font-size: 22px; line-height: 1.6; }
/* 无序列表条目 */
ul li { font-size: 22px; line-height: 2; margin-bottom: 6px; }
/* 列表：字号、行距 */
/* .adj-list { font-size: 22px; line-height: 2; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--flow">

**{小标题1}**

{说明段落 — 裸文字，支持 $...$}

- {特点一，支持 $...$ 公式}
- {特点二}
- {特点三}

**{小标题2}**

{说明段落}

- {特点一}
- {特点二}
- {特点三}

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```

---

## 布局 K：纯大图 (buaa-layout--center + buaa-hm-fig)

适用：整页仅一张大图，无文字或仅标题。

```html
<!-- _class: buaa-chapter -->

<style scoped>
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: {90-95}% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
}
/* === 文本密度调节 === */
section {
  --text-p-size: 26px;
  --text-p-line-height: 1.5;
}
/* 图片缩放比例 */
/* .buaa-hm-fig img { max-width: 95% !important; } */
</style>

<div class="buaa-chapter__badge"><span>{编号}</span></div>

## {主标题}——{副标题}

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-hm-fig">

<img src="{图片路径}">

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">{N}</div>
```



---

## 附录：图片宽高比保持模式

> 自 v3 起，所有含图片的布局（A / F / I / K）统一采用此 Grid 居中 + 双向约束模式，取代旧版固定 max-height 方案。

### 为什么替换旧方案

旧方案 `max-height: 480px` 强制限制图片高度，会导致宽高比与原文不一致的图片被拉伸或纵向截断。新方案用 `max-width` + `max-height` 的双向约束配合 `width/height: auto`，浏览器在可用空间内保持原始宽高比缩放。

### 核心 CSS 模板

```css
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: {80-95}% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
  transform: translateY(0px);
}
```

### 参数速查

| 参数 | 默认值 | 用途 | 调整场景 |
|------|:---:|------|------|
| `max-width` | 80% | 图片占容器宽度的最大比例 | 图片偏小时调大至 90-95% |
| `max-height` | 100% | 图片占容器高度的最大比例 | 纵向太扁时减小（如 85%） |
| `transform: translateY` | 0px | 垂直微调，负值上移 | 图片整体偏下时设置 -30~-60px |

### 样式优先级

本模式使用 `!important` 确保覆盖 `buaa.css` 全局主题的 `max-height` 默认约束。务必保持四个属性（`max-width`、`max-height`、`width: auto`、`height: auto`）同时存在且带 `!important`，缺失任一可能导致宽高比失真。

### 实战示例（文左图右 + 表格曲线图）

```css
.buaa-hm-fig {
  display: grid !important;
  place-items: center !important;
}
.buaa-hm-fig img {
  max-width: 90% !important;
  max-height: 100% !important;
  width: auto !important;
  height: auto !important;
  transform: translateY(-55px);
}
```

效果：图片占右侧列 90% 宽度，保持原始宽高比，在列内水平+垂直居中，向上偏移 55px 平衡视觉重心。
