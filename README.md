# BUAA Marp PPT Template

> 基于 Marp 的北航（Beihang University）主题演示文稿模板系统——轻松取代 PowerPoint 与 LaTeX Beamer！

## 为什么要做这个项目？

在学术场景中，制作演示文稿通常面临两种选择：PowerPoint 操作繁琐、排版难以统一；LaTeX Beamer 学习曲线陡峭、调试成本高。Marp 的出现，让我们可以用 Markdown 写 PPT——但 Marp 内置的原生主题样式数量少、呈现效果一般，且缺乏针对高校学术汇报场景的定制化设计。

于是，我基于北航 VI 视觉识别系统，以我往常所做的PPT模板作为参考，打造了这套 **BUAA Marp PPT Template**。它提供 6 套主题色系、12 种排版布局、系统框图/流程图等学术专用组件，以及 **AI Agent 一键生成** 能力——你只需要提供一份**大纲**，AI 就能自动生成排版精美、风格统一的完整 PPT。对 AI 生成的排版不满意，可以根据本文档中所说明的样例，让 AI Agent 进行调整或者自己手动调整。

## 快速预览

- **6 套主题色系**：北航蓝（默认）、北航红、北航金、深空蓝、银杏绿、星空紫——覆盖日常答辩、重要庆典、学术典礼、科技汇报等场景
- **12 种排版布局**：从文左图右、纯文字列表、双栏对比，到流程图、系统框图、窄表格分栏——智能布局决策树自动匹配最佳方案
- **AI Agent 原生集成**：只需提供一份 `.md` 大纲文件，AI 自动分析内容类型、字数、图片，选择最佳布局并生成完整 PPT
- **CSS 变量体系**：通过 `section { --var: val; }` 按页微调字号、行距、颜色，全局样式零侵入
- **学术专用组件**：KaTeX 公式支持、代码块可调参数、流程图 `buaa-arrow--line-long` 箭头、系统框图 Hub-Spoke 拓扑

## 你需要了解的工具

就这几样：

