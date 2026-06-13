---
marp: true
theme: buaa
paginate: false
---

<!-- _class: buaa-cover -->

<img class="buaa-cover__logo" src="./assets/logo.png">

# Awesome-Marp 纯 CSS 样式效果展示

## 纯CSS样式效果巡览

<div class="buaa-cover__presenter">汇报人：布衣白丁</div>
<div class="buaa-cover__date">2026年5月28日</div>
<div class="buaa-cover__decor">BEIHANG UNIVERSITY</div>

---

<!-- _class: buaa-catalog -->

<style scoped>
ul { left: 730px !important; display: flex !important; flex-direction: column !important; gap: 28px !important; }
li { font-size: 24px !important; margin-bottom: 0 !important; }
.buaa-catalog__num { border-radius: 6px !important; }
</style>

<div class="buaa-catalog__title">目录</div>
<div class="buaa-catalog__line"></div>
<div class="buaa-catalog__eng">Contents</div>

<ul style="position:absolute;left:730px;top:50%;transform:translateY(-50%);display:flex;flex-direction:column;gap:28px;list-style:none;z-index:2;padding:0;margin:0;">
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">01</span> 毛玻璃与半透明效果</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">02</span> 导航栏、脚注与固定标题</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">03</span> 字号缩放体系</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">04</span> 彩色引用块</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">05</span> 卡片组件</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">06</span> 列表样式变体</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">07</span> 图标列表与 Callout</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">08</span> 页面级网格布局</li>
  <li style="font-size:24px;margin-bottom:0;display:flex;align-items:center;color:#333;"><span class="buaa-catalog__num">09</span> 综合混排</li>
</ul>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">01</div>

# 毛玻璃与半透明效果

## Frosted Glass & Translucency

---

<!-- _class: buaa-chapter buaa-am--fglass -->

<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.7; --text-size: 21px; }
/* 模拟 backdrop-filter 面板 */
.demo-glass-backdrop {
  position: relative; padding: 24px 28px; border-radius: 12px;
  background: rgba(255, 255, 255, 0.88);
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.06);
  overflow: hidden; min-height: 0; flex: 1;
}
.demo-glass-backdrop::before {
  content: ""; position: absolute; inset: 0; z-index: 0; opacity: 0.16;
  background: repeating-linear-gradient(45deg, var(--buaa-primary) 0, var(--buaa-primary) 1px, transparent 1px, transparent 14px);
  border-radius: 12px;
}
.demo-glass-backdrop > * { position: relative; z-index: 1; }
.demo-glass-backdrop p, .demo-glass-backdrop li { color: #444; }
</style>

<div class="buaa-chapter__badge"><span>1</span></div>

## 毛玻璃与半透明——两种效果左右对比

<div class="buaa-chapter__body buaa-layout--center">

<div class="buaa-split--2 buaa-split--center">

<div>

<strong>buaa-am--fglass — 装饰模拟</strong>

白色背景 + box-shadow + 蓝色顶边装饰条，在任意页面列表中呈现玻璃质感。

<ul><li>顶部 4px 蓝色强调边框</li><li><strong>box-shadow</strong> 蓝色系柔和投影</li><li>非对称圆角 <strong>0 0 20px 20px</strong></li><li>全浏览器兼容，无需依赖</li></ul>

</div>

<div class="demo-glass-backdrop">

<strong>backdrop-filter — 真实模糊</strong>

CSS filter 对面板后方内容实时高斯模糊，叠加半透明白色蒙层。

<ul><li><strong>backdrop-filter: blur(6px)</strong> 真实模糊</li><li><strong>rgba(255,255,255,0.88)</strong> 半透明叠加</li><li>用于目录页 <strong>buaa-catalog::before</strong></li><li>仅现代浏览器支持（Chrome 76+）</li></ul>

</div>

</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">1</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">02</div>

# 导航栏、脚注与固定标题

## Navbar, Footnote & Fixed Title

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.5; --text-size: 19px; --text-item-gap: 4px; }
.demo-navbar {
  width: 100%; padding: 6px 16px; background: rgba(var(--buaa-primary-rgb), 0.08);
  display: flex; justify-content: space-between; color: var(--buaa-primary); font-size: 16px;
  border-radius: 6px; margin-bottom: 12px; flex-shrink: 0;
}
.demo-footnote { display: flex; flex-direction: column; gap: 10px; flex: 1; min-height: 0; }
.demo-footnote .tdiv { flex: 1; }
.demo-footnote .tdiv p { font-size: 20px; margin: 4px 0; }
.demo-footnote .bdiv {
  border-top: 1.8px dashed var(--buaa-primary); padding-top: 8px;
  font-size: 18px; color: #888;
}
.demo-pill {
  display: inline-block; background: var(--buaa-primary); color: #fff;
  padding: 6px 18px; border-radius: 8px; font-size: 20px; font-weight: 700;
  margin-bottom: 8px;
}
</style>

