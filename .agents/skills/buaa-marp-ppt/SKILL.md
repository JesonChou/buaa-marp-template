---
name: buaa-marp-ppt
description: >-
  Create, edit, and manage BUAA (Beihang University) themed Marp presentations.
  USE FOR: creating BUAA-style slides, generating Marp PPT from outlines,
  auto-layout of mixed content (text/images/tables/code/equations/diagrams),
  fixing slide formatting, adding new sections, adjusting page numbers,
  styling individual tables, debugging Marp theme issues.
  DO NOT USE FOR: general Marp questions unrelated to BUAA theme;
  PPTX generation via PowerPoint; non-Marp slide frameworks.
license: MIT
metadata:
  author: BUAA
  version: "2.0.0"
  theme: buaa
  slide-size: "1366x768"
  primary-color: "#004F9E"
---

# BUAA Marp PPT 技能

为北京航空航天大学主题的 Marp 学术演示文稿提供创建、编辑和美化能力。

## ⚠️ 前置检查清单

生成 PPT 前逐项确认：

| # | 检查项 | 详情 |
|---|--------|------|
| 1 | 图注用 `.hm-cap` | 禁止 Markdown 斜体或 `.img-caption` |
| 2 | `<img>` 前后各空行 | 防止被 `<p>` 包裹 |
| 3 | 加粗用 `<strong>` | `<div>` 内 `**text**` 不被 Marp 解析 |
| 4 | 禁止 `<footer>` | 改用 `<div class="footer-bar">` |
| 5 | 禁止内容中 `---` | 改用 `<hr>` |
| 6 | `<img>` 不设 class/style | Marp 会剥离，改用父 div + CSS |
| 7 | `.chapter-body` 恰好一个对齐类 | `layout-center` / `layout-flow` / `layout-space` / `layout-between` |
| 8 | 表格在 `.layout-center` 内 | 否则不居中 |
| 9 | 仅 chapter/end 页有页码 | 封面/目录/过渡页无页码 |
| 10 | buaa.css 无 BOM | 修改后执行 Developer: Reload Window |

> **关键：生成前先通读 `references/buaa-layout-styles.md`，所有内容页必须从 8 种布局模式中选择。**

## Instructions

### Step 1: 读取环境

```powershell
# 检查 buaa.css BOM
$bytes = [System.IO.File]::ReadAllBytes("buaa-marp-template/buaa.css")
if ($bytes[0] -eq 239) { Write-Output "BOM detected!" }
```

读取 `buaa.css`、`presentation-template.md`（参考模板）和 `references/buaa-layout-styles.md`（布局模式）。

### Step 2: 确定页面结构

根据大纲确定每页的 page type（5 种）和 body layout（10 种模式，A~J）：

```
封面(cover) → 目录(catalog) → 过渡(transition) → 正文(chapter)×N → ... → 结尾(end)
```

正文页布局从 [10 种布局模式](references/buaa-layout-styles.md) 中选择。

#### 图文自动生成触发语法

当大纲中使用**自然语言缩进格式**描述图表时，自动生成对应图表：

**流程图触发：**
```
流程图（纵向）：
  → 步骤1
  → 步骤2
  → 步骤3
```
- `流程图` 独占一行 + 后续缩进 `→` 行 → 触发生成
- `（纵向）`/默认：垂直排列（`.flow-chart`），箭头 `arr-solid-down`
- `（横向）`：水平排列，箭头 `arr-solid-right`
- 每行 `→` 开头；步骤数 3~9 个；>5 步时缩小 `--fc-font-size`
- 步骤文本含 `→` 时用 `\→` 转义
- 兼容旧格式：`流程图：A→B→C`（单行退化为纵向）

