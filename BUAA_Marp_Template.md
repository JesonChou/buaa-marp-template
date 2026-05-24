---
marp: true
theme: buaa-green
paginate: false
---

<!-- _class: buaa-cover -->

<img class="buaa-cover__logo" src="./assets/logo.png">

# BUAA Marp PPT

## 通用大纲模板

<div class="buaa-cover__presenter">汇报人：XXX</div>
<div class="buaa-cover__date">2026年5月24日</div>
<div class="buaa-cover__decor">BEIHANG UNIVERSITY</div>

---

<!-- _class: buaa-catalog -->

<style scoped>
ul { left: 730px !important; display: flex !important; flex-direction: column !important; gap: 28px !important; }
li { font-size: 24px !important; margin-bottom: 0 !important; }
.buaa-catalog__num {
  /* background: linear-gradient(135deg, #004F9E, #0091ffff) !important; */
  border-radius: 6px !important;
}
</style>

<div class="buaa-catalog__title">目录</div>
<div class="buaa-catalog__line"></div>
<div class="buaa-catalog__eng">Contents</div>

<ul style="position:absolute;left:730px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:28px;list-style:none;z-index:2;padding:0;margin:0;">
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">01</span> 项目概述</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">02</span> 页面类型与布局系统</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">03</span> 样式体系详解</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">04</span> 增强组件库</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">05</span> 素材输入与排版输出</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">06</span> 快速上手流程</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">07</span> 模板样式说明</li>
</ul>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">01</div>

# 项目概述

## Project Overview

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 26px; --text-p-line-height: 2; }
</style>

<div class="buaa-chapter__badge"><span>1.1</span></div>

## 项目定位——什么是 BUAA Marp 模板项目

<div class="buaa-chapter__body buaa-layout--flow">

BUAA Marp 模板项目是一套基于 Marp 的北航主题演示文稿生成系统。用户只需提供文字、图片和表格数据，AI 即可自动完成排版，生成专业美观的 PPT。

<strong>项目特色：</strong>

<ol>
  <li>纯 Markdown 编写，专注内容创作，告别拖拽排版</li>
  <li>5 种页面类型：封面、目录、正文、过渡、结尾</li>
  <li>11 种正文布局，自动匹配内容形态</li>
  <li>集成 Awesome-Marp 增强组件库</li>
  <li>内置 AI Skill，一句话生成完整 PPT</li>
</ol>

<strong>核心原则：</strong>

用户提供完整素材，AI 负责辅助排版；大纲中没有的内容，AI 一律不自行添加。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">1</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
.buaa-flow-chart { --fc-font-size: 24px; --fc-min-width: 520px; --arr-length: 30px; --line-width: 4px; --arr-color: var(--buaa-primary); }
.buaa-flow-chart__arrow { margin: 8px 0 24px 0; }
/* 箭头样式微调：长/粗/颜色 */
/* .adj-fc-arrow { --arr-length: 40px !important; --line-width: 3px !important; } */
</style>

<div class="buaa-chapter__badge"><span>1.2</span></div>

## 工作流程——从大纲到 PPT

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-flow-chart">

<div class="buaa-flow-chart__node">用户按模板编写大纲（填入文字、图片路径、表格数据）</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">AI 逐页分析 {页面类型, 内容类型, 布局选择, 密度参数}</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">AI 生成 presentation.md（套用 buaa.css 主题样式）</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">用户在 VS Code 中预览（Ctrl+K V），微调 adj-* 占位符</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">导出为 PDF / PPTX / HTML</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">2</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 26px; --text-p-line-height: 1.7; }
</style>

<div class="buaa-chapter__badge"><span>1.3</span></div>

## 文件关系——三份文档的分工

<div class="buaa-chapter__body buaa-layout--center">

| 文档 | 面向对象 | 作用 |
| :--: | :--: | :--: |
| 本大纲模板 | 用户 | 定义大纲编写格式，供 AI 准确解析 |
| SKILL.md | AI | 11 种布局模板 + 决策树 + 生成流程 |
| copilot-instructions.md | AI | 16 条硬约束 + 常见陷阱速查 |

<br>

<div class="buaa-text-block">
<center><strong>工作区关键文件：</strong></center>
</div>

- themes/buaa.css — 完整主题样式（约1888行）
- .vscode/settings.json — 注册主题：markdown.marp.themes
- assets/ — logo.png、cover-bg.png、catalog-bg.png

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">3</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">02</div>

# 页面类型与布局系统