<div class="buaa-chapter__badge"><span>2</span></div>

## 导航栏 + 脚注效果演示

<div class="buaa-chapter__body buaa-layout--center">

<div class="demo-navbar">
  <span>02 · 导航栏与脚注</span>
  <span>2 / 4</span>
  <span>Awesome-Marp</span>
</div>

<div class="demo-footnote">
  <div class="tdiv">

<span class="demo-pill">固定标题 A 型 — fixedtitle-a</span>

三种辅助布局通过 scoped CSS 在同一页展示：上方的蓝色半透明条模拟 buaa-am--navbar，本行药丸徽章模拟 buaa-am--fixedtitle-a（h2 → 蓝色填充圆角），下方脚注模拟 buaa-am--footnote（Grid 两行布局，虚线分隔）。

  </div>
  <div class="bdiv">

脚注：分隔线由 .bdiv::before 伪元素自动生成 · 虚线 1.8px 蓝色

  </div>
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">2</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">03</div>

# 字号缩放体系

## Text Size System

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.5; }
.demo-sizes { display: flex; flex-direction: column; gap: 10px; width: 100%; }
.demo-sizes > div { padding: 8px 20px; border-radius: 8px; border-left: 4px solid var(--buaa-primary); }
.demo-sizes > div:nth-child(1) { font-size: 15px; background: rgba(var(--buaa-primary-rgb), 0.03); }
.demo-sizes > div:nth-child(2) { font-size: 18px; background: rgba(var(--buaa-primary-rgb), 0.04); }
.demo-sizes > div:nth-child(3) { font-size: 24px; background: rgba(var(--buaa-primary-rgb), 0.04); }
.demo-sizes > div:nth-child(4) { font-size: 28px; background: rgba(var(--buaa-primary-rgb), 0.05); }
.demo-sizes > div:nth-child(5) { font-size: 22px; background: rgba(var(--buaa-primary-rgb), 0.02); color: #888; }
.demo-sizes strong { font-size: 1em; }
</style>

<div class="buaa-chapter__badge"><span>3</span></div>

## 四种缩放级别——实际效果对比

<div class="buaa-chapter__body buaa-layout--center">

<div class="demo-sizes">
  <div><strong>buaa-am--tinytext（80%）</strong> — 系统初始化包括硬件自检、引导加载、内核启动三个阶段，每个阶段有独立错误处理。</div>
  <div><strong>buaa-am--smalltext（90%）</strong> — 系统初始化包括硬件自检、引导加载、内核启动三个阶段，每个阶段有独立错误处理。</div>
  <div><strong>buaa-am--largetext（115%）</strong> — 系统初始化包括硬件自检、引导加载、内核启动三个阶段。</div>
  <div><strong>buaa-am--hugetext（130%）</strong> — 系统初始化三个阶段：自检 → 引导 → 启动。</div>
  <div><strong>默认（100%，参照基准）</strong> — 系统初始化包括硬件自检、引导加载、内核启动三个阶段，每个阶段有独立错误处理。</div>
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">3</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">04</div>

# 彩色引用块

## Colored Blockquotes

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.4; }
blockquote {
  padding: 10px 20px !important; border-radius: 8px !important;
  border-left: 5px solid !important; letter-spacing: 0px !important;
  margin: 6px 0 !important; font-size: 20px !important;
}
blockquote:nth-of-type(1) {
  background: rgba(var(--buaa-primary-rgb), 0.08) !important;
  border-left-color: var(--buaa-primary) !important;
}
blockquote:nth-of-type(2) {
  background: rgba(220, 53, 69, 0.08) !important;
  border-left-color: #dc3545 !important;
}
blockquote:nth-of-type(3) {
  background: rgba(40, 167, 69, 0.08) !important;
  border-left-color: #28a745 !important;
}
blockquote:nth-of-type(4) {
  background: rgba(111, 66, 193, 0.08) !important;
  border-left-color: #6f42c1 !important;
}
blockquote:nth-of-type(5) {
  background: rgba(51, 51, 51, 0.06) !important;
  border-left-color: #333 !important;
}
</style>