**系统框图触发：**
```
系统框图：
  center: 枢纽节点名
  left: 节点A → 节点B → 枢纽节点名
  right: 节点C → 枢纽节点名
  bottom: 节点D → 节点E → 枢纽节点名
  top: 枢纽节点名 → 节点F
```
- `center:` 声明枢纽（必填，渲染为 `.bd-hub` 深蓝填充）
- **链中保留 Hub**：方向行写出完整链路，枢纽出现在链尾或链首
- **Hub 位置决定箭头方向**：Hub 在末尾 → 向心（箭头指向中心）；Hub 在开头 → 离心（箭头从中心出发）
- **位置决定链排列**：`left`/`right` → 横向 flex row；`top`/`bottom` → 纵向 flex column
- 方向行可选（`left`/`right`/`top`/`bottom`），链内 `→` 分隔
- 兼容旧格式：`系统框图关系：` + 方向标注行；`bottom（纵向）` 等旧标注自动忽略

**正文区分规则：**
- `流程图`/`系统框图` 独占一行 + 后续缩进 `→` 行 → **触发图表**
- 同行后有正文（如 `流程图：这是我们系统的...`）→ **不触发**，视为普通文本
- 箭头默认 `arr-solid` 样式，scoped 中可切换 `arr-outline` / `arr-line`
- 节点文本过长（>30字 flowchart / >15字 block-diagram）时自动缩小字号

### Step 3: 空间预评估 ⚠️ 必须执行（逐页不可跳过）

`.chapter-body` 可视区域：**宽 1246px × 高 634px**（1366×768 减去 60px 左右边距、80px 上边距、54px 下边距）。

#### 各布局空间预算

| 布局 | 文字区可用 | 图片区可用 | 关键约束 |
|------|:---:|:---:|------|
| split-2（50:50） | ~603px 宽 × ~580px 高 | ~603px 宽 × ~500px 高 | 每列宽 ~600px，列间 20px 间距 |
| split-right（68:32） | ~827px 宽 × ~580px 高 | ~379px 宽 × ~500px 高 | 图片在 379px 下是否可辨？ |
| split-tb（文上图下） | 全宽 × 自适应高 | 全宽 × (580px - 文字高) | 文字高 + img max-h + 图注 ≤ 580px |
| layout-flow（纯文字） | 全宽 × ~580px 高 | — | 条目数 × 字号 × 行距 ≤ 520px |
| layout-center（居中） | 全宽 × ~580px 高 | — | 表格行数 × 44px ≤ 400px |

#### 溢出快速判定

| 检查项 | 公式 | 安全阈值 | 超标处理 |
|--------|------|:---:|------|
| 列表条目总高 | `条目数 × (字号 × 行距 + item-gap)` | ≤ 520px | 缩小字号/行距，仍超标则拆页 |
| 散文段落高 | `估算行数 × 字号 × 行距` | ≤ 500px | 缩小 --text-p-size |
| 图片+图注 | `max-height + 30px(图注)` | ≤ 分配区高度 | 减小 max-height 或切换布局 |
| 表格行数 | `行数 × 44px + 表头 48px` | ≤ 400px | 缩小表格字号至 18~20px |
| 双列每列宽 | `最长条目字数 × 50%字号` | ≤ 列宽 - 40px | 缩小字号或换更短表述 |
| 流程图节点数 | `节点数 × (52px + 箭头 14px)` | ≤ 550px | 缩小 --fc-font-size 或 --fc-min-width |
| 框图节点总数 | `(2 + 节点数) × 60px` | ≤ 500px | 缩小 --bd-node-font-size |

**处理优先级**：① 调 CSS 变量（字号/行距）→ ② 调图片 max-height → ③ 拆页/切换布局模式。

**每页生成后必须附带 `/* === 文本密度调节 === */` scoped 块**，供后续手动微调。

### Step 4: 生成正文页

每页使用标准骨架：

```html
<!-- _class: chapter -->
<div class="chapter-badge"><span>X.Y</span></div>
## 主标题——副标题
<div class="chapter-body layout-xxx">
  <!-- 从 10 种布局模式中选择一种 -->
</div>
<div class="footer-bar"></div>
<div class="page-num">N</div>
```