## Page Types & Layout System

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>2.1</span></div>

## 五种页面类型——骨架速查

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2-1 buaa-split--center">

<div>

| 页面类型 | CSS class | 用途 | 页码 |
| :--: | :--: | :--: | :--: |
| 封面 | buaa-cover | 首页，含 logo + 渐变蒙层 | 无 |
| 目录 | buaa-catalog | 左侧中文"目录" + 右侧章节列表 | 无 |
| 过渡 | buaa-transition | 深蓝全幅背景 + 大号章号 + 标题 | 无 |
| 正文 | buaa-chapter | 蓝色 badge + h2 标题 + footer 底部栏 | 有 |
| 结尾 | buaa-end | 结语 badge + 居中感谢文字 + Q&A | 有 |

</div>

<div>

<div class="buaa-text-block">
<strong>封面要素</strong>（全部可选，按需填写）：
</div>

- 主标题（必填，&le;20字）
- 副标题（&le;20字，未说明则不写）
- 汇报人、日期
- 装饰文字（固定 BEIHANG UNIVERSITY）

<div class="buaa-callout">
<strong>结尾固定文本：</strong>感谢您的观看与收听，敬请批评指正（禁止"感谢聆听"）
</div>

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">4</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 26px; --text-p-line-height: 1.8; }
</style>

<div class="buaa-chapter__badge"><span>2.2.1</span></div>

## Markdown 标题层级规范——一级与二级标题

<div class="buaa-chapter__body buaa-layout--flow">

<strong>1. 一级标题（<code>#</code>）</strong>

<code>#</code> 仅用于标识整体题目，即文件最顶部的演示文稿总标题。一份大纲中最多出现一个 <code>#</code>。

<strong>2. 二级标题（<code>##</code>）</strong>

<code>##</code> 统一格式为 <code>## Slide N: {可选短标签}</code>，用于区分不同页码的幻灯片内容，<code>N</code> 为从 1 开始递增的序号。标签仅在过渡页使用，正文页可省略标签。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">5</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>2.2.2</span></div>

## Markdown 标题层级规范——三级标题与深度限制

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-text-block">
<strong>3. 三级标题（<code>###</code>）及四级标题（<code>####</code>）</strong>
</div>

<code>###</code> 为正文主标题，格式 <code>### {编号} 主标题——副标题</code>，用中文破折号连接。

| 规则 | 说明 |
| :--: | :--: |
| 有编号 | 标题中标注了序号 → badge 中填入该序号 |
| 无编号 | 未标注序号 → AI 根据原则自动分配 |
| 标题栏 | 标题栏中**不得出现序号**，序号统一在 badge 内 |

<br>

<div class="buaa-text-block">
<strong>4. 标题深度限制</strong>
</div>

一级：<code>1</code>、<code>2</code>、<code>3</code> &hellip;&hellip; 二级：<code>1.1</code>、<code>1.2</code> 三级：<code>1.1.1</code>、<code>1.4.2</code>

不得使用四级及以上标题。<code>####</code> 仅用于同编号拆分多页时的子页标识。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">6</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>2.3</span></div>

## 编号与页码——自动规则

<div class="buaa-chapter__body buaa-layout--center">

| 条件 | badge 编号 | 页码 |
| :--: | :--: | :--: |
| 封面 | — | — |
| 目录 | — | — |
| 过渡页 | — | — |
| 正文单页 | 单数字如 `1` | 从 1 递增 |
| 正文多子节 | X.Y 如 `1.1` `1.2` | 连续递增 |
| 同一编号拆多页 | X.Y.Z 如 `1.1.1` | 连续递增 |
| 结尾 | `结语` | 最后页号 |

<br>

<div class="buaa-callout">
<strong>注意：</strong>封面、目录、过渡页不显示页码。正文页从 1 开始连续递增。插入新幻灯片后需重新编号所有后续页面。
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">7</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>2.4</span></div>

## 正文布局总览——11 种布局 (A~K)

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

| 布局 | CSS 组合 | 适用场景 |
| :--: | :--: | :--: |
| A | split-2 + split-center | 文左图右（默认图文布局） |
| B | layout-flow + ol/ul | 纯文字嵌套列表 |
| C | layout-center + text-block | 居中混排（段落 + 表格 + 总结） |
| D | split-2 + split-top + callout | 双栏对比（各 3~5 条目） |
| E | layout-center + text-block + ul + table | 居中混排含列表 |
| F | split-tb | 文上图下（技术大图专用） |

</div>