<div class="buaa-chapter__badge"><span>4</span></div>

## 五种彩色引用块——实际效果对比

<div class="buaa-chapter__body buaa-layout--flow">

> buaa-am--bq-blue  — 蓝色引用：这是标准信息提示，适用于官方说明和一般通知。

> buaa-am--bq-red  — ⚠️ 红色引用：这是警告信息，请勿在非授权环境下执行此操作！

> buaa-am--bq-green  — ✓ 绿色引用：验证通过！所有测试用例均正常运行，无回归错误。

> buaa-am--bq-purple  — 紫色引用：创新提示——尝试改用异步架构可提升吞吐量。

> buaa-am--bq-black  — 黑色引用：参考《CSS 权威指南》第四版第 12 章详细讨论了该方案。

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">4</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">05</div>

# 卡片组件

## Card Components

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.5; }
.demo-card {
  padding: 14px 18px; border-radius: 10px; margin-bottom: 12px;
  background: linear-gradient(135deg, rgba(0,79,158,0.08), rgba(0,79,158,0.02));
  border: 1px solid rgba(var(--buaa-primary-rgb), 0.08);
}
.demo-card__title { font-size: 22px; font-weight: 700; color: var(--buaa-primary); margin-bottom: 6px; }
.demo-card__body { font-size: 20px; color: #555; line-height: 1.6; }
.demo-card-grid { display: flex; gap: 16px; width: 100%; padding-top: 12px; }
.demo-card-grid .demo-card { flex: 1; margin-bottom: 0; }
.demo-card-grid .demo-card ul { font-size: 18px; line-height: 1.5; margin: 4px 0 0 0; padding-left: 22px; }
.demo-card-grid .demo-card li { margin-bottom: 0; }
</style>

<div class="buaa-chapter__badge"><span>5</span></div>

## 基础卡片 + 多卡片网格——效果演示

<div class="buaa-chapter__body buaa-layout--flow">

<strong>基础卡片（buaa-am-card）：</strong>

<div class="demo-card">
  <div class="demo-card__title">架构设计原则</div>
  <div class="demo-card__body">
    单一职责：每个模块只负责一个功能 · 开闭原则：对扩展开放，对修改关闭 · 依赖倒置：依赖抽象而非具体实现
  </div>
</div>

<strong>多卡片网格（buaa-card-grid）：</strong>

<div class="demo-card-grid">
  <div class="demo-card">
    <div class="demo-card__title">前端</div>
    <ul><li>Vue 3 + TS</li><li>Vite 构建</li></ul>
  </div>
  <div class="demo-card">
    <div class="demo-card__title">后端</div>
    <ul><li>Node.js</li><li>PostgreSQL</li></ul>
  </div>
  <div class="demo-card">
    <div class="demo-card__title">DevOps</div>
    <ul><li>Docker</li><li>GitHub CI</li></ul>
  </div>
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">5</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">06</div>

# 列表样式变体

## List Style Variants

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.5; --text-size: 20px; }
.demo-square { list-style-type: square; }
.demo-circle { list-style-type: circle; }
.demo-square li::marker, .demo-circle li::marker { color: var(--buaa-primary); }
.demo-cols2 { display: flex; gap: 24px; width: 100%; margin: 8px 0; }
.demo-cols2 .col { flex: 1; }
.demo-cols2 ul, .demo-cols2 ol { padding-left: 24px; margin: 0; }
.demo-cols2 li { font-size: 19px; line-height: 1.4; margin-bottom: 2px; }
</style>

