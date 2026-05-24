# BUAA Marp 布局模板库

> 本文件包含 12 个完整布局模板（A-K + C-split），按需加载。使用时从 SKILL.md 决策树选定布局后，复制对应模板替换 `{...}` 占位符。

---

## 布局 A：文左图右 (buaa-split--2) — ⭐ 图文默认布局

适用：文字 + 照片/渲染图/封面图/散文段落/bullet列表。

```html
<!-- _class: buaa-chapter -->

<style scoped>
/* === 图片尺寸 === */
/* 图片最大高度 */
.buaa-hm-fig img { max-height: {480-520}px !important; }
/* === 文本密度调节 === */
section {
  --text-p-size: 26px;
  --text-p-line-height: 2;
}
/* 图片：最大高度 */
/* .adj-img { max-height: {480-520}px !important; } */
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

---

## 布局 B：纯文字嵌套列表 (buaa-layout--flow + ol/ul)

适用：ol 主条目内含 ul 子条目，末尾有 buaa-callout 总结。

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

<ol>
  <li><strong>{主条目1}</strong>
    <ul>
      <li><strong>{子条目名}：</strong>{描述}</li>
      <li><strong>{子条目名}：</strong>{描述}</li>
      <li><strong>{子条目名}：</strong>{描述}</li>
    </ul>
  </li>
  <li><strong>{主条目2}</strong></li>
  <li><strong>{主条目3}</strong></li>
  <li><strong>{主条目4}</strong></li>
</ol>

<div class="buaa-callout">
<strong>总结：</strong>{总结语}
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

适用：两类并列内容，各 3~5 个条目，末尾一句总结。

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
  <li><strong>{条目名}。</strong></li>
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

适用：目标说明 + bullet列表 + 表格 + 图注。

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
/* === 图片尺寸 === */
/* 图片最大高度 */
.buaa-hm-fig img { max-height: {250-350}px !important; }
/* === 文本密度调节 === */
section {
  --text-p-size: 28px;
  --text-p-line-height: 2;
}
/* === 图文间距 === */
/* 文字与图片之间的间距 */
.buaa-split-tb { gap: 1px; }
/* 图片：最大高度 */
/* .adj-img { max-height: {250-350}px !important; } */
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

## 布局 J：含 strong 标题的无序列表 (buaa-layout--flow + ul)

适用：strong 小标题 + 说明文字；多个 strong 块 + ul 子列表混合。

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

<strong>{小标题1}</strong>

{说明段落 — 裸文字}

<ul>
  <li>{特点一}</li>
  <li>{特点二}</li>
  <li>{特点三}</li>
</ul>

<strong>{小标题2}</strong>

{说明段落}

<ul>
  <li>{特点一}</li>
  <li>{特点二}</li>
  <li>{特点三}</li>
</ul>

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
/* === 图片尺寸 === */
/* 图片最大高度 */
.buaa-hm-fig img { max-height: 520px !important; }
/* === 文本密度调节 === */
section {
  --text-p-size: 26px;
  --text-p-line-height: 1.5;
}
/* 图片：最大高度 */
/* .adj-img { max-height: 520px !important; } */
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