<div>

| 布局 | CSS 组合 | 适用场景 |
| :--: | :--: | :--: |
| G | flow-chart | 纵向流程图 |
| H | block-diagram | 系统框图（五方向组件关系） |
| I | img-pair + hm-cap | 双图并排 + 各自图注 |
| J | layout-flow + strong + ul | strong 小标题 + 无序列表 |
| K | layout-center + hm-fig | 纯大图（全页仅一张图） |

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">8</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
.buaa-flow-chart { --fc-font-size: 28px; --fc-min-width: 580px; --arr-length: 30px; --line-width: 4px; --arr-color: var(--buaa-primary); }
.buaa-flow-chart__arrow { margin: 8px 0 24px 0; }
/* 箭头样式微调：长/粗/颜色 */
/* .adj-fc-arrow { --arr-length: 40px !important; --line-width: 3px !important; } */
</style>

<div class="buaa-chapter__badge"><span>2.5</span></div>

## 布局决策树——AI 如何选择布局

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-flow-chart">

<div class="buaa-flow-chart__node">先判断：有图还是无图？</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">有图：照片/渲染图 &rarr; A；技术图 &rarr; 文字&le;180用F，&gt;180用A</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">无图：嵌套列表 &rarr; B；表格 &rarr; C；strong+ul &rarr; J；双栏对比 &rarr; D</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">特殊标记：流程图 &rarr; G；系统框图 &rarr; H；纯大图 &rarr; K</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">9</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>2.6</span></div>

## 文本密度参数——按内容形态自动调节

<div class="buaa-chapter__body buaa-layout--center">

| 内容形态 | 段落字号 | 段落行高 | 图片 max-height |
| :--: | :--: | :--: | :--: |
| 散文段落（无图） | 26px | 1.7 | — |
| 散文 + 大图 split-2 | 26px | 2 | 480-520px |
| 短文字 &le;100字 + 技术大图 split-tb | 28px | 2 | 300-350px |
| 中等文字 100~180字 + 图 split-tb | 28px | 1.5 | 250-280px |
| 嵌套列表 ol&gt;ul | 22px | 3(ol)/2(ul) | — |
| 平铺列表 &le;4条 | 24px | 3.25 | — |
| 双列密集对比 split-top | 19px | 2.4 | — |

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">10</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 2.35; }
</style>

<div class="buaa-chapter__badge"><span>2.7.1</span></div>

## 内容类型标记——图片与流程图

<div class="buaa-chapter__body buaa-layout--flow">

<strong>图片标记</strong>：

<code>![image-xxx.png](./figures/image-xxx.png)</code>

<strong>（全页大图）</strong>标记：整页仅一张图且无其他文字时使用，AI 走布局 K。

<strong>流程图标记</strong>：

<code>流程图（纵向）：</code>
<code>&nbsp;&nbsp;&rarr; 步骤一（3~9 个步骤，每步 &le;20 字）</code>
<code>&nbsp;&nbsp;&rarr; 步骤二</code>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">11</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.7; }
</style>

<div class="buaa-chapter__badge"><span>2.7.2</span></div>

## 内容类型标记——系统框图与公式

<div class="buaa-chapter__body buaa-layout--flow">

<strong>系统框图标记</strong>：

<code>系统框图：</code><br>
<code>center: 枢纽节点（&le;10字，唯一出现一次）</code><br>
<code>left: 节点A &rarr; 节点B</code><br>
<code>right: 节点C</code><br>
<code>top: 节点D</code><br>
<code>bottom: 节点E &rarr; 节点F</code>

<strong>公式：</strong>仅用于裸文本段落，禁止在 <code>&lt;li&gt;</code>/<code>&lt;td&gt;</code>/<code>&lt;hm-cap&gt;</code> 中使用。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">12</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">03</div>

# 样式体系详解

## Style System Details

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>3.1</span></div>

## 颜色方案——北航标准色系

<div class="buaa-chapter__body buaa-layout--center">

| 用途 | 颜色值 | 说明 |
| :--: | :--: | :--: |
| 主色 | #004F9E | BUAA 标准蓝 |
| 主色深色 | #003D7A | 表头边框 |
| 背景白色 | #FFFFFF | 正文页背景 |
| 正文文字 | #333333 | 主文字色 |
| 辅助文字 | #444 / #555 / #666 | 递减层级 |
| 浅蓝背景 | rgba(0,79,158,0.06) | 表格条纹、callout |
| 封面渐变 | rgba(0,47,94,0.97)&rarr;透明 | 封面左侧蒙层 |
| 过渡页 | #004F9E 纯色 | 过渡页满幅背景 |

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">13</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.7; }
</style>