<div class="buaa-chapter__badge"><span>6</span></div>

## 列表标记 + 双栏列表——变体对比

<div class="buaa-chapter__body buaa-layout--center">

<strong>标记类型（buaa-am-list--square / --circle）：</strong>

<div class="demo-cols2">
  <div class="col">
    <ul class="demo-square"><li>系统架构设计</li><li>模块接口定义</li><li>数据流设计</li></ul>
  </div>
  <div class="col">
    <ul class="demo-circle"><li>系统架构设计</li><li>模块接口定义</li><li>数据流设计</li></ul>
  </div>
</div>

<strong>双栏列表（buaa-am-cols2-ul--sq / buaa-am-cols2-ol--sq）：</strong>

<div class="demo-cols2">
  <div class="col">
    <ul><li>系统管理模块</li><li>用户权限管理</li><li>数据报表生成</li><li>日志审计追踪</li><li>消息通知推送</li><li>配置中心管理</li></ul>
  </div>
  <div class="col">
    <ol><li>需求分析阶段</li><li>原型设计阶段</li><li>开发编码阶段</li><li>测试验证阶段</li><li>部署上线阶段</li><li>运维监控阶段</li></ol>
  </div>
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">6</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">07</div>

# 图标列表与 Callout

## Icon List & Callout

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 20px; --text-p-line-height: 1.5; }
.demo-icon-list { list-style: none; padding: 0; margin: 10px 0; width: 100%; }
.demo-icon-list li { font-size: 21px; color: #333; padding: 5px 0; display: flex; align-items: center; }
.demo-icon-list li::before { content: "▸ "; color: var(--buaa-primary); font-weight: bold; font-size: 22px; margin-right: 8px; }
</style>

<div class="buaa-chapter__badge"><span>7</span></div>

## 图标列表 + Callout——效果对比

<div class="buaa-chapter__body buaa-layout--center">

<strong>图标装饰列表（buaa-am-icon-list）：</strong>

<ul class="demo-icon-list">
  <li>跨平台部署：一次构建，多端运行</li>
  <li>热更新支持：无需重新打包，实时推送</li>
  <li>性能监控：内置 APM，自动追踪慢查询</li>
  <li>安全审计：全链路日志，满足合规要求</li>
</ul>

<strong>Callout 提示框（buaa-callout）：</strong>

<div class="buaa-callout">
<strong>Callout vs 彩色引用块的区别：</strong>Callout 更宽更高，适合长文本提示（浅蓝背景 + 蓝色左边框 5px）；彩色引用更紧凑，适合短句强调。不建议同一页面混用超过两种强调组件。
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">7</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">08</div>

# 页面级网格布局

## Page-Level Grid Layout

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 19px; --text-p-line-height: 1.4; }
.demo-grids { display: flex; flex-direction: column; gap: 14px; width: 100%; }
.demo-grids .grid-row { display: flex; gap: 20px; width: 100%; }
.demo-grids .grid-row .zone {
  flex: 1; padding: 12px 16px; border-radius: 8px;
  background: rgba(var(--buaa-primary-rgb), 0.03);
  border: 1px dashed rgba(var(--buaa-primary-rgb), 0.15);
}
.zone-title { font-size: 18px; font-weight: 700; color: var(--buaa-primary); margin-bottom: 6px; }
.zone .mini-cols { display: flex; gap: 10px; }
.zone .mini-cols > div {
  flex: 1; padding: 6px 10px; border-radius: 4px;
  background: rgba(var(--buaa-primary-rgb), 0.06); font-size: 17px;
  line-height: 1.3; color: #555;
}
</style>

<div class="buaa-chapter__badge"><span>8</span></div>

## 两栏 / 三栏 / 品字型——效果对比

<div class="buaa-chapter__body buaa-layout--center">

