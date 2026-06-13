# BUAA Marp 排版设计参考规范

> 当用户要求「参照项目风格」或「符合北航VI规范」生成时，优先参考以下标准。

---

## 基础参数

| 参数 | 值 | 说明 |
|------|:--:|------|
| 画布尺寸 | 1280 × 720 px | 标准 16:9 宽屏 |
| 布局模式 | 空白（Blank） | 纯文本框自由排版 |

---

## 字体体系

| 字体 | 角色 | 用途 |
|------|:--:|------|
| **HarmonyOS Sans SC Medium** | 主力 | 标题、正文、表格内容 |
| Noto Sans SC | 辅助 | 正文 |
| 微软雅黑 | 备选 | 兼容性回退 |
| Cascadia Code | 代码 | 代码块等宽字体 |

Marp 中设定字体栈：

```css
font-family: "HarmonyOS Sans SC", "Noto Sans SC", "Microsoft YaHei", sans-serif;
```

---

## 字号层级

| 用途 | CSS 变量 / 目标 | 默认值 |
|------|------|:--:|
| 封面主标题 | `buaa-cover h1` 硬编码 | 73-96pt |
| 封面副标题 | `buaa-cover h2` 硬编码 | 38-40pt |
| 正文段落 | `--text-p-size` | **26px** |
| 正文列表 | `--text-size` | 24px |
| 表格内容 | 继承段落字号 | ~22px |
| 代码块 | `--pre-font-size` | 22px |
| 行内代码 | `--code-font-size` | 0.9em |
| 脚注/注释 | `--text-size` 调小 | 18-20px |

---

## 颜色体系

| 色值 | 角色 | 用途 |
|------|:--:|------|
| **#004F9E** | **主色（北航蓝）** | 标题、强调、表头、badge、图形着色 |
| #003D7A | 主色深 | 表格边框、表头 |
| #333333 | 正文深灰 | 段落文字 |
| #444-#666 | 辅助灰 | 递减层级 |
| #FF0000 | 强调红 | 关键词强调、警示信息 |
| #FFFFFF | 反白 | 深色背景上的文字 |
| rgba(0,79,158,0.06) | 浅蓝背景 | 表格条纹、callout、代码行内背景 |

各主题变体通过 CSS 变量 `--buaa-primary` 覆盖主色。

---

## 推荐布局类型

### 优先使用

- 顶部标题 + 下方段落/列表（布局 B，占 70%+）
- 标题 + 居中表格（布局 C）
- 标题 + 左文右图（布局 A）
- 封面/结尾页

### 避免过度复杂

- 多图片画廊（img-gallery）— 不兼容图注
- 系统框图（block-diagram）— 仅在明确需求时使用
- 双栏密集对比（split-top）— 注意字号需缩小至 19px
- 图片固定 max-height — 已废弃，改用 Grid 居中 + 双向约束模式

---

## 样式优先级

| 优先级 | 方式 | 可靠性 | 适用 |
|:---:|------|:---:|------|
| 1（最高） | inline `style="..."` | ✅ 始终有效 | 目录 ul |
| 2 | `<style scoped>` 中 `section { --var:val }` | ✅ 可靠 | pre / code / table / p |
| 3 | `<style scoped>` 中直接写选择器 | ✅ ol/ul/callout/hm-fig 可用 | 见 SKILL.md §2.4 安全列表 |
| 4（最低） | `buaa.css` 全局默认 | 默认值 | 无需覆盖时 |

---

## 常见错误速查

| 错误写法 | 正确做法 | 原因 |
|----------|----------|------|
| `.text-block` 内用 `<p>` | 裸写文字 | `<p>` 阻断 KaTeX |
| 把大纲 `1. item` 转为 `<ol><li>` | 保留原生语法 | HTML `<li>` 阻断 `$...$` 和 `**text**` |
| HTML `<li>` 内写 `$...$` | 用原生列表或 `<i>x</i><sub>1</sub>` | HTML `<li>` 不经 KaTeX |
| `## 标题` 不完整 | `## 主标题——副标题` | 大纲给了就要用 |
| 多页同编号未细化 | 自动细化 X.Y.Z | 见约束 #10 |
| 目录 `ul` 无 inline style | 必须 `style="position:absolute;..."` | inline 最可靠 |
| `<footer>` 标签 | `<div class="buaa-chapter__footer">` | Marp 不白名单 footer |
| 幻灯片内 `---` | `<hr>` | `---` 是分页符 |
| `<img class/style>` | 父 div class + CSS 选择器 | Marp 剥离 img class/style |
| scoped 中 `pre { font-size }` | `section { --pre-font-size:22px }` | specificity 不足 |
| 修改 `buaa.css` 全局样式 | 在 `.md` 中 `section { --var:val }` | CSS 变量注入 |