<div class="buaa-chapter__badge"><span>3.2</span></div>

## 文字与排版——默认样式值

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

<strong>字体设置：</strong>

| 角色 | 字体族 |
| :--: | :--: |
| 全局正文 | Microsoft YaHei, PingFang SC, Noto Sans SC, sans-serif |
| 代码 | Consolas, Source Code Pro, Courier New, monospace |
| 公式 | Cambria Math, Times New Roman, serif |

</div>

<div>

<strong>正文排版默认值：</strong>

- 段落：26px，行高 1.7，颜色 #333
- 加粗 strong：颜色 #004F9E（北航蓝高亮）
- 列表 li：24px，左侧蓝色标记
- h3（正文小节标题）：26px，颜色 #004F9E
- 引用块 blockquote：蓝色 5px 左边框 + 浅蓝背景，字号 24px
- 水平线 hr：渐变 #004F9E&rarr;透明，高度 2px

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">14</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>3.3</span></div>

## 表格样式——全局默认值

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

| 属性 | 默认值 |
| :--: | :--: |
| 表头背景 | #004F9E |
| 表头文字色 | #FFFFFF |
| 单元格内边距 | 12px 16px（表头）/ 10px 16px（单元格） |
| 偶数行条纹 | #f4f8fc 浅蓝 |
| 边框颜色 | #003D7A（表头）/ #d0d0d0（单元格） |
| 字号 | 22px |
| 全局宽度 | 100%（layout-center 中自动居中） |

</div>

<div>

<div class="buaa-text-block">
<strong>表格素材规范：</strong>
</div>

- 列数建议 2~5 列，行数 3~12 行（含表头）
- 表头行必须写，用 <code>:--</code> / <code>:--:</code> / <code>--:</code> 标记对齐
- 超过 5 列或 12 行建议拆表或拆分多页
- 表格必须在居中布局（layout-center）中使用

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">15</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 0.; }
</style>

<div class="buaa-chapter__badge"><span>3.4</span></div>

## 代码块与公式——技术内容展示

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

<strong>代码块（pre）：</strong>

- 背景：#f5f7fa 浅灰蓝
- 左边框：4px solid #004F9E 蓝条
- 字号：18px，等宽字体
- 内边距：20px 28px，圆角 8px

<strong>行内代码（code）：</strong>

- 背景：rgba(0,79,158,0.06) 浅蓝
- 颜色：#004F9E 蓝色
- 内边距：2px 8px，圆角 4px

</div>

<div>

<strong>公式显示：</strong>

- 公式使用 LaTeX 语法（行内）或（块级）
- 只能在裸文本段落中使用
- 不可在 <code>&lt;li&gt;</code> / <code>&lt;td&gt;</code> / 图注中使用

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">16</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 1.7; }
</style>

<div class="buaa-chapter__badge"><span>3.5</span></div>

## 提示框与引用块——强调组件

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

<strong>callout 提示框</strong>（buaa-callout）：

- 浅蓝背景 rgba(0,79,158,0.06)
- 蓝色左边框 5px solid #004F9E
- 内边距 20px 28px
- 适用于总结框、强调提示、组件说明

<strong>引用块</strong>（blockquote）：

- 蓝色左边框 5px solid #004F9E
- 浅蓝背景 rgba(0,79,158,0.05)
- 字号 24px，颜色 #555

</div>

<div>

<strong>居中引用块</strong>（buaa-quote-block）：

- 文本 30px 斜体，居中，大号引号装饰
- 底部署名 22px #666

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">17</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">04</div>

# 增强组件库

## Enhanced Component Library

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 28px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>4.1</span></div>

## Awesome-Marp 集成——页面级网格布局

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-text-block" style="text-align:center;">
<center>项目集成了 Awesome-Marp 增强布局（适配 BUAA 主题色）：</center>
</div>

<br>

<div class="buaa-split--2 buaa-split--top">

<div>

<center><strong>两栏分栏：</strong></center>

| class | 比例 | 说明 |
| :--: | :--: | :--: |
| buaa-am-cols--2 | 50%:50% | 两栏五五分 |
| buaa-am-cols--2-64 | 60%:40% | 两栏六四分 |
| buaa-am-cols--2-73 | 70%:30% | 两栏七三分 |
| buaa-am-cols--2-46 | 40%:60% | 两栏四六分 |
| buaa-am-cols--2-37 | 30%:70% | 两栏三七分 |

