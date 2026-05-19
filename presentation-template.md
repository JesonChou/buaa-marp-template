---
marp: true
theme: buaa
paginate: false
---

<!-- _class: cover -->

<!-- 封面页 -->

<img class="cover-logo" src="./assets/logo.png">

# 北京航空航天大学

## 学术汇报通用模板 · Marp 主题演示

<div class="presenter">汇报人：XXX</div>
<div class="cover-date">20XX年XX月XX日</div>
<div class="cover-decor">BEIHANG UNIVERSITY</div>

---

<!-- _class: catalog -->

<!-- 目录页 -->

<div class="catalog-title">目录</div>
<div class="catalog-line"></div>
<div class="catalog-eng">Contents</div>

<ul>
  <li><span class="toc-num">1</span> 课题背景与研究意义</li>
  <li><span class="toc-num">2</span> 国内外研究现状</li>
  <li><span class="toc-num">3</span> 研究方法与技术路线</li>
  <li><span class="toc-num">4</span> 实验结果与分析</li>
  <li><span class="toc-num">5</span> 总结与展望</li>
</ul>

---

<!-- _class: transition -->

<!-- 过渡页 - 第一章 -->

<div class="trans-num">01</div>

# 课题背景与研究意义

## Background & Significance

---

<!-- _class: chapter -->

<!-- 章节页 - 研究背景 -->

<div class="chapter-badge"><span>1.1</span></div>

## 研究背景——航空航天领域的发展现状与挑战

<div class="chapter-body layout-flow">

航空航天技术是现代科技发展的重要引擎。随着深空探测、高超声速飞行等前沿领域的快速发展，对**飞行器设计**、**材料科学**和**智能控制**提出了更高的要求。

- **深空探测**：火星采样返回、小行星探测任务持续推进
- **绿色航空**：新能源飞机、氢燃料发动机成为研究热点
- **卫星互联网**：低轨星座建设进入快车道
- **智能制造**：数字化设计与仿真技术深度应用

</div>

<div class="footer-bar"></div>
<div class="page-num">1</div>

---

<!-- _class: chapter -->

<!-- 章节页 - 研究意义 -->

<div class="chapter-badge"><span>1.2</span></div>

## 研究意义——本课题的理论价值与应用前景

<div class="chapter-body layout-flow">

#### 理论价值

- 丰富和完善**飞行器结构动力学**理论体系
- 为复杂工况下的**多物理场耦合分析**提供新方法
- 建立面向工程的**不确定性量化**与可靠性评估框架

#### 应用前景

- 支撑我国新一代**高超声速飞行器**研制
- 提升航空航天**结构健康监测**能力
- 推动**数字孪生技术**在航空领域的落地应用

</div>

<div class="footer-bar"></div>
<div class="page-num">2</div>

---

<!-- _class: transition -->

<!-- 过渡页 - 第二章 -->

<div class="trans-num">02</div>

# 国内外研究现状

## Literature Review

---

<!-- _class: chapter -->

<!-- 章节页 - 国内外对比 -->

<div class="chapter-badge"><span>2</span></div>

## 国内外研究对比——主要研究机构与技术路线对比

<div class="chapter-body layout-center">

| 研究方向 | 国内代表机构 | 国际代表机构 | 技术成熟度 |
|:--------:|:-----------:|:-----------:|:--------:|
| 结构优化设计 | BUAA、西工大 | NASA、MIT | ★★★★☆ |
| 智能材料 | 中科院、哈工大 | Boeing、ETH | ★★★☆☆ |
| 数字孪生 | 清华、上交 | GE、Airbus | ★★★☆☆ |
| 不确定性量化 | 南航、大工 | Stanford | ★★★★☆ |
| 多物理场耦合 | 国防科大 | DLR、ONERA | ★★★☆☆ |

> **小结**：国内在结构优化设计领域已达到**国际先进水平**，但在智能材料和数字孪生方面仍有提升空间。

</div>

<div class="footer-bar"></div>
<div class="page-num">3</div>

---

<!-- _class: transition -->

<!-- 过渡页 - 第三章 -->

<div class="trans-num">03</div>

# 研究方法与技术路线

## Methodology & Technical Route

---

<!-- _class: chapter -->

<!-- 章节页 - 技术路线 -->

<div class="chapter-badge"><span>3.1</span></div>

## 总体技术路线

<div class="chapter-body layout-flow">

<div class="columns">

<div>

### 理论建模

- 建立**多尺度**力学模型
- 推导**控制方程**与边界条件
- 发展**高效数值求解**算法
- 验证模型的**收敛性**与精度

### 实验验证

- 设计典型**验证实验**方案
- 搭建**数据采集**系统
- 开展**对比实验**研究
- 标定模型**关键参数**

</div>

<div>

### 仿真分析

- 开发**参数化**仿真平台
- 开展**灵敏度分析**研究
- 实施**不确定性传播**分析
- 完成**多工况**仿真计算

### 工程应用

- 面向**典型结构**应用验证
- 形成**设计准则**与规范
- 开发**辅助设计**工具
- 推广至**型号研制**

</div>

</div>

</div>

<div class="footer-bar"></div>
<div class="page-num">4</div>

---

<!-- _class: chapter -->

<!-- 章节页 - 核心算法 -->

