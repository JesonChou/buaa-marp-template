# BUAA 系统框图样例规范

> **用途**：AI 生成新的系统框图时，参照此样例的 CSS 变量体系、类命名约定、间距策略。
> 以下规范以 TLP 测试系统组成（中心枢纽 DUT + 四向设备链）为典型参考布局。

---

## 一、页面骨架

```
page-type: chapter
layout: layout-center
badge: 2.3
title: TLP 测试系统组成——系统框图
components: block-diagram + callout
```

---

## 二、CSS 变量体系

### 2.1 区块级全局变量（在 `.block-diagram` 上声明）

| 变量 | 推荐值 | 说明 |
|------|:---:|------|
| `--bd-node-font-size` | 18px | 普通节点字号 |
| `--bd-hub-font-size` | 36px | 枢纽节点字号 |
| `--bd-gap` | 10px | Grid 九宫格 cell 间距 |
| `--arr-color` | #004F9E | 所有箭头颜色 |
| `--arr-length` | 40px | 长尾箭头尾长 |
| `--line-width` | 2px | 箭头线宽（三角同步缩放） |

### 2.2 位置与间距变量

| 变量 | 推荐值 | 说明 |
|------|:---:|------|
| `--node-pad-x` | 20px | 节点左右内边距 |
| `--node-pad-y` | 10px | 节点上下内边距 |
| `--arr-gap-x` | 10px | 水平箭头 ↔ 节点间距 |
| `--arr-gap-y` | 10px | 垂直箭头 ↕ 节点间距 |

### 2.3 间距规则应用

```css
/* 节点内边距 */
.bd-node { padding: var(--node-pad-y) var(--node-pad-x) !important; }
/* 水平箭头间距 */
.bd-chain:not(.bd-vertical) .bd-arrow {
  margin-left:  var(--arr-gap-x) !important;
  margin-right: var(--arr-gap-x) !important;
}
/* 垂直箭头间距 */
.bd-chain.bd-vertical .bd-arrow {
  margin-top:    var(--arr-gap-y) !important;
  margin-bottom: var(--arr-gap-y) !important;
}
```

---

## 三、类命名约定

### 3.1 单箭头类：`a-*`

格式：`.a-{位置}`，在 scoped CSS 中覆写 `--arr-length` / `--line-width` / `--arr-color`

| class | 含义 | 方向 |
|-------|------|:---:|
| `.a-top` | 顶部终端箭头 | down/up |
| `.a-l-mid` | 左链内部箭头 | right |
| `.a-l-end` | 左链终端箭头 | right |
| `.a-r` | 右链箭头 | left |
| `.a-bot-end` | 底部终端箭头 | up |
| `.a-bot-mid` | 底部内部箭头 | up |

### 3.2 单节点类：`n-*`

格式：`.n-{名称}`，在 scoped CSS 中用 `margin` 或 `transform` 微调位置

| class | 节点 |
|-------|------|
| `.n-top` | 探针台（夹具） |
| `.n-gen` | 脉冲发生器 |
| `.n-tline` | 传输线 |
| `.n-dc` | 直流偏置/漏电流测量单元 |
| `.n-probe` | 电压、电流探头 |
| `.n-scope` | 高速示波器 |

### 3.3 链布局类

| class | 作用 |
|-------|------|
| `.bd-chain` | 默认（居中 flex row） |
| `.bd-chain.bd-vertical` | 纵向 flex column |
| `.bd-chain.bd-spread` | `justify-content: space-between`（水平均匀分布） |

### 3.4 箭头伸缩

| class | 作用 |
|-------|------|
| `.arr-fill` | `flex: 1`，箭头自动填充节点间剩余空间 |

---

## 四、箭头方向速查

箭头方向由 HTML class 中的方向后缀决定：

| class 后缀 | 方向 | 视觉 |
|:---|:---:|:--:|
| `-right` | 向右 → | `arr-line-long-right` |
| `-left` | 向左 ← | `arr-line-long-left` |
| `-down` | 向下 ↓ | `arr-line-long-down` |
| `-up` | 向上 ↑ | `arr-line-long-up` |

---

## 五、箭头样式选择

| style class | 视觉 | 场景 |
|------|:--:|------|
| `arr-solid-*` | ▶ 实心三角 | 默认粗壮 |
| `arr-outline-*` | ⪢ 空心V形 | 现代科技 |
| `arr-line-*` | → 细线短尾(24px) | 学术紧凑 |
| `arr-line-long-*` | —→ 细线长尾(60px) | **框图推荐** |
| `arr-double-*` | ⇒ 双线 | 数据流 |

---

## 六、节点排列模式（链内方向推断）

| Grid 位置 | flex 方向 | 箭头默认 | Hub 在末尾 | Hub 在开头 |
|:---:|:---:|:---:|:---:|:---:|
| `left` / `right` | 横向 `flex row` | → / ← | 向心 | 离心 |
| `top` / `bottom` | 纵向 `flex column` | ↑ / ↓ | 向心 | 离心 |

---

## 七、终端箭头位置规则