</div>

<div>

<center><strong>其他布局：</strong></center>

| class | 说明 |
| :--: | :--: |
| buaa-am-cols--3 | 三栏均分 |
| buaa-am-rows--2 | 上下两行分栏 |
| buaa-am-pin--3 | 品字型（上全宽 + 下两栏） |

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">18</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>4.2</span></div>

## 多栏列表——8 种样式组合

<div class="buaa-chapter__body buaa-layout--center">

| class | 说明 |
| :--: | :--: |
| buaa-am-cols2-ul--sq | 两栏无序列表 + 方形序号 |
| buaa-am-cols2-ul--ci | 两栏无序列表 + 圆形序号 |
| buaa-am-cols2-ol--sq | 两栏有序列表 + 方形序号 |
| buaa-am-cols2-ol--ci | 两栏有序列表 + 圆形序号 |
| buaa-am-col1-ol--sq | 单栏有序列表 + 方形序号 |
| buaa-am-col1-ol--ci | 单栏有序列表 + 圆形序号 |
| buaa-am-col1-ul--sq | 单栏无序列表 + 方形序号 |
| buaa-am-col1-ul--ci | 单栏无序列表 + 圆形序号 |

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">19</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 26px; --text-p-line-height: 1.5; }
</style>

<div class="buaa-chapter__badge"><span>4.3.1</span></div>

## 全局效果修饰——字号缩放与彩色引用块

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

<div class="buaa-text-block">
<center><strong>字号缩放：</strong></center>
</div>

| class | 效果 |
| :--: | :--: |
| buaa-am--tinytext | 全局缩字 80% |
| buaa-am--smalltext | 全局缩字 90% |
| buaa-am--largetext | 全局放字 115% |
| buaa-am--hugetext | 全局放字 130% |

</div>

<div>

<div class="buaa-text-block">
<center><strong>彩色引用块</strong>（buaa-am--bq-*）：</center>
</div>

| class | 边框颜色 |
| :--: | :--: |
| buaa-am--bq-blue | 蓝色 #004F9E |
| buaa-am--bq-red | 红色 #dc3545 |
| buaa-am--bq-green | 绿色 #28a745 |
| buaa-am--bq-purple | 紫色 #6f42c1 |
| buaa-am--bq-black | 黑色 #333 |

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">20</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 32px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>4.3.2</span></div>

## 全局效果修饰——毛玻璃与页面装饰

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-text-block">
<center><strong>其他增强：</strong></center>
</div>

| class | 说明 |
| :--: | :--: |
| buaa-am--fglass | 毛玻璃效果列表 |
| buaa-am--navbar | 导航进度栏 |
| buaa-am--footnote | 脚注布局（内容 + 虚线分隔底部脚注） |
| buaa-am--fixedtitle-a/b | 固定标题样式 A/B |

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">21</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.4; }
</style>

<div class="buaa-chapter__badge"><span>4.4.1</span></div>

## 内置组件库——前 7 种场景组件

<div class="buaa-chapter__body buaa-layout--center">

| 组件 | CSS class | 适用场景 |
| :--: | :--: | :--: |
| 卡片网格 | buaa-card-grid + buaa-card | 带标题+正文的信息卡片 |
| 前后对比 | buaa-before-after + label | 两张图并排 + 标签 |
| 水平步骤流 | buaa-step-flow + step-card | 3~5 步水平流程 |
| 垂直步骤流 | buaa-step-vflow + row | 纵向编号步骤 + 文字 |
| 图片画廊 | buaa-img-gallery + gal-2/3/4 | 多张图片自动缩放 |
| 双图+图注 | buaa-img-pair + hm-cap | 两张图并排 + 独立标注 |
| 全宽图片 | buaa-img--full | 单张大图填充 |

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">22</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.4; }
</style>

<div class="buaa-chapter__badge"><span>4.4.2</span></div>

## 内置组件库——剩余 11 种

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

| 组件 | CSS class | 适用场景 |
| :--: | :--: | :--: |
| 键值对列表 | buaa-kv-list + dt/dd | 术语定义对 |
| 时间轴 | buaa-timeline + t-node | 水平时间线 |
| 公式块 | buaa-formula-block | 突出显示公式 |
| 大数字 | buaa-num--big + num-label | 统计数据展示 |
| 文本块 | buaa-text-block + highlight | 密集段落 + 内联高亮 |
| 统计指标行 | buaa-stat-row + stat | 3~4 个指标卡片 |