- **[Visual Studio Code](https://code.visualstudio.com/)** 或任何支持 Marp 的编辑器。也可以使用 Codex、Cursor 或者 Trae 等原生支持 AI Agent 的编辑器
- **[Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode)**（插件）
- **[Marp CLI](https://github.com/marp-team/marp-cli)**（可选，用于命令行导出 PDF/HTML/PPTX）
- 任何一种大语言模型的 API Key。本项目在设计与制作过程中所使用的大语言模型是 deepseek-v4-pro，你可以在 AI Agent 中使用你较为顺手的大语言模型，并将其接入到你的 AI Agent 中

Markdown 是一种极轻量的文本标记语言，支持表格、代码、图片、公式等。Marp 将 Markdown 转换为演示文稿，而本项目提供了完整的北航主题 CSS 层和 AI 生成规范。

---

## 项目特色

### 六套北航 VI 主题色系

所有主题通过 `@import-theme 'buaa'` 继承基础主题，每个变体只需约 15 行 CSS 重写颜色变量：

| 主题名 | 主色 | 深色 | 适用场景 |
|--------|:----:|:----:|------|
| `buaa` | `#004F9E` | `#003D7A` | 北航蓝（默认），日常汇报/课题答辩 |
| `buaa-red` | `#C41230` | `#9A0E24` | 北航红，重要庆典/党建/竞赛 |
| `buaa-gold` | `#C49B2C` | `#9A7A22` | 北航金，学术典礼/荣誉表彰 |
| `buaa-dark` | `#1B2D55` | `#111D38` | 深空蓝，科技感/深色场景 |
| `buaa-green` | `#2E7D32` | `#1E5A22` | 银杏绿，自然/环保/校园主题 |
| `buaa-purple` | `#5C2D91` | `#3F1E64` | 星空紫，创新/探索/太空主题 |

切换主题只需改一行 YAML：`theme: buaa-red`。

```css
/* themes/buaa-red.css — 仅 15 行覆盖颜色变量 */
@import-theme 'buaa';
:root {
  --buaa-primary: #C41230;
  --buaa-primary-rgb: 196, 18, 48;
  /* ... */
}
```

### 十二种排版布局

内置布局决策树，按内容类型自动匹配最佳方案：

| 布局 | 类名 | 典型场景 |
|:----:|------|----------|
| **A** | `buaa-split--2` | 文左图右（图文默认） |
| **B** | `buaa-layout--flow` + ol/ul | 嵌套列表 + callout 总结 |
| **C** | `buaa-layout--center` | 居中混排（段落+表格+公式） |
| **C-split** | `buaa-split--2 buaa-split--top` | 窄表格分栏（防溢出出现表格滚动条） |
| **D** | `buaa-split--2 buaa-split--top` | 双栏对比 + callout |
| **E** | `buaa-layout--center` | 标题+列表+表格+图注 |
| **F** | `buaa-split-tb` | 文上图下（技术大图专用） |
| **G** | `buaa-flow-chart` | 纵向流程图（3~9步），line-long 箭头 |
| **H** | `buaa-block-diagram` | 系统框图（Hub-Spoke 拓扑） |
| **I** | `buaa-img-pair` | 双图并排+独立图注 |
| **J** | `buaa-layout--flow` + ul | strong 标题 + 子列表混合 |
| **K** | `buaa-hm-fig` | 纯大图全屏展示 |

### 纵向流程图

支持 3~9 步纵向流程，`buaa-arrow--line-long` 箭头类型，`--arr-length` / `--line-width` / `--arr-color` 三个 CSS 变量控制样式：

```html
<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--line-long-down"></div>
```

### 系统框图

Hub-Spoke 拓扑结构，支持上/下/左/右四个方向的节点链。Hub 只在 `buaa-block-diagram__center` 渲染一次，链中不重复。

### CSS 变量体系

解决了 Marp `<style scoped>` 中直接写选择器因 specificity 不足而无效的痛点。通过 `section { --var: val; }` 注入 CSS 变量穿透全局样式：

| 变量 | 用途 | 默认值 |
|------|------|:---:|
| `--text-p-size` | 段落字号 | 28px |
| `--text-p-line-height` | 段落行高 | 1.8 |
| `--text-size` | 列表字号 | 24px |
| `--text-line-height` | 列表行高 | 1.8 |
| `--text-item-gap` | 列表条目间距 | 8px |
| `--pre-font-size` | 代码块字号 | 18px |
| `--pre-font-family` | 代码块字体 | Consolas, monospace |
| `--pre-color` | 代码块文字颜色 | #333 |
| `--pre-line-height` | 代码块行高 | 1.6 |
| `--code-font-size` | 行内代码字号 | 0.9em |
| `--code-color` | 行内代码颜色 | var(--buaa-primary) |

### AI Agent 一键生成

项目集成了 Agent Skills 规范中的 SKILL.md 文件，支持 Trae SOLO Agent 、Cursor、Claude Code 、Github Copilot 等 AI 编码助手的渐进式加载：

1. **发现阶段**（~100 tokens）：加载 skill 名称和描述
2. **激活阶段**（~1100 tokens）：加载 16 条硬约束、布局决策树、页面骨架模板
3. **执行阶段**（按需加载）：选中布局后加载对应 HTML/CSS 模板

你只需要准备一份大纲 `.md` 文件，AI 就会自动：
- 分析每页的内容类型、字数、有无图片
- 按决策树选择最佳布局（A-K / C-split）
- 生成符合 16 条硬约束的完整 PPT
- 自动细化编号层级（X / X.Y / X.Y.Z）

如果对 AI Agent 的排版方案不满意，可以告诉 Agent 具体哪一页要调整成什么样的布局，或者根据自己的排版偏好，直接在大纲中说明。或者让 Agent 给你提供手动微调的代码，进行符合自己审美的微调。

---

## 项目结构

```
buaa-marp-template/
├── themes/                              # 6 套主题 CSS
│   ├── buaa.css                          # 北航蓝基础主题（~2000 行）
│   ├── buaa-red.css                      # 北航红（~15 行，继承 buaa.css）
│   ├── buaa-gold.css                     # 北航金
│   ├── buaa-dark.css                     # 深空蓝
│   ├── buaa-green.css                    # 银杏绿
│   └── buaa-purple.css                   # 星空紫
├── assets/                               # 静态资源
│   ├── logo.png                          # 北航校徽
│   ├── cover-bg.png                      # 封面背景图
│   └── catalog-bg.png                    # 目录背景图
├── .agents/skills/buaa-marp-ppt/         # AI Agent Skill
│   ├── SKILL.md                          # 核心生成规范（269 行）
│   └── references/
│       └── layout-templates.md           # 12 个完整布局模板
├── .github/
│   └── copilot-instructions.md           # 项目级配置与快速参考
├── .vscode/
│   └── settings.json                     # Marp 主题注册
├── BUAA_Marp_Template.md                 # 完整模板演示文件（44 页）
└── BUAA_Marp_Template-outline.md         # 大纲示例文件
```

---

## 快速开始

### 1. 环境准备

在 VS Code 中安装 [Marp for VS Code](https://marketplace.visualstudio.com/items?itemName=marp-team.marp-vscode) 插件，或者使用 Trae CN 进行插件的安装。如果你有 VS Code 的基础，换用 Trae CN 时，编译器会提供从 VS Code 导入预设的选项，点击即可。

### 2. 打开项目

用 VS Code 打开 `buaa-marp-template/` 文件夹。确保 `.vscode/settings.json` 已注册所有 6 套主题。

### 3. 预览模板

打开 `BUAA_Marp_Template.md`，点击右上角 Marp 预览按钮即可查看所有布局效果。

### 4. 创建你的 PPT

创建一个新的 `.md` 文件，YAML 头指定主题：

```yaml
---
marp: true
theme: buaa          # 可选: buaa / buaa-red / buaa-gold / buaa-dark / buaa-green / buaa-purple
paginate: false
---
```

然后按照 [SKILL.md](.agents/skills/buaa-marp-ppt/SKILL.md) 中的页面结构编写内容，或直接提供大纲让 AI 生成。大纲的撰写可参考 [BUAA_Marp_Template-outline.md](BUAA_Marp_Template-outline.md)。

AI 生成的文件以你大纲的主题命名。根据上述大纲模板生成的 Marp 格式的 PPT 参见 [BUAA_Marp_Template.md](BUAA_Marp_Template.md)。建议 Marp 格式的 `.md` 文件在编译器中预览，在 Typora 等 markdown 编辑器中预览容易出现乱码或者错排。

### 5. 导出

- **VS Code 插件**：点击 Marp 图标 → Export Slide Deck → 选择 PDF / HTML / PPTX
- **Marp CLI**：`marp your-slides.md --pdf --theme themes/buaa.css`

---

## AI 生成规范

项目为 AI Agent 定义了 **16 条硬约束**，分为三个级别：

| 级别 | 数量 | 说明 |
|:----:|:----:|------|
| 🔴 致命级 | 7 条 | 违反即渲染崩溃 |
| 🟡 严重级 | 6 条 | 影响排版正确性 |
| 🟢 注意级 | 3 条 | 影响呈现质量 |

核心规范包括：`<style scoped>` 必须在 badge 之前、文本块内禁止 `<p>` 标签、公式只能在裸文本段落、目录 `ul` 必须带 inline style、scoped 样式必须用 `section { --var: val; }` 注入 CSS 变量等。

完整规范见 [SKILL.md](.agents/skills/buaa-marp-ppt/SKILL.md)。

---

## 页面结构

```
封面 → 目录 → 过渡页 → 正文×N → 过渡页 → ... → 结尾
```

- **封面**：北航校徽 + 汇报标题 + 副标题 + 汇报人 + 日期
- **目录**：右侧纵向列表，带章节编号
- **过渡页**：章节号 + 中英文标题
- **正文**：badge 编号 + 标题栏 + 内容区 + 页脚
- **结尾**：致谢语 + Q&A

---

## 设计规范

### 字体体系

`"HarmonyOS Sans SC Medium", "Noto Sans SC", "Microsoft YaHei", sans-serif`

- 标题/正文主力：HarmonyOS Sans SC Medium
- 辅助正文：Noto Sans SC
- 兼容回退：微软雅黑

### 颜色参考

| 色值 | 角色 | 用途 |
|------|:--:|------|
| `#005BAC` | 主色 | 标题、强调、表头 |
| `#505050` | 正文灰 | 段落文字 |
| `#FF0000` | 强调红 | 关键词强调 |
| `#333333` | 深灰 | 正文深色 |
| `#0078D7` / `#009688` / `#D97706` | 辅助色 | 图表/流程图点缀 |

---

## 参考与致谢

本项目在设计和实现过程中参考了以下优秀项目：

> - **Awesome-Marp** — 一套功能丰富的 Marp 自定义主题集合，提供了多套主题色系和 38 种自定义样式，启发了本项目的多主题架构和布局分栏设计。  
>   
>   🔗 [https://github.com/favourhong/Awesome-Marp](https://github.com/favourhong/Awesome-Marp)
>   
> - **claude-code-templates / marp-slide** — 一个面向 AI Agent 的 Marp 幻灯片生成 Skill 模板，提供了 7 套预制主题和渐进式加载的 SKILL.md 设计范式，启发了本项目的 AI Agent 集成方案。 
>   
>   🔗 [https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/creative-design/marp-slide](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/creative-design/marp-slide)

---

## 更新记录

- `2026年5月24日` BUAA Marp PPT Template v1.0

    - **首个正式版本发布**，README 文档上线
    - 引入排版设计参考规范：字体体系（HarmonyOS Sans SC Medium）、颜色参考（#005BAC 主色）、推荐布局类型
    - 以 blockquote 引用格式致谢 [Awesome-Marp](https://github.com/favourhong/Awesome-Marp) 与 [claude-code-templates/marp-slide](https://github.com/davila7/claude-code-templates/tree/main/cli-tool/components/skills/creative-design/marp-slide) 两个参考仓库

## 更新计划

- 添加 README 的图片说明
- 完善大纲模板的撰写规范
- 完善大纲的说明内容，添加上图片的排版类型和说明
- 完善 AI Agent 的决策，使其获得大纲后的排版决策更精准
- 修复代码块中的文字不能手动调整的问题

---

## License

MIT
