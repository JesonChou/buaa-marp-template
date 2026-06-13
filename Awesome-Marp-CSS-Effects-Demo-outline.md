# Awesome-Marp 纯 CSS 样式效果展示

---

## Slide 1: 封面

BUAA Marp PPT —— Awesome-Marp 纯CSS样式效果展示

汇报人：JesonChou

---

## Slide 2: 目录

- 01 毛玻璃与半透明效果
- 02 导航栏、脚注与固定标题
- 03 字号缩放体系
- 04 彩色引用块
- 05 卡片组件
- 06 列表样式变体
- 07 图标列表与 Callout
- 08 页面级网格布局
- 09 综合混排

---

## Slide 3: 01 毛玻璃与半透明效果

### 第一章：毛玻璃与半透明效果

---

## Slide 4:

### 1 毛玻璃与半透明——两种效果左右对比

> 布局：A  |  class：buaa-am--fglass  |  内容：split-2左(毛玻璃列表)右(CSS毛玻璃说明)  |  密度：--text-size:22px lh1.8

页面使用 `<!-- _class: buaa-chapter buaa-am--fglass -->`，body 内用 split-2 左右分栏对比：

- **左侧**（`buaa-am--fglass`）：无序列表演示，白色背景 + 顶部4px蓝色装饰条 + box-shadow投影 + 非对称圆角——模拟玻璃质感，适合任意页面列表
- **右侧**（`backdrop-filter: blur(6px)`）：半透明白色面板模拟目录页的 CSS 真实毛玻璃——`rgba(255,255,255,0.88)` + `backdrop-filter` + `mask-image` 渐变淡出

两种效果一左一右，视觉差异不言自明。

---

## Slide 5: 02 导航栏、脚注与固定标题

### 第二章：导航栏、脚注与固定标题

---

## Slide 6:

### 2 导航栏 + 脚注效果演示

> 布局：B  |  class：buaa-am--navbar + buaa-am--footnote + buaa-am--fixedtitle-a/b  |  内容：多种class叠加演示  |  密度：--text-size:22px lh1.8

同一页通过 scoped CSS 同时展示三种辅助布局的效果：

1. **导航栏**（buaa-am--navbar）：顶部半透明浅蓝色条，`<header>` + `justify-content: space-between` 水平分布
2. **脚注布局**（buaa-am--footnote）：`.tdiv` 正文 + `.bdiv` 脚注，CSS Grid 两行，`::before` 虚线分隔
3. **固定标题 A/B**（buaa-am--fixedtitle-a/b）：`<h2>` 变蓝色药丸徽章，A 型占文档流，B 型绝对定位

---

## Slide 7: 03 字号缩放体系

### 第三章：字号缩放体系

---

## Slide 8:

### 3 四种缩放级别——实际效果对比

> 布局：B  |  class：buaa-am--tinytext / smalltext / largetext / hugetext  |  内容：4段同类文字不同字号对比  |  密度：各class自带缩放比例

同一页用 scoped CSS 展示 4 种缩放：tinytext(80%) / smalltext(90%) / largetext(115%) / hugetext(130%)，每段标明 `buaa-am--tinytext` 等 class 名称。

加上代码默认基准(100%)作为参照。缩放通过 `font-size: N%` 相对上下文实现，所有子元素等比缩放。

---

## Slide 9: 04 彩色引用块

### 第四章：彩色引用块

---

## Slide 10:

### 4 五种彩色引用块——实际效果对比

> 布局：B  |  class：buaa-am--bq-blue / red / green / purple / black  |  内容：5段blockquote不同颜色对比  |  密度：--text-size:22px lh1.8

同一页用 scoped CSS + `nth-of-type(1~5)` 展示 5 种颜色的 `<blockquote>`，每条标注 class 名称：

- blue `#004F9E` — 官方说明
- red `#dc3545` — 警告禁止
- green `#28a745` — 成功实践
- purple `#6f42c1` — 创新方案
- black `#333333` — 中性备注

---

## Slide 11: 05 卡片组件

### 第五章：卡片组件

---

## Slide 12:

### 5 基础卡片 + 多卡片网格——效果演示

> 布局：B  |  内容：单卡+三卡网格  |  密度：--text-size:22px lh1.8

同一页用 scoped CSS 展示 `<div class="buaa-am-card">` 单卡效果 + `<div class="buaa-card-grid">` 三卡网格布局。

- 单卡：渐变背景（rgba(0,79,158,0.08) → rgba(0,79,158,0.02)）、12px 圆角、标题 + 正文分离
- 三卡网格：flexbox 等宽排列，2~4 张最佳

---

## Slide 13: 06 列表样式变体

### 第六章：列表样式变体

---

## Slide 14:

### 6 列表标记 + 双栏列表——变体对比

> 布局：B  |  class：buaa-am-list--disc/circle/square + buaa-am-cols2-ul/ol  |  内容：多种列表标记+双栏列表对比  |  密度：--text-size:22px lh1.8

同一页用 scoped CSS 展示三种列表变体：

1. **标记类型**：square / circle 两种标记通过 `::marker` 或 `list-style` 控制
2. **双栏无序列**：两栏 cols2-ul（50% 每列），适合 6~8 条目
3. **双栏有序列**：两栏 cols2-ol，序号带方形/圆形背景色

---

## Slide 15: 07 图标列表与 Callout

### 第七章：图标列表与 Callout

---

## Slide 16:

### 7 图标列表 + Callout——效果对比

> 布局：B  |  内容：buaa-am-icon-list + buaa-callout对比  |  密度：--text-size:22px lh1.8

同一页展示两种 CSS 强调组件：

- **图标列表**（buaa-am-icon-list）：`▸` 蓝色前缀 + 列表项，适合功能罗列
- **Callout**（buaa-callout）：浅蓝背景 + 蓝色左边框，适合长文本提示

底部 Callout 总结两者的区别和适用场景。

---

## Slide 17: 08 页面级网格布局

### 第八章：页面级网格布局

---

## Slide 18:

### 8 两栏 / 三栏 / 品字型——效果对比

> 布局：B  |  class：buaa-am-cols--2 / cols--3 / pin--3  |  内容：三种网格布局对比  |  密度：--text-size:22px lh1.8

同一页用 scoped CSS 创建三块区域，每块展示一种网格布局：

1. **两栏五五分**（cols--2）：左右 `.ldiv` / `.rdiv` 各 50%
2. **三栏均分**（cols--3）：左中右 `.ldiv` / `.mdiv` / `.rdiv`
3. **品字型**（pin--3）：上部 `.tdiv` 通栏 + 下部两栏

---

## Slide 19: 09 综合混排

### 第九章：综合混排

---

## Slide 20:

### 9 多组件叠加——页面级 class 组合 + 内嵌组件

> 布局：B  |  内容：navbar+fixedtitle+footnote叠加 + card-grid内嵌icon-list  |  密度：--text-size:22px lh1.8

同一页演示两种「组件嵌套」场景：

1. **页面级叠加**：navbar header + fixedtitle h2 药丸标题 + footnote 脚注虚线分隔，三个页面 class 可叠加
2. **组件内嵌**：card-grid 卡片网格内部嵌入 icon-list 图标列表，底部 Callout 总结

<br>

设计原则：外部容器决定布局（网格/分栏），内部元素决定样式（卡片/列表），各司其职，互不干扰。

---

## Slide 21: 结尾