</div>

<div>

| 组件 | CSS class | 适用场景 |
| :--: | :--: | :--: |
| 图标列表 | buaa-icon-list + li-icon | 带图标的项目列表 |
| 小结框 | buaa-summary-box | 章节小结 |
| 提示框 | buaa-callout | 总结框、强调提示 |
| 网格 | buaa-grid--2/3/4 | 2/3/4 项自适应网格 |
| 毛玻璃 | buaa-am--fglass | 列表半透明背景阴影 |

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">23</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">05</div>

# 素材输入与排版输出

## Input Specifications & Output Standards

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 24px; --text-p-line-height: 2; }
</style>

<div class="buaa-chapter__badge"><span>5.1</span></div>

## 文字内容规范——输入要求

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--top">

<div>

<strong>散文段落：</strong>

- 用自然语言书写，直接跟在标题后，段间空一行
- 建议 50~300 字/组，超过 500 字的连续段落考虑拆页

<strong>列表内容：</strong>

- 用 <code>1.</code>（有序）或 <code>-</code>（无序）Markdown 语法
- 每条 &le;60 字为宜，超过 80 字考虑拆项或拆页
- 嵌套最多 2 层（ol &gt; ul 或 ul &gt; ul）
- 单页总条目建议 &le;10 条

</div>

<div>

<strong>加粗强调：</strong>

- 用 <code>**文字**</code> 语法，AI 自动转为 <code>&lt;strong&gt;</code> 标签
- 每页加粗词条建议 &le;5 个

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">24</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>5.2</span></div>

## 图片素材规范——输入要求

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

| 项目 | 规范 |
| :--: | :--: |
| 存放路径 | figures/ 或 {大纲名}.assets/ |
| 引用方式 | `![描述]({相对路径})` |
| 图片格式 | PNG（推荐）、JPG、SVG |
| 分辨率 | 技术图 1200~1920px / 照片 800~1200px |
| 长宽比 | 4:3 或 16:9 |
| 图注 | 需要时在图下方加 `图注：{说明}` |

</div>

<div>

<div class="buaa-text-block">
<strong>图片数量规则：</strong>
</div>

- 每页正文建议 0~2 张图
- 双图并排时两张图宽高比应一致
- 图片前后各留空行（防止被 <code>&lt;p&gt;</code> 包裹）
- 封面背景图已内置（cover-bg.png），无需额外提供

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">25</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 26px; --text-p-line-height: 2.2; --text-size: 24px; --text-line-height: 2.6; --text-item-gap: 10px; }
/* 列表条目微调：字号/行距/条目间距 */
/* section { --text-size: 20px; --text-line-height: 2.0; --text-item-gap: 6px; } */
</style>

<div class="buaa-chapter__badge"><span>5.3</span></div>

## 排版输出标准——生成结果检查

<div class="buaa-chapter__body buaa-layout--flow">

AI 生成 PPT 后，用户应检查：

<ol>
  <li><strong>编号正确：</strong>正文页码从 1 开始连续递增，封面/目录/过渡无页码</li>
  <li><strong>badge 编号：</strong>单页用单数字，多页用 X.Y，拆页用 X.Y.Z</li>
  <li><strong>标题一致：</strong>大纲中的标题与生成 PPT 中一字不差</li>
  <li><strong>图片可见：</strong>路径正确、图片未压扁拉伸</li>
  <li><strong>图注节制：</strong>图注仅在大纲明确标注时出现</li>
  <li><strong>表格居中：</strong>不在 layout-flow 中放置表格</li>
  <li><strong>公式位置：</strong>公式不在 <code>&lt;li&gt;</code> / <code>&lt;td&gt;</code> / 图注中</li>
</ol>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">26</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>5.4</span></div>

## 常用微调——adj-* 占位符

<div class="buaa-chapter__body buaa-layout--center">

AI 生成的 <code>.md</code> 文件中，<code>&lt;style scoped&gt;</code> 包含注释占位符。取消注释即可微调：

| 占位符 | 作用 | 默认值示例 |
| :--: | :--: | :--: |
| <code>.adj-img</code> | 图片最大高度 | max-height: 480px |
| <code>.adj-txt</code> | 文本块字号行距 | font-size: 24px; line-height: 1.8 |
| <code>.adj-tbl</code> | 表格字号 | font-size: 22px |
| <code>.adj-list</code> | 列表字号行距 | font-size: 22px; line-height: 2 |
| <code>.adj-buaa-callout</code> | callout 字号行距 | font-size: 22px; line-height: 1.8 |