<div class="chapter-badge"><span>3.2</span></div>

## 核心算法实现——有限元求解器关键代码（Python）

<div class="chapter-body layout-flow">

```python
import numpy as np
from scipy.sparse.linalg import spsolve

def solve_fem(K, F, bc_dofs, bc_vals):
    """
    有限元求解器 - 处理位移边界条件
    K: 全局刚度矩阵 (稀疏格式)
    F: 全局载荷向量
    bc_dofs: 约束自由度索引
    bc_vals: 约束自由度值
    """
    n_dof = K.shape[0]
    free_dofs = np.setdiff1d(np.arange(n_dof), bc_dofs)

    # 修改右端项以施加边界条件
    F_modified = F.copy()
    F_modified -= K[:, bc_dofs] @ bc_vals

    # 求解自由自由度
    U = np.zeros(n_dof)
    U[bc_dofs] = bc_vals
    U[free_dofs] = spsolve(K[free_dofs][:, free_dofs],
                            F_modified[free_dofs])
    return U
```

</div>

<div class="footer-bar"></div>
<div class="page-num">5</div>

---

<!-- _class: transition -->

<!-- 过渡页 - 第四章 -->

<div class="trans-num">04</div>

# 实验结果与分析

## Results & Discussion

---

<!-- _class: chapter -->

<!-- 章节页 - 数值仿真结果 -->

<div class="chapter-badge"><span>4</span></div>

## 数值仿真结果——不同方法精度与效率对比

<div class="chapter-body layout-flow">

<div class="card-grid">

<div class="card card-3">

<div class="card-title">传统 FEM</div>

<div class="card-body">

- 网格数：50,000
- 自由度：150,000
- 计算时间：45 min
- 最大误差：3.2%

适用场景：常规结构分析，工程精度要求。

</div>

</div>

<div class="card card-3">

<div class="card-title">本方法</div>

<div class="card-body">

- 网格数：12,000
- 自由度：36,000
- 计算时间：8 min
- 最大误差：1.8%

适用场景：复杂多尺度问题，高精度需求。

</div>

</div>

<div class="card card-3">

<div class="card-title">深度学习</div>

<div class="card-body">

- 无需网格
- 推理时间：&lt; 1s
- 最大误差：5.6%

适用场景：实时预测，初步设计阶段。

</div>

</div>

</div>

<div class="summary-box">
<div class="summary-title">结论</div>
<div class="summary-body">本方法在保证<b>高精度</b>的同时，计算效率相比传统FEM提升了 <b>5.6 倍</b>。</div>
</div>

</div>

<div class="footer-bar"></div>
<div class="page-num">6</div>

---

<!-- _class: transition -->

<!-- 过渡页 - 第五章 -->

<div class="trans-num">05</div>

# 总结与展望

## Conclusion & Outlook

---

<!-- _class: chapter -->

<!-- 章节页 - 主要结论 -->

<div class="chapter-badge"><span>5.1</span></div>

## 主要结论

<div class="chapter-body layout-flow">

#### 理论创新

- 提出了**多尺度自适应**建模框架，突破了传统方法在跨尺度问题上的精度瓶颈
- 建立了**不确定性传播**的高效计算方法，计算成本降低了一个数量级

#### 技术突破

- 开发了**参数化仿真平台**，支持全流程自动化分析与优化
- 实现了**数字孪生**驱动的结构健康监测系统原型

#### 实验验证

- 完成了 **3 类典型结构**的对比验证实验
- 实验结果与仿真预测的吻合度达到 **98%** 以上

</div>

<div class="footer-bar"></div>
<div class="page-num">7</div>

---

<!-- _class: chapter -->

<!-- 章节页 - 主要结论 -->

<div class="chapter-badge"><span>5.1</span></div>

## 主要结论

<div class="chapter-body layout-flow">

#### 未来展望

1. 将方法推广至**多物理场耦合**问题
2. 融合**人工智能**技术实现智能设计优化
3. 推动研究成果在**型号研制**中的工程应用

</div>

<div class="footer-bar"></div>
<div class="page-num">8</div>

---

<!-- _class: chapter -->

<!-- 章节页 - 致谢 -->

<div class="chapter-badge"><span>5.2</span></div>

## 致谢

<div class="chapter-body layout-center">

本研究的开展得到了以下项目和单位的支持：

<br>

|     资助来源     |           项目名称           |     编号      |
| :--------------: | :--------------------------: | :-----------: |
| 国家自然科学基金 | 多尺度结构动力学建模方法研究 |   12345678    |
| 国家重点研发计划 |  高超声速飞行器结构健康监测  | 2024YFBxxxxxx |
|   国防基础科研   |   智能材料与结构一体化设计   | JCKY2024xxxx  |

<br>

衷心感谢 **导师 XXX教授** 的悉心指导！

感谢课题组全体同学的支持与帮助！

感谢各位评审专家的宝贵意见！

</div>

<div class="footer-bar"></div>
<div class="page-num">9</div>

---

<!-- _class: end -->

<!-- 结束页 -->

<div class="chapter-badge"><span>结语</span></div>

# 感谢您的观看与收听，敬请批评指正

## Q & A

<div class="footer-bar"></div>
<div class="page-num">10</div>
