# BUAA Marp 高级修饰符参考

> 从 SKILL.md §5 提取。`buaa-am--*` 系列 class 可直接叠加在 `<!-- _class: buaa-chapter -->` 行或 body 容器上，无需额外 CSS。

---

## 字号缩放

| class | 效果 | 适用 |
|:-:|:-:|:-:|
| `buaa-am--tinytext` | 整页缩至 80% | 密集数据页 |
| `buaa-am--smalltext` | 整页缩至 90% | 较多内容页 |
| `buaa-am--largetext` | 整页放大至 115% | 强调展示页 |
| `buaa-am--hugetext` | 整页放大至 130% | 标题页 |

用法：`<!-- _class: buaa-chapter buaa-am--smalltext -->`

## 彩色引用块

叠加在 section 上，blockquote 自动着色：

| class | 颜色 |
|:-:|:-:|
| `buaa-am--bq-blue` | #004F9E 蓝 |
| `buaa-am--bq-red` | #dc3545 红 |
| `buaa-am--bq-green` | #28a745 绿 |
| `buaa-am--bq-purple` | #6f42c1 紫 |
| `buaa-am--bq-black` | #333 黑 |

## 特殊布局

| class | 说明 |
|:-:|:-:|
| `buaa-am--fglass` | 毛玻璃效果列表（白色背景 + 投影 + 非对称圆角），叠加在 body 容器上 |
| `buaa-am--navbar` | 顶部导航进度栏 |
| `buaa-am--footnote` | 脚注布局（CSS Grid 分区：正文 + 脚注） |
| `buaa-am--fixedtitle-a` / `b` | 固定标题栏（标题始终在顶部，内容区可滚动） |
| `buaa-am--trans` | 过渡页增强变体 |
| `buaa-am-card` | 增强卡片样式 |
| `buaa-am-icon-list` | 图标列表 |
| `buaa-am--caption` | 图片/表格题注样式 |

## 多栏列表

| class | 说明 |
|:-:|:-:|
| `buaa-am-cols2-ul--sq` / `--ci` | 两栏无序列表（方形/圆形序号） |
| `buaa-am-cols2-ol--sq` / `--ci` | 两栏有序列表（方形/圆形序号） |
| `buaa-am-col1-ol--sq` / `--ci` | 单栏有序列表（方形/圆形序号） |
| `buaa-am-col1-ul--sq` / `--ci` | 单栏无序列表（方形/圆形序号） |

用法：在 `buaa-chapter__body` 容器内嵌入 `<div class="buaa-am-cols2-ul--sq"><ul>...</ul></div>`

## 箭头尺寸

| class | 效果 |
|:-:|:-:|
| `buaa-arrow--sm` | 箭头缩小至 70% |
| `buaa-arrow--lg` | 箭头放大至 140% |

用法：加在流程图或系统框图的箭头 div 上，如 `<div class="buaa-flow-chart__arrow buaa-arrow--line-long buaa-arrow--lg">`

## 图片尺寸修饰符

同一页中不同图片可能需要不同尺寸时，在 scoped 中定义 `.buaa-hm-fig--a` / `--b` / `--c` / `--d` 修饰符，叠加在 `<div class="buaa-hm-fig">` 上：

```css
.buaa-hm-fig--a img { max-height: 180px !important; max-width: 100% !important; }
.buaa-hm-fig--b img { max-height: 200px !important; max-width: 100% !important; }
```

用法：`<div class="buaa-hm-fig buaa-hm-fig--a"><img src="..."></div>`