<br>

<div class="buaa-callout">
<strong>⚠️ 注意：</strong><code>adj-*</code> 为 class 选择器在 scoped 中大概率不生效，应改用 <code>section { --var }</code> 注入 CSS 变量。
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">27</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">06</div>

# 快速上手流程

## Quick Start Guide

---

<!-- _class: buaa-chapter -->

<style scoped>
.buaa-flow-chart { --fc-font-size: 26px; --fc-min-width: 480px; --arr-length: 30px; --line-width: 4px; --arr-color: var(--buaa-primary); }
.buaa-flow-chart__arrow { margin: 8px 0 24px 0; }
/* 箭头样式微调：长/粗/颜色 */
/* .adj-fc-arrow { --arr-length: 40px !important; --line-width: 3px !important; } */
</style>

<div class="buaa-chapter__badge"><span>6.1</span></div>

## 四步生成——从大纲到导出

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-flow-chart">

<div class="buaa-flow-chart__node">步骤一：准备素材（整理文字 &rarr; 图片放入 figures/ &rarr; 准备表格）</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">步骤二：编写大纲（复制模板 &rarr; 填入封面/目录/各章内容 &rarr; 标记规范）</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">步骤三：交给 AI Agent（提供大纲.md &rarr; AI 逐页分析 &rarr; 生成 presentation.md）</div>
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
<div class="buaa-flow-chart__node">步骤四：预览微调（Ctrl+K V 预览 &rarr; 取消 adj-* 注释 &rarr; 导出），或交由AI Agent微调</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">28</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
/* === 代码块字体可调参数 === */
section {
  --pre-font-size:   30px;      /* 字号: 支持 px/em/rem, 如 18px 0.9em */
  --pre-font-family: "Consolas", "Courier New", "Fira Code", monospace;  /* 字体 */
  --pre-color:       #2d3436;   /* pre 文字色: 支持 #hex / rgb() / rgba() */
  --pre-code-color:  #2d3436;   /* pre 内 code 颜色 (通常与 pre-color 一致) */
  --pre-line-height: 1.6;       /* 行高 */
  --code-font-size:  1em;       /* code 相对字号: 1em = 与 pre 等大, 0.85em = 缩小15% */
  --text-p-size:     18px;
  --text-p-line-height: 1.5;
}
</style>

<div class="buaa-chapter__badge"><span>6.2</span></div>

## 大纲空白模板——可直接复制使用

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

```
# {演示文稿总标题}

---

## Slide 1: 封面

{主标题，≤20字}

{副标题，≤20字；不需要则删除此行}

汇报人：{姓名}

---

## Slide 2: 目录

- 01 {章节1标题}
- 02 {章节2标题}
- 03 {章节3标题}

---

## Slide 3: 01 {章节1标题}

### 第X章：{章节1全称}

---

## Slide 4:

### {编号} {页面标题}

{散文段落 / 列表 / 表格 / 图片，按标记规范书写}

---

## Slide N: 结尾
```

</div>

<div>

<div class="buaa-callout">
<strong>提醒：</strong>正文标题（<code>###</code>）中的序号将自动填入 PPT 的章节块（badge），标题栏中不再重复显示序号。标题深度严格限制为三级（1 / 1.1 / 1.1.1），禁止四级及以上。
</div>

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">29</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
/* 列表条目微调：字号/行距/条目间距 */  
section { --text-p-size: 26px; --text-p-line-height: 2; --text-size: 22px; --text-line-height: 2.4; --text-item-gap: 14px; }
</style>

<div class="buaa-chapter__badge"><span>6.3.1</span></div>

## 16 条硬约束——致命级

<div class="buaa-chapter__body buaa-layout--flow">

<strong>致命级：</strong>

<ol>
  <li><code>&lt;style scoped&gt;</code> 放在 badge 之前，绝不可放在 page-num 后面</li>
  <li><code>.text-block</code> 内禁止 <code>&lt;p&gt;</code> 标签，裸写文字</li>
  <li>目录 <code>ul</code> 必须带完整 inline style</li>
  <li>公式只能在裸文本段落中，<code>&lt;li&gt;/&lt;td&gt;/hm-cap</code> 中用 <code>&lt;i&gt;x&lt;/i&gt;&lt;sub&gt;1&lt;/sub&gt;</code></li>
  <li>图注仅在大纲标注"图注："时添加</li>
  <li>block-diagram 中 Hub 只在 center 出现一次</li>
  <li>封面必须有 cover-date</li>