> **生成系统框图（模式 J）时**：必须参照 [`references/buaa-block-diagram-example.md`](references/buaa-block-diagram-example.md) 中的完整规范——包括 CSS 变量体系、`a-*`/`n-*` 类命名约定、终端箭头位置规则、间距变量等。该样例以中心枢纽 + 四向设备链为典型布局参考。

### Step 5: 应用格式化规则

- **加粗** ⚠️: `<strong>text</strong>`（禁止 `**text**`）
- **图注** ⚠️: `<div class="hm-cap">text</div>`（禁止其他样式）
- **图片**: `hm-fig` 容器 + `<img>` 前后空行
- **目录**: `ul { left: 730px }` 不设 width，`gap: 28px`，`li { font-size: 24px }`
- **副标题** ⚠️: 若大纲中未说明副标题，则 `##` 标题中不加 `——副标题`，仅保留主标题
- **长文本密度调节** ⚠️: **每个 chapter slide 必须附带文本密度调节块**。首选 CSS 变量方式（简洁通用），仅当需逐元素精细控制时用逐元素规则。**禁止**通过修改 `buaa.css` 来调节
- **重要图片放大** ⚠️: 图片需要放大时，在 scoped 块中加 `.hm-fig img { max-height: XXXpx !important; }`，不改 `buaa.css`
- **注释规范** ⚠️: CSS 注释放在被描述代码的**上一行**，禁止行尾注释
- **元素调整 class** ⚠️: 生成每个 chapter 页时，正文元素必须加独立调整 class（`.adj-txt`/`.adj-list`/`.adj-img`/`.adj-tbl`/`.adj-callout`），并在 scoped CSS 中附带注释掉的调整块。参照 `buaa-block-diagram-example.md` 第十一章

### CSS 变量钩子（buaa.css 已内置，覆盖所有文本元素）

| 变量名 | 默认值 | 控制范围 | 常用覆写值 |
|--------|:---:|------|:---:|
| `--text-size` | 24px | `li`、`.callout` 字号 | 22px（列表为主）/ 19px（密集双列） |
| `--text-line-height` | 1.8 | `ol`/`ul`/`li`/`.callout` 行距 | 2~3（列表）/ 2.4（密集双列） |
| `--text-item-gap` | 8px | `li` 条目间距 | 4~6px（密集）/ 8~16px（松散） |
| `--text-p-size` | 26px | `p`、`.text-block`、split 容器裸文字 字号 | 26px（标准）/ 28px（短文字）/ 24px（密集） |
| `--text-p-line-height` | 1.7 | `p`、`.text-block`、split 容器裸文字 行距 | 1.5~1.7（中等）/ 2（短文字+大图）/ 1.5（密集） |

**首选模板（每个 chapter slide 都要有，参数值按排版参数速查表选取）：**

```html
<style scoped>
/* === 图片尺寸 ===（有图时必写） */
/* 图片最大高度 */
/* .hm-fig img { max-height: XXXpx !important; } */

/* === 文本密度调节 === 覆写 CSS 变量即可，无需逐元素写规则 */
section {
  --text-size: 22px;
  --text-line-height: 2;
  --text-item-gap: 6px;
  --text-p-size: 26px;
  --text-p-line-height: 1.7;
}

/* === 图文间距 ===（仅 split-tb 布局） */
/* 文字与图片之间的间距 */
/* .split-tb { gap: 1px; } */

/* 以下为逐元素调整占位块（注释掉，按需取消注释） */
/* 文本块：字号、行距、颜色 */
/* .adj-txt { font-size: 24px; line-height: 1.8; color: #333; } */
/* 列表：字号、行距 */
/* .adj-list { font-size: 22px; line-height: 2; } */
/* 图片：最大高度、边距 */
/* .adj-img { max-height: 480px !important; margin: 10px 0; } */
/* 表格：字号 */
/* .adj-tbl { font-size: 22px; } */
/* callout：字号、行距、内边距 */
/* .adj-callout { font-size: 22px; line-height: 1.8; padding: 14px 24px; } */
</style>
```

