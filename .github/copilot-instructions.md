# BUAA Marp PPT 项目规范

> 最后更新: 2026-05-24 | 本文件为项目级配置与快速参考。完整生成规范见 [SKILL.md](.agents/skills/buaa-marp-ppt/SKILL.md)。

## 适用范围

`buaa-marp-template/` 目录下所有 `.md` 文件的 Marp 幻灯片生成和编辑。

---

## 项目配置

### 主题文件

| 文件 | 主题名 | 主色 |
|------|--------|:----:|
| `themes/buaa.css` | `buaa`（默认） | #004F9E |
| `themes/buaa-red.css` | `buaa-red` | #C41230 |
| `themes/buaa-gold.css` | `buaa-gold` | #C49B2C |
| `themes/buaa-dark.css` | `buaa-dark` | #1B2D55 |
| `themes/buaa-green.css` | `buaa-green` | #2E7D32 |
| `themes/buaa-purple.css` | `buaa-purple` | #5C2D91 |

### 切换与注册

- **切换主题**：修改 `.md` 文件 YAML 头 `theme: buaa-red`
- **注册新主题**：编辑 `.vscode/settings.json` → `markdown.marp.themes` 数组添加路径
- **修改 CSS 后生效**：VS Code → **Developer: Reload Window**

### 样式优先级

| 优先级 | 方式 | 可靠性 |
|:---:|------|:---:|
| 1（最高） | inline `style="..."` | ✅ 始终有效 |
| 2 | `<style scoped>` 中 `section { --var: val; }` | ✅ 唯一可靠 scoped 方式 |
| 3 | `<style scoped>` 中直接写选择器 | ⚠️ 不可靠，specificity 常不足 |
| 4（最低） | `buaa.css` 全局默认 | 默认值 |

> 详细失效原因与有效写法见 SKILL.md §九（Scoped 样式覆盖指南）

---

## 快速参考

### 页面结构与页码

```
封面 → 目录 → 过渡 → 正文×N → 结尾
```

- 封面/目录/过渡页：无页码
- 正文页：从 1 开始连续递增
- 结尾页：有页码

### 图片规范

| 规则 | 说明 |
|------|------|
| 容器 | `<div class="buaa-hm-fig">` |
| 空行 | `<img>` 前后各留空行，防止被 `<p>` 包裹 |
| 图注 | `<div class="buaa-hm-cap">text</div>`（16px/#000/bold/微软雅黑） |
| 双图 | 用 `img-pair` + `hm-cap`（不用 `img-gallery`，不兼容图注） |
| 下载 | 大纲指明 URL 时，下载至 `figures/`，`.md`中以 `./figures/xxx.png` 引用 |

### 内容忠实原则

1. 严格按大纲逐页生成，大纲中没有的内容一律不添加
2. 图片仅在大纲明确标注图片文件名时才插入
3. 图注仅在大纲以"图注："标注时才使用 `.buaa-hm-cap`
4. 标题严格沿用大纲中的编号和标题，一字不改

### 输出文件命名

生成的 `.md` 文件以 PPT 主题命名，**不加**「大纲」「outline」「presentation」等后缀。

> 例：大纲名为 `EMC_Measure_TLP-outline.md` → 生成 `EMC_Measure_TLP.md`

### 结尾页固定文本

结束语固定为：**感谢您的观看与收听，敬请批评指正**（禁止"感谢聆听"等变体）

---

## 排版设计参考规范

> 当用户要求「参照项目风格」或「符合北航VI规范」生成时，优先参考以下标准。

### 基础参数

| 参数 | 值 | 说明 |
|------|:--:|------|
| 画布尺寸 | 33.9 × 19.1 cm | 标准 16:9 宽屏 |
| 布局模式 | 空白（Blank） | 不使用预设占位符，纯文本框自由排版 |

### 字体体系

| 字体 | 角色 | 用途 |
|------|:--:|------|
| **HarmonyOS Sans SC Medium** | 主力 | 标题、正文、表格内容 |
| Noto Sans SC | 辅助 | 正文 |
| HarmonyOS Sans SC | 辅助 | 副标题、补充文字 |
| 微软雅黑 | 备选 | 兼容性回退 |

> Marp 中设定 `font-family: "HarmonyOS Sans SC", "Noto Sans SC", "Microsoft YaHei", sans-serif`

### 字号层级

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

### 颜色体系

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

> 主色 `#005BAC` 可映射为 `--buaa-primary: #005BAC` 覆盖默认蓝。

### 推荐布局类型

**优先使用**：
- ✅ 顶部标题 + 下方段落/列表（占 70%+）
- ✅ 标题 + 居中表格（含表头着色）
- ✅ 标题 + 左侧文字 + 右侧图片
- ✅ 封面/结尾页

**避免过度复杂**：
- ⚠️ 多图片画廊（img-gallery）— 不兼容图注
- ⚠️ 系统框图（block-diagram）— 仅在明确需求时使用
- ⚠️ 双栏密集对比（split-top）— 注意字号需缩小至 19px

---

## 常见错误速查

| 错误写法 | 正确做法 | 原因 |
|----------|----------|------|
| `.text-block` 内用 `<p>` | 裸写文字 | `<p>` 阻断 KaTeX |
| `## 标题` 不完整 | `## 主标题——副标题` | 大纲给了就要用 |
| 多页同编号未细化 | 自动细化 X.Y.Z | 见 SKILL.md 规则#9 |
| 目录 ul 无 inline style | 必须有 `style="position:absolute;..."` | scoped CSS 可能被忽略 |
| `<footer>` 标签 | `<div class="footer-bar">` | Marp 不白名单 footer |
| 幻灯片内 `---` | `<hr>` | `---` 是分隔符 |
| `<img class/style>` | 父 div class + CSS 选择器 | Marp 剥离 img 的 class/style |
| scoped 中 `pre { font-size }` | `section { --pre-font-size: 22px; }` | specificity 不足，见 SKILL.md §九 |
| 修改 `buaa.css` 全局样式 | 在 `.md` 中 `section { --var: val; }` | CSS 变量注入不依赖 specificity |

> 完整 16 条硬约束见 SKILL.md §二