</ol>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">30</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.8; }
</style>

<div class="buaa-chapter__badge"><span>6.3.2</span></div>

## 16 条硬约束——严重级与注意级

<div class="buaa-chapter__body buaa-layout--flow">

<strong>严重级：</strong>

<ol start="8">
  <li>大纲已有标题 &rarr; 严格沿用，一字不改</li>
  <li>同一编号多页 &rarr; 自动细化 X.Y.Z</li>
  <li><code>.adj-*</code> 仅作为 CSS 注释占位，不在 HTML 元素上激活</li>
  <li>加粗用 <code>&lt;strong&gt;</code>，禁止 <code>**text**</code></li>
</ol>

<hr>

<strong>注意级：</strong>

<ol start="12">
  <li>图片前后各空行，防 <code>&lt;p&gt;</code> 包裹</li>
  <li>禁止：<code>&lt;footer&gt;</code> 标签、内容中用 <code>---</code>（幻灯片分隔符）、<code>&lt;img class/style&gt;</code></li>
  <li>标题层级：<code>#</code>仅用于文件总标题；<code>##</code>仅用于<code>Slide N:</code>分页标识；<code>###</code>为正文主标题；标题深度严格限三级（X / X.Y / X.Y.Z），禁止四级及以上</li>
  <li>序号与标题分离：大纲<code>###</code>中的编号提取填入 badge；<code>##</code>标题栏不出现序号，序号统一放 badge</li>
  <li><strong>规则 #16：</strong>Scoped 样式必须用 <code>section { }</code> 注入 CSS 变量（禁止直接写选择器覆盖）</li>
</ol>

<div class="buaa-callout">
<strong>常见陷阱：</strong>footer &rarr; 用 <code>div.buaa-chapter__footer</code>；幻灯片内 <code>---</code> &rarr; 用 <code>&lt;hr&gt;</code>；表格在 layout-flow &rarr; 用 layout-center
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">31</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">07</div>

# 模板样式说明

## Template Style Guide

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>7.1</span></div>

## 单图布局效果——三种展示方式

<div class="buaa-chapter__body buaa-layout--flow">

<strong>文左图右</strong>（布局 A，split-2）：

散文段落与图片并排展示。文字在左，图片在右，各占约 50% 宽度。

<strong>文上图下</strong>（布局 F，split-tb）：

文字在上方（&le;180字），技术原理图/曲线图在下方全宽展示。

<strong>纯大图</strong>（布局 K，layout-center + hm-fig）：

整页仅展示一张大图，无文字或仅标题，最大化展示空间。

<div class="buaa-callout">
<strong>适用场景：</strong>单图布局涵盖日常 80% 的图文混排需求。照片/渲染图用 A，技术大图用 F，核心图表全页展示用 K。
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">32</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>7.2</span></div>

## 双图布局效果——并排与对比

<div class="buaa-chapter__body buaa-layout--flow">

<strong>双图并排 + 图注</strong>（布局 I，img-pair）：

两张图片左右并排，各自可带独立图注。适用于两方案对比、前后对照等场景。

<strong>前后对比</strong>（before-after + ba-label）：

两张图片并排展示，各自上方有标签（如"优化前"、"优化后"），适用于结果对比、方案改进。

<strong>双图画廊</strong>（img-gallery gal-2）：

两张图片均匀分布，自动缩放。适用于产品双视角、两阶段结果等对称展示。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">33</div>

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.6; }
</style>

<div class="buaa-chapter__badge"><span>7.3</span></div>

## 三图及多图布局效果——画廊与网格

<div class="buaa-chapter__body buaa-layout--flow">

<strong>三图画廊</strong>（img-gallery gal-3）：

三张图片均匀分布，自动缩放。适用于三方案对比、三阶段展示等。

<strong>四图画廊</strong>（img-gallery gal-4）：

四张图片均匀分布，适用于多角度对比或四象限展示。

<strong>三栏均分</strong>（split-3）：

三列分栏，可用于三方案并排对照、三维度同时展示。

<strong>卡片网格</strong>（card-grid + card）：

多个卡片等大排列，带标题和正文说明，适合特性介绍列表。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">34</div>

---

<!-- _class: buaa-end -->

<div class="buaa-chapter__badge"><span>结语</span></div>

# 感谢您的观看与收听，敬请批评指正

## Q &amp; A

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">35</div>