### Step 6: 编号

- **章节编号**: 该章仅 1 页正文 → 单数字；≥2 页 → X.Y 格式；子节使用 X.Y.Z 格式
- **编号层级**: 章节编号最多 3 级（如 `1.1.1`），禁止更深层级（如 `1.1.1.1`）
- **页码**: 封面/目录/过渡无页码，正文从 1 开始连续，结尾页最后

---

## 布局模式速查

> 完整规范见 [`references/buaa-layout-styles.md`](references/buaa-layout-styles.md)

| 模式 | 组件 | 适用场景 |
|------|------|----------|
| A 文左图右 | `split-2` + `hm-fig` | ⭐ **图文默认布局**：散文段落 / bullet 列表（≤5条）/ 任意图片 |
| B 文宽图窄 | `split-right` + `hm-fig` | ⚠️ **最后手段**：仅当 bullet 列表 >5 条、多条 >60 字、图片为辅助示意图 |
| C 三卡+图廊 | `card-grid card-3` + `img-gallery gal-3` | 3 概念并列 + 3 张图 |
| D 三卡+单图 | `card-grid card-3` + `hm-fig` | 3 方法对比 + 总结图 |
| E 三卡+双图 | `card-grid card-3` + `img-pair` + `hm-cap` | 3 趋势 + 2 张图（各有图注） |
| F 时间轴 | `timeline` + `callout` | 5 里程碑 + 总结句 |
| G 图标总结 | `split-right` + `icon-list` + `hm-fig` | 4 条总结 + 展望图 |
| H 双栏对比 | `split-2 split-top` + `callout` | 两类并列内容（如通用 vs 硬件），各 3~5 条目 + 底部总结句 |
| I 流程图 | `flow-chart` + `fc-node` + `arr-solid-down` | 3~9 个串行步骤，大纲以"流程图"缩进格式标注 |
| J 系统框图 | `block-diagram` + `bd-hub` + `bd-chain` + `bd-node` | 中心枢纽 + 四向节点链，大纲以"系统框图"缩进格式标注 |

### ⚠️ 图文布局决策铁律（必读）

> 经验证：split-2 可覆盖绝大多数图文并排场景，split-tb 专用于技术大图，**split-right 仅在极端条件下使用**。

#### 第一铁律：split-2 是图文左右并排的唯一默认布局

**散文段落 + 图 → split-2（永远）。散文在 50% 列宽自然换行即可，不需要 68% 宽列。**

**bullet 列表 + 图 → split-2（首选）。优先通过缩小字号（22→20→19px）解决溢出，而非切换布局。**

#### 第二铁律：split-right 仅限以下 ALL 条件同时满足

1. 内容是 bullet 列表（不是散文）
2. 条目 ≥4 条，多条 >60 字
3. 图片是辅助示意图（在 32% 宽度下仍可辨）
4. 已尝试 split-2 + 字号降至 19px 仍溢出

#### 第三铁律：split-tb 仅用于"图需全宽展示细节"

| 图片类型 | 文字上限 | 典型场景 |
|----------|:---:|------|
| 技术原理图（含标注/箭头/多组件） | ≤180 字 | 电路图、测试系统框图 |
| 数据曲线图（含多曲线/坐标轴） | ≤150 字 | I-V 特性曲线、时域波形 |
| 流程图（非 I/J 模式生成） | ≤120 字 | 系统工作流 |

**照片/渲染图/封面图 → 不用 split-tb，用 split-2（50% 宽足够）。**

#### 横竖排版决策矩阵