终端箭头应放在链中**贴近 Hub 的那一侧**：
- `left` 链 → 终端箭头在最右侧（最后一个子元素）
- `right` 链 → 终端箭头在最左侧（第一个子元素）
- `top` 链 → 终端箭头在最下方（`bd-vertical` 中最后一个子元素）
- `bottom` 链 → 终端箭头在最上方（`bd-vertical` 中第一个子元素）

---

## 八、完整 scoped CSS 模板

```html
<style scoped>
section { --text-p-size: 22px; --text-p-line-height: 1.5; }

/* 箭头全局 */
.block-diagram {
  --bd-node-font-size: 18px;
  --bd-hub-font-size: 36px;
  --bd-gap: 10px;
  --arr-color: #004F9E;
  --arr-length: 40px;
  --line-width: 2px;
  --node-pad-x: 20px;
  --node-pad-y: 10px;
  --arr-gap-x: 10px;
  --arr-gap-y: 10px;
}
.bd-node { padding: var(--node-pad-y) var(--node-pad-x) !important; }
.bd-chain:not(.bd-vertical) .bd-arrow {
  margin-left: var(--arr-gap-x) !important;
  margin-right: var(--arr-gap-x) !important;
}
.bd-chain.bd-vertical .bd-arrow {
  margin-top: var(--arr-gap-y) !important;
  margin-bottom: var(--arr-gap-y) !important;
}

/* 单节点微调 */
/* .n-gen { margin-right: 2px; } */

/* 单箭头覆写 */
/* .a-l-mid { --arr-length: 80px; --line-width: 4px; } */

.callout { font-size: 20px; line-height: 2; padding: 12px 22px; }
</style>
```

---

## 九、完整 HTML 模板

```html
<div class="chapter-body layout-center">
<div class="block-diagram">

  <div class="bd-top">
    <div class="bd-chain bd-vertical">
      <div class="bd-node n-top">节点名</div>
      <div class="bd-arrow arr-line-long arr-line-long-down a-top"></div>
    </div>
  </div>

  <div class="bd-left">
    <div class="bd-chain bd-spread">
      <div class="bd-node n-gen">节点A</div>
      <div class="bd-arrow arr-line-long arr-line-long-right arr-fill a-l-mid"></div>
      <div class="bd-node n-tline">节点B</div>
      <div class="bd-arrow arr-line-long arr-line-long-right a-l-end"></div>
    </div>
  </div>

  <div class="bd-center">
    <div class="bd-hub">枢纽名</div>
  </div>

  <div class="bd-right">
    <div class="bd-chain">
      <div class="bd-arrow arr-line-long arr-line-long-left a-r"></div>
      <div class="bd-node n-dc">节点C</div>
    </div>
  </div>

  <div class="bd-bottom">
    <div class="bd-chain bd-vertical">
      <div class="bd-arrow arr-line-long arr-line-long-up a-bot-end"></div>
      <div class="bd-node n-probe">节点D</div>
      <div class="bd-arrow arr-line-long arr-line-long-up a-bot-mid"></div>
      <div class="bd-node n-scope">节点E</div>
    </div>
  </div>

</div>
</div>
```

---

## 十、验证清单

生成新的系统框图后，逐项检查：

| # | 检查项 |
|---|--------|
| 1 | `.bd-hub` 深蓝填充，`.bd-node` 白底蓝边框 |
| 2 | 每个箭头都有 `a-*` 独立类 |
| 3 | 每个节点都有 `n-*` 独立类 |
| 4 | 终端箭头放在贴近 Hub 一侧 |
| 5 | `left`/`right` 链默认横向，`top`/`bottom` 默认纵向 |
| 6 | 箭头样式统一用 `arr-line-long-*` |
| 7 | 间距变量 `--arr-gap-x` / `--arr-gap-y` 已设置 |
| 8 | scoped CSS 中包含单节点 + 单箭头覆写注释块 |
| 9 | 所有 CSS 注释在代码上一行，禁止行尾注释 |

## 十一、通用元素调整 class 约定（适用于任何 chapter 页）

| class | 元素 | 可调参数 |
|-------|------|------|
| `.adj-txt` | `.text-block` / `p` | `font-size`, `line-height`, `color`, `margin` |
| `.adj-list` | `ol` / `ul` / `li` | `font-size`, `line-height`, `item-gap` |
| `.adj-img` | `.hm-fig img` | `max-height`, `margin` |
| `.adj-tbl` | `table` | `font-size`, `width` |
| `.adj-callout` | `.callout` | `font-size`, `line-height`, `padding`, `margin` |

scoped CSS 模板：
```css
/* 文本块：字号、行距、颜色 */
/* .adj-txt { font-size: 24px; line-height: 1.8; color: #333; } */
/* 列表：字号、行距、条目间距 */
/* .adj-list { font-size: 22px; line-height: 2; } */
/* 图片：最大高度、边距 */
/* .adj-img { max-height: 480px !important; margin: 10px 0; } */
/* 表格：字号 */
/* .adj-tbl { font-size: 22px; } */
/* callout：字号、行距、内边距 */
/* .adj-callout { font-size: 22px; line-height: 1.8; padding: 14px 24px; } */
```
