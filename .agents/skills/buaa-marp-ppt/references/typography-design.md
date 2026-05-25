# BUAA Marp 排版设计参考规范

> 当用户要求「参照项目风格」或「符合北航VI规范」生成时，优先参考以下标准。

---

## 基础参数

| 参数 | 值 | 说明 |
|------|:--:|------|
| 画布尺寸 | 33.9 × 19.1 cm | 标准 16:9 宽屏 |
| 布局模式 | 空白（Blank） | 不使用预设占位符，纯文本框自由排版 |

---

## 字体体系

| 字体 | 角色 | 用途 |
|------|:--:|------|
| **HarmonyOS Sans SC Medium** | 主力 | 标题、正文、表格内容 |
| Noto Sans SC | 辅助 | 正文 |
| HarmonyOS Sans SC | 辅助 | 副标题、补充文字 |
| 微软雅黑 | 备选 | 兼容性回退 |

Marp 中设定字体栈：

```css
font-family: "HarmonyOS Sans SC", "Noto Sans SC", "Microsoft YaHei", sans-serif;
```

---

## 字号层级

| 字号 | 层级 | 用途 | Marp 映射 |
|:----:|:--:|------|-----------|
| **24pt** | **正文主力** | 段落文字 | `--text-p-size: 24px` |
| 22pt | 正文辅助 | 内容文字 | `--text-size: 22px` |
| 20pt | 内容/表格 | 表格正文 | `--text-size: 20px` |
| 12-14pt | 小字 | 表格内容、注释 | — |
| 11pt | 最小 | 脚注 | — |
| 73-96pt | 封面 | 封面主标题 | `buaa-cover h1` 硬编码 |
| 38-40pt | 封面 | 封面副标题 | `buaa-cover h2` 硬编码 |
| 28pt | 强调 | 页面强调标题 | `h2` 默认字号 |

---

## 颜色体系

| 色值 | 角色 | 用途 |
|------|:--:|------|
| **#005BAC** | **主色** | 标题、强调、表头、图形着色 |
| #505050 | 正文灰 | 正文段落 |
| #FF0000 | 强调红 | 关键词强调、警示信息 |
| #333333 | 深灰 | 正文深色 |
| #FFFFFF | 反白 | 深色背景上的文字 |
| #0078D7 | 辅助蓝 | 链接、高亮 |
| #009688 | 辅助青绿 | 图表点缀 |
| #D97706 | 辅助橙 | 图表点缀 |

主色 `#005BAC` 可映射为 `--buaa-primary: #005BAC` 覆盖默认蓝。

---

## 推荐布局类型

### 优先使用

- 顶部标题 + 下方段落/列表（占 70%+）
- 标题 + 居中表格（含表头着色）
- 标题 + 左侧文字 + 右侧图片
- 封面/结尾页

### 避免过度复杂

- 多图片画廊（img-gallery）— 不兼容图注
- 系统框图（block-diagram）— 仅在明确需求时使用
- 双栏密集对比（split-top）— 注意字号需缩小至 19px
- 图片固定 max-height — 已废弃，改用 Grid 居中 + 双向约束模式（见 layout-templates.md 附录）

---

## 样式优先级

| 优先级 | 方式 | 可靠性 |
|:---:|------|:---:|
| 1（最高） | inline `style="..."` | ✅ 始终有效 |
| 2 | `<style scoped>` 中 `section { --var: val; }` | ✅ 唯一可靠 scoped 方式 |
| 3 | `<style scoped>` 中直接写选择器 | ⚠️ 不可靠，specificity 常不足 |
| 4（最低） | `buaa.css` 全局默认 | 默认值 |

详细失效原因与有效写法见 SKILL.md Scoped 样式覆盖指南。

---

## 常见错误速查

| 错误写法 | 正确做法 | 原因 |
|----------|----------|------|
| `.text-block` 内用 `<p>` | 裸写文字 | `<p>` 阻断 KaTeX |
| 把大纲 `1. item` 转为 `<ol><li>item</li></ol>` | 保留 `1. item` 原生语法 | HTML `<li>` 阻断 `$...$` 和 `**text**`，且丧失 Markdown 原生可读性 |
| HTML `<li>` 内写 `$...$` | 用 Markdown 原生列表或 `<i>x</i><sub>1</sub>` | HTML `<li>` 不经 KaTeX 处理 |
| `## 标题` 不完整 | `## 主标题——副标题` | 大纲给了就要用 |
| 多页同编号未细化 | 自动细化 X.Y.Z | 见 SKILL.md 规则 |
| 目录 `ul` 无 inline style | 必须有 `style="position:absolute;..."` | scoped CSS 可能被忽略 |
| `<footer>` 标签 | `<div class="footer-bar">` | Marp 不白名单 footer |
| 幻灯片内 `---` | `<hr>` | `---` 是分隔符 |
| `<img class/style>` | 父 div class + CSS 选择器 | Marp 剥离 img 的 class/style |
| scoped 中 `pre { font-size }` | `section { --pre-font-size: 22px; }` | specificity 不足 |
| 修改 `buaa.css` 全局样式 | 在 `.md` 中 `section { --var: val; }` | CSS 变量注入不依赖 specificity |