```
有文字 + 有图片 →
├─ 图片是照片/渲染图？ → split-2（无条件）
├─ 图片是技术原理图/曲线图/框图？
│   ├─ 文字 ≤ 180 字 → split-tb
│   └─ 文字 > 180 字 → split-2
├─ 文字是散文段落？ → split-2（无条件）
├─ 文字是 bullet 列表？
│   ├─ ≤3条, 每条≤40字 → split-2
│   ├─ 3~5条, 部分>40字 → split-2 + 字号降至 20px
│   ├─ >5条, 多条>60字 → 优先拆页；不拆则 split-2 + 字号降至 19px
│   └─ >5条, 多条>80字, 图辅助 → split-right（最后手段）
└─ 只有文字（无图）？ → layout-flow 或 layout-center
```

---

## 常见陷阱

| 错误 | 正确 | 原因 |
|------|------|------|
| `<footer>` | `<div class="footer-bar">` | Marp 不白名单 footer |
| 幻灯片内 `---` | `<hr>` | `---` 会分割幻灯片 |
| `<img class="x">` | 父 div class + CSS `.x img` | Marp 剥离 img 的 class/style |
| `**text**` 在 div 内 | `<strong>text</strong>` | HTML 块内不解析 Markdown |
| `*图注*` 或 `.img-caption` | `.hm-cap` | 图注必须统一 hm-cap 样式 |
| `width:100%` + padding | + `box-sizing:border-box` | 总宽溢出被 overflow 裁掉 |
| 目录 `left:563px` | `left:730px` | 错误约束推导，正确为右半区居中 |
| 表格在 `layout-flow` 中 | 用 `layout-center` + `.text-block` 包裹文本 | `<style scoped>` 对 Marp 表格无效，必须靠 `.layout-center table` 规则 |
| 修改 `buaa.css` 调字号/行距 | 在 `.md` 中加 `<style scoped>`（`/* === 文本密度调节 === */`）| 用户偏好：样式微调始终在 `.md` 文件中完成，不改全局 CSS |

---

## 目录页精确定位

```
PPT 宽度 1366px，中心 683px
条目块在右半区（683→1366px）中自然居中
ul { left: 730px }  ← 不设 width，块宽由内容自适应
ul { display: flex; flex-direction: column; gap: 28px }
li { font-size: 24px; margin-bottom: 0 }
```

调整纵向间距：改 `gap` 值即可（20px 紧凑 / 28px 标准 / 36px 舒展）。

Marp 缓存 CSS → 需 **Developer: Reload Window**。若不生效 → inline style 兜底。

---

## 表格

- 表格居中**必须**放在 `.layout-center` 容器内（`.layout-center table` 规则将 `width:100%` 覆写为 `width:auto; margin:auto`）
- `<style scoped>` 加 `!important` 对 Marp markdown 生成的 `<table>` 无效，不可依赖
- **混合文本+表格的 slide**：用 `layout-center`，同时将文本段落包裹在 `.text-block`（`width:100%`）中保持左对齐；多个 `.text-block` 之间、`.text-block` 与表格之间用 `<br>` 分隔，保持呼吸感
- 表头 `background: #004F9E; color: #fff`
- 偶数行 `background: #f4f8fc`
- 自定义：内联 `style="width:70%;font-size:18px"` 或 CSS class

---

## Troubleshooting

| 症状 | 原因 | 解决 |
|------|------|------|
| 主题无法识别 | buaa.css 有 UTF-8 BOM | PowerShell 去 BOM |
| 图注变灰斜体 | 用了 `*text*` 或 `.img-caption` | 改用 `.hm-cap` |
| 图片不居中 | `<img>` 被 `<p>` 包裹 | `<img>` 前后各加空行 |
| 加粗显示星号 | `**text**` 在 `<div>` 内 | 改用 `<strong>` |
| 目录贴右边缘 | `ul` 的 `left` 值错误 | 设为 `730px` |
| 右侧内容被截断 | `width:100%` + padding 溢出 | 加 `box-sizing:border-box` |
| 修改 buaa.css 不生效 | Marp 扩展缓存 | Developer: Reload Window |
| 表格不居中 | 父容器不是 `layout-center` | 加 `layout-center` |
