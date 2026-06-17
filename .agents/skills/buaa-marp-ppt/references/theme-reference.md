# BUAA Marp 主题切换参考

> 从 SKILL.md §6 提取。在生成 PPT 的 YAML frontmatter 中修改 `theme` 字段即可切换主题。

| theme | 主色 | 适用场景 |
|---|---|---|
| `buaa` | #004F9E 北航蓝 | 默认，日常汇报/答辩 |
| `buaa-red` | #C41230 北航红 | 庆典/党建/竞赛 |
| `buaa-gold` | #C49B2C 北航金 | 学术典礼/荣誉表彰 |
| `buaa-dark` | #1B2D55 深空蓝 | 科技感/深色场景 |
| `buaa-green` | #2E7D32 银杏绿 | 自然/环保/校园 |
| `buaa-purple` | #5C2D91 星空紫 | 创新/探索/太空 |

## 使用方式

```yaml
---
marp: true
theme: buaa        # 替换为上述任一主题名
paginate: false
---
```