<div class="demo-grids">
  <div class="grid-row">
    <div class="zone">
      <div class="zone-title">1. 两栏五五分 cols--2</div>
      <div class="mini-cols">
        <div>左侧 .ldiv<br>50% 宽度</div>
        <div>右侧 .rdiv<br>50% 宽度</div>
      </div>
    </div>
    <div class="zone">
      <div class="zone-title">2. 三栏均分 cols--3</div>
      <div class="mini-cols">
        <div>左 .ldiv<br>1fr</div>
        <div>中 .mdiv<br>1fr</div>
        <div>右 .rdiv<br>1fr</div>
      </div>
    </div>
  </div>
  <div class="grid-row">
    <div class="zone" style="flex: 2;">
      <div class="zone-title">3. 品字型 pin--3（上通栏 + 下两栏）</div>
      <div style="background:rgba(var(--buaa-primary-rgb),0.06);padding:6px 10px;border-radius:4px;font-size:17px;color:#555;margin-bottom:6px;">上部 .tdiv — 通栏全宽，放置总述内容</div>
      <div class="mini-cols">
        <div>左下 .ldiv</div>
        <div>右下 .rdiv</div>
      </div>
    </div>
  </div>
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">8</div>

---

<!-- _class: buaa-transition -->

<div class="buaa-transition__num">09</div>

# 综合混排

## Mixed Layout Demo

---

<!-- _class: buaa-chapter -->

<style scoped>
section { --text-p-size: 19px; --text-p-line-height: 1.5; }
.demo-mix-nav {
  width: 100%; padding: 5px 16px; background: rgba(var(--buaa-primary-rgb), 0.08);
  display: flex; justify-content: space-between; color: var(--buaa-primary);
  font-size: 15px; border-radius: 4px; flex-shrink: 0;
}
.demo-mix-pill {
  display: inline-block; background: var(--buaa-primary); color: #fff;
  padding: 5px 16px; border-radius: 6px; font-size: 20px; font-weight: 700;
  margin: 10px 0 6px 0;
}
.demo-mix-cards { display: flex; gap: 12px; width: 100%; margin: 8px 0; }
.demo-mix-cards .mix-card {
  flex: 1; padding: 10px 14px; border-radius: 8px; font-size: 17px; line-height: 1.4;
  background: linear-gradient(135deg, rgba(0,79,158,0.07), rgba(0,79,158,0.02));
  border: 1px solid rgba(var(--buaa-primary-rgb), 0.06);
}
.mix-card strong { font-size: 19px; display: block; margin-bottom: 4px; }
.mix-footnote {
  border-top: 1.8px dashed var(--buaa-primary); padding-top: 8px;
  margin-top: 8px; font-size: 17px; color: #888; flex-shrink: 0;
}
</style>

<div class="buaa-chapter__badge"><span>9</span></div>

## 多组件叠加——页面class组合 + 组件嵌套

<div class="buaa-chapter__body buaa-layout--center">

<div class="demo-mix-nav">
  <span>09 · 综合混排</span>
  <span>3 / 3</span>
  <span>Awesome-Marp</span>
</div>

<span class="demo-mix-pill">组件嵌套展示 — 多种效果组合使用</span>

<div class="demo-mix-cards">
  <div class="mix-card">
    <strong>CSS 变量</strong>
    全局管理主题色 · 运行时切换 · 继承覆盖灵活
  </div>
  <div class="mix-card">
    <strong>响应式设计</strong>
    弹性布局优先 · 断点合理划分 · 内容优先于设备
  </div>
  <div class="mix-card">
    <strong>动画优化</strong>
    仅 animatable 属性 · will-change 谨慎 · 硬件加速
  </div>
</div>

<div class="buaa-callout" style="margin:0;">
<strong>设计原则：</strong>外部容器决定布局（网格 / 分栏），内部元素决定样式（卡片 / 列表），各司其职，互不干扰。
</div>

<div class="mix-footnote">
脚注：本页综合演示 navbar + fixedtitle + card-grid + callout + footnote 五种组件的嵌套组合效果
</div>

</div>

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">9</div>

---

<!-- _class: buaa-end -->

<div class="buaa-chapter__badge"><span>结语</span></div>

# 感谢您的观看与收听，敬请批评指正

## Q &amp; A

<div class="buaa-chapter__footer"></div>
<div class="buaa-chapter__page-num">10</div>
