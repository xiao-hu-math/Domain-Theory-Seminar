# 前八周详细计划 (Domain Theory Seminar)

## 总体目标
本计划覆盖讨论班前八周（周0至周7-8），聚焦于**目标1**的1.1、1.2、1.3部分：弄清楚 Domain Theory 中结构的数学动机，包括 dcpo/cpo、CCC、连续性/代数性。另外熟悉Scott经典论文，理解其公理体系和动机。此外，了解IMP、PCF、$\lambda$ 演算等程序语言的语法及语义要求，为后续目标2和3打基础。

- **方式**：每周下午2:30开始，每小节讨论两次。
  - 第一次：同学汇报，然后大家讨论，梳理不清楚的问题。
  - 第二次：针对遗留问题深入讨论，尽力弄清楚。若仍有不清楚的地方，记录下来，后面再找机会讨论。

## 周次详细安排

### 周0: 03/30 - 课程介绍与目标梳理
- **讨论内容**：课程介绍与目标梳理
- **目标关联**：---
- **主讲人**：陈俣旭
- **参考资料**：---
- **计划**：
  - 介绍讨论班总体目标、方式和时间安排。
  - 讨论前八周的阅读计划。
  - 简单介绍对于域理论的背景知识的理解，以及不清楚的地方，激发同学们的兴趣和好奇心。
  - 介绍IMP语法及其指称语义的基本构造（Andrew Pitts，Denotational Semantics 讲义二至四章）。

### 周1-2: 04/13, 04/20 - Andrew Pitts, *Denotational Semantics* (讲义) 5、6章 （难度一颗星🌟）
- **讨论内容**：Andrew Pitts, *Denotational Semantics* (讲义) 5、6章内容，熟悉PCF及其指称语义 
- **目标关联**：1.1～1.3 
- **主讲人**：待定
- **参考资料**：1）Domain theory and denotational semantics by Tom de Jong
- **阅读内容**：
  - 第5章：PCF 语法 - 类型、项、值、操作语义。
  - 第6章：PCF 指称语义 - 域构造、解释函数、递归定义。
- **目标计划**：
  - 熟悉 PCF 语言：理解语法、类型和操作语义。
  - 掌握指称语义构造：学习如何为 PCF 定义语义域和解释。
- **计划**：
  - 第一次（04/13）：汇报 PCF 语法及其指称语义。
  - 第二次（04/20）：按第一次梳理内容讨论。 

### 周3-4: 04/27, 05/04 - Dana Scott 相关论文： "Outline of a mathematical theory of computation" (1971) + "Continuous Lattices" (1972)  （难度两颗星🌟🌟）
- **讨论内容**：Dana Scott 相关论文： "Outline of a mathematical theory of computation" (1971) + "Continuous Lattices" (1972)
- **目标关联**：1.3 (为什么要求连续性 / 代数性？)
- **主讲人**：待定
- **参考资料**：1）Scott & Strachey (1971)："Towards a mathematical semantics for computer languages"。    2）SEMANTIC DOMAINS AND DENOTATIONAL SEMANTICS, 1989. 
- **阅读内容**：
  - "Outline of a mathematical theory of computation" (1971)。
  - "Continuous Lattices" (1972)：连续格的基础。
- **目标计划**：
  - 理解求解domain方程 $D \cong [D \to D]$ 的动机及思路。为什么需要连续性、笛卡尔闭性？
  - 了解连续格引入的背景，以及序与拓扑如何相关。
- **计划**：
  - 第一次（04/27）：汇报 Scott 的公理和连续格概念，梳理已理解的问题和仍然存在的问题。
  - 第二次（05/04）：根据遗留问题，进一步查阅资料，进行讨论。

### 周5-6: 05/11, 05/18 - Dana Scott 相关论文： "Data Types as Lattices" (1976) + Scott & Strachey (1971)。   （难度三颗星🌟🌟🌟）
- **讨论内容**：Dana Scott 相关论文： "Data Types as Lattices" (1976) + Scott & Strachey (1971)
- **目标关联**：1.3 (为什么要求连续性 / 代数性？)
- **主讲人**：胡晓
- **参考资料**：Scott
- **阅读内容**：
  - "Data Types as Lattices" (1976)：数据类型作为格。

- **目标计划**：
- 了解 $P_\omega$ 模型的构造。构造动机：$D_{\infty}$ 构造太复杂，构建通用域，任意类型可表示为 $P_\omega$ 收缩核。
- 了解收缩核的概念及其在domain理论中的作用。 
- **计划**：
  - 第一次（05/11）：讲解论文，梳理已理解的问题和仍然存在的问题。
  - 第二次（05/18）：根据遗留问题，进一步查阅资料，进行讨论。

### 周7-8: 05/25, 06/01 - Thomas Streicher, "Domain-theoretic foundations of functional programming" (2023) Computability in Domains 章节  （难度两颗星🌟🌟）
- **讨论内容**：Thomas Streicher, "Domain-theoretic foundations of functional programming" (2023) 中的 Computability in Domains 章节 
- **目标关联**：理解domain理论中可计算函数的要求的来龙去脉
- **主讲人**：待定
- **阅读内容**：
  - Computability in Domains 章节 
  - 书中提到的其他重要知识，我们可能遗漏了的。
- **目标计划**：
  - 
- **计划**：
  - 第一次（05/18）：汇报 Computability in Domains 章节内容。
  - 第二次（05/25）：梳理前八周内容，记录遗留问题。

## 总结
前八周计划通过经典论文和书籍，逐步深入理解域理论的基础动机和扩展。每个周次包括具体阅读、目标和讨论计划，确保系统学习。

后续内容围绕目标1.4-1.5展开，涉及幂domain和monad的关系，计划待定。
