# 🚀 Domain Theory 的指称语义背景学习路线图


## 讨论班方式

总体目标：熟悉 Domain 理论的背景, 可以给外行讲解来龙去脉, 为未来的深入研究指明可能的方向.

方式：围绕一些内容 (比如书籍中某些章节, 或者文献) 展开阅读, 定期汇报交流, 一起学习.

时间：每周一下午2:30开始，每小节讨论两次
 - 第一次同学汇报，然后大家讨论，梳理清楚还没弄清楚的问题。
 - 第二次针对遗留问题进行深入讨论，尽力弄清楚。若仍有不清楚的地方，记录下来，后面再找机会讨论。

 
以下是整体目标，本学期主要弄清楚目标1及目标2中部分内容。预计12次讨论，讨论6个小节。


## 目标 1：弄清楚 Domain Theory 中结构的数学动机

本阶段旨在理解：为了给计算提供严谨的数学分身，为何选取了序拓扑结构，我们为何要在拓扑和序结构上层层加码？

### 1.1 为什么要求 dcpo / cpo？
* **核心动机：**
    * **描述循环 (Iteration)：** 循环语句（如 `while`）的语义定义为泛函的最小不动点。根据 **Kleene 不动点定理**，这要求定向集（或链）的最小上界（LUB）必须存在。
    * **在 $\lambda$ 演算中：** 处理**递归定义**。即便没有显式循环，自引用的函数定义也需要 dcpo 来保证收敛，使 $Y$ 组合子在数学上合法。

> 1）最小元是必须的吗？为什么现在domain理论各种数学结构研究几乎不要求最小元了？ 
2）有界完备、L-dcpo等性质是否有对应的计算动机？（比如处理部分定义的程序，或者处理某些特定的计算效应）

### 1.2 为什么要求范畴是笛卡尔闭的 (Cartesian Closed, CCC)？
* **核心动机：支持高阶函数 (Higher-order Functions)**。
    * 在函数式编程（如 $\lambda$ 演算）中，函数是一等公民。数学上，这要求范畴内必须存在**指数对象 (Exponential Objects)** $[D \to E]$。
    * **柯里化 (Currying)：** CCC 保证了二元函数 $f: X \times D \to E$ 与高阶函数 $\hat{f}: X \to [D \to E]$ 之间的自然同构。
* **在 Domain 中的意义：** 并不是所有 Domain 的子范畴都是 CCC 的。寻找既能处理计算效应（如连续性、概率）又是 CCC 的范畴（如 **Scott Domains** 或 **FS-domains**）是核心任务。

> 1) 对于无类型 $\lambda$ 演算，Scott求解的 $D \cong [D \to D]$。程序语义是D或 $[D \to D]$ 中的一个元素,那么其实只需要一个偏序集就可以，和范畴论无关了？为什么还要CCC？这个要求是有类型 $\lambda$ 演算的语义模型才有的要求吗？
2) 任何范畴都可以通过一些构造（如局部完备化）得到一个新的CCC范畴，那么为什么我们还要在原始的Domain范畴上要求CCC？


### 1.3 为什么要求连续性 (Continuity) / 代数性 (Algebraicity)？
* **说法 1：有限逼近无限。** 这是 **Way-below 关系 ($\ll$)** 的本质。它保证了无限对象（如实数、无限流）可以由其**基 (Basis)** 中的有限信息（紧致元素）唯一确定。
* **说法 2：Domain 方程 $[D \to D]$ 有解。** 构造无类型 $\lambda$ 演算的 $D_\infty$ 模型时，普通的 dcpo 无法保证 $apply$ 运算的拓扑稳定性。连续性（特别是 **Scott Domains**）保证了 $D$ 是局部紧的，从而使函数求值运算连续。
* **说法 3：概率幂需要连续性。** 在非连续 dcpo 上，定义在 Scott 拓扑上的**估值 (Valuation)** 无法唯一扩展为 **Borel 测度**。这是构建带概率程序语言（PPCF）语义的门槛。




```markdown
Scott 的五条公理 (Dana Scott, "Outline of a mathematical theory of computation")
Scott 给出了五条公理来定义数据类型：
1) A data type is partially ordered set.
2) Mappings between data types are monotonic.
3) A data type is a complete lattice under its partial ordering.
4) Mappings between data types are continuous.
5) A data type has an effectively given basis.
更详细的论述参考 Scott & Strachey (1971), "Towards a mathematical semantics for computer languages".

Plotkin 的四个要求 (1983, "Pisa notes")
1) All domains are partial orders with a least element.
2) All computable functions are monotonic.
3) Every domain is a cpo.
4) Every computable function is continuous.
为了给出递归定义语句的语义。比如在 PCF 中，一个加法句子的指称语义，他也解释了为什么要添加最小元（解释不终止的语句的语义），函数空间用来解释 PCF 中的 function type。作为应用，他只需要考虑可数链完备的偏序集。
另一个更详细的参考书：Thomas Streicher, "Domain-theoretic foundations of functional programming" (2023)。

Questions:
1) 这些要求的适用范围是什么？对于 IMP 这样的简单命令式语言，dcpo/cpo 就足够了；对于 PCF 这样的有型 $\lambda$ 演算，需要连续性来处理递归定义；对于无型 $\lambda$ 演算，需要更强的连续性（如 Scott Domains）来解决 $D \cong [D \to D]$ 的问题；对于带概率的语言（PPCF），需要连续域来处理估值和测度的关系？
```


### 1.4 为什么幂 Domain (Powerdomain) 是一个 Monad？
* **核心动机：** **计算效应 (Computational Effects)** 的代数化。非确定性（Nondeterminism）被视为一种效应。Monad 的 `unit` 将确定性值嵌入效应空间，`bind` 处理这些效应的复合。

### 1.5 自由代数 (Free Algebra) 与 Monad 的关系
* **核心动机：** 各种幂域（Smyth, Hoare, Plotkin）实际上是某种代数理论（如半格理论）在 Domain 范畴内的**自由构造**。研究这种伴随关系能揭示序关系的物理意义。


> 它们的逻辑链路是：非确定性计算 $\rightarrow$ 幂域构造 $\rightarrow$ 对应的 Monad $\rightarrow$ 该 Monad 的 Eilenberg-Moore 代数（即自由代数）。Monad 是抽象工具：Moggi 指出，任何一种“计算效应”（如非确定性、概率、状态）都可以用 Monad 来建模。幂域是具体实现：对于非确定性，对应的 Monad 就是“幂域 Monad”。自由代数是代数本质：幂域中的元素不仅是集合，它们还满足某些代数定律（如结合律、交换律、幂等律）。自由代数解释了如何从一个基础域出发，通过这些定律“生成”出幂域。

---

## 目标 2：弄清楚各类程序语义的数学要求与限制

| 程序语言 | 核心数学结构要求 | 限制与挑战 |
| :--- | :--- | :--- |
| **1. IMP** (简单命令式) | **Flat Domains** ($S \to S_\bot$) | 结构简单，无法处理高阶函数。 |
| **2. PCF** (有型 $\lambda$ 演算) | **CPO + Scott 连续函数** | 存在“全抽象 (Full Abstraction)”不匹配问题。 |
| **3. $\lambda$ 演算** (无型) | **连续格 (Continuous Lattices)** | 必须满足 $D \cong [D \to D]$，绕过康托尔势论困境。 |
| **4. PPCF** (带概率的 PCF) | **连续域 (Continuous Domains)** | 涉及 Valuations 到 Borel 测度的唯一扩展。 |

---

## 目标 3：Full Abstraction 与相关语义模型

本阶段旨在理解：为何域模型在某些程序语言（如 PCF）中无法达到“全抽象 (Full Abstraction)”，以及如何通过稳定域 (Stable Domains) 和博弈语义 (Game Semantics) 来解决这些问题。

### 3.1 什么是 Full Abstraction？
* **定义：** 在程序语义中，全抽象要求语义模型中的等价关系与操作语义（基于程序行为）完全匹配。即，如果两个程序在所有上下文中的行为相同，则它们在语义模型中等价，反之亦然。
* **问题：** 在 PCF（有型 $\lambda$ 演算）中，基于域的指称语义通常不满足全抽象。域模型可能有“太多”的等价，导致语义上等价但操作上不同的程序被误认为等价。
* **例子：** 某些 PCF 程序在域模型中不可区分，但在操作语义中可以通过上下文分离。

### 3.2 Stable Domains：解决全抽象的尝试
* **动机：** 标准域模型（如 Scott Domains）缺乏稳定性，导致全抽象失败。
* **定义：** Stable Domains 是一种增强的域结构，添加了“稳定性”条件，确保函数空间中的函数对某些序关系是稳定的。
* **意义：** 通过稳定性，可以更精确地捕捉程序的计算行为，减少不必要的等价，从而接近全抽象。
* **挑战：** 构建稳定的域模型需要额外的数学结构，可能牺牲一些范畴性质（如 CCC）。

### 3.3 Game Semantics：一种全抽象的语义框架
* **动机：** 当域模型失败时，博弈语义提供了一种基于交互的替代方法。
* **核心思想：** 将程序视为博弈中的玩家，程序执行通过博弈规则建模。语义等价基于博弈策略的等价。
* **优势：** Game Semantics 自然地达到全抽象，因为它直接模拟程序的交互行为。
* **例子：** 在 PCF 中，Abramsky 和 McCusker 的博弈语义模型证明了全抽象。
* **与域论的关系：** 博弈语义可以与域论结合，但它提供了更细粒度的语义描述。

---

## 📚 阅读资料清单

### 第一部分：经典与基础
1. **Andrew Pitts, *Denotational Semantics* (讲义)**
   * **重点：** 2.1 (Posets), 2.3 (CPO), 2.4 (Tarski 不动点定理)。
   * **对应目标：** 1.1 和 2.1。
2. **Dana Scott (1976), *"Data Types as Lattices"* 或 (1972) *"Continuous Lattices"***
   * **重点：** 逆极限构造 $D_\infty$ 以及 $D \cong [D \to D]$ 的同构证明。
   * **对应目标：** 1.3 (说法 2) 和 2.3。
3. **Abramsky & Jung, *"Domain Theory"* (Handbook chapter)**
   * **重点：** 域理论的全面综述：Scott 拓扑、代数域、连续域、范畴观点与具体例子。
   * **对应目标：** 贯穿多目标，作为索引式参考。

### 第二部分：代数与 Monad
3. **Eugenio Moggi (1991), *"Notions of computation and monads"***
   * **重点：** 理解计算效应与范畴论中 Monad 的对应关系。
   * **对应目标：** 1.4 和 1.5。
4. **Giry, *"A Categorical Approach to Probability Theory"* (1982)**
   * **重点：** Giry 单子与概率测度的范畴论处理，构造与基本性质。
   * **对应目标：** 2.4，提供概率语义的范畴模板。

### 第三部分：现代概率语义 (前沿论文与著作)
5. **J. Goubault-Larrecq (2023), *"A Domain-theoretic Approach to Statistical Programming Languages"***
   * **重点：** 极小估值 (Minimal Valuations) 理论，探讨在弱连续性条件下的测度扩展。
   * **对应目标：** 2.4 的数学边界。
6. **Di Gianantonio (2024), *"A Cartesian Closed Category for Random Variables"***
   * **重点：** 偏序集上的随机变量路径。提供了一种不同于传统测度论的视角，利用随机变量构造满足 CCC 的概率语义模型。
   * **对应目标：** 2.4 (PPCF 的现代指称语义实现)。
7. **Jones & Plotkin 等（概率幂域系列工作）**
   * **重点：** 概率幂域或概率效果的构造、性质与限制；PPCF 语义建模的具体技术。
   * **对应目标：** 2.4，直接关联估值/测度在域上的处理。
8. **Edalat / Tix / Keimel（域论与测度/积分相关工作，survey 级别）**
   * **重点：** 域论下的积分与测度构造、估值的代数/拓扑性质研究。
   * **对应目标：** 2.4，补充概率与测度论在域论框架下的细节（积分、期望等）。

### 第四部分：全抽象与语义模型 (前沿与经典)
9. **Abramsky, S. (1997), *"Game Semantics"***
   * **重点：** 博弈语义的基础框架及其在程序语言语义中的应用，特别是全抽象的证明。
   * **对应目标：** 3.3。
10. **Abramsky & McCusker (1997), *"Full Abstraction for PCF"***
    * **重点：** 使用博弈语义证明 PCF 的全抽象，展示域模型的局限性。
    * **对应目标：** 3.1 和 3.3。
11. **Berry, G. (1978), *"Stable Models of Typed λ-Calculi"***
    * **重点：** 稳定域的引入及其在解决全抽象问题中的作用。
    * **对应目标：** 3.2。
12. **Hyland-Ong 等（全抽象与博弈语义系列工作）**
    * **重点：** 博弈语义如何实现 PCF 的全抽象，以及与域论模型的比较。
    * **对应目标：** 3.1 和 3.3，提供替代视角理解域模型全抽象失败的根源。

---

## 背景知识
- **基础数学：** 集合论、序理论、拓扑学、范畴论。
- **程序语言理论：** $\lambda$ 演算、类型系统、操作语义。
- **概率论：** 测度论、随机变量。

## 参考资料汇总
### 参考书籍
- Andrew Pitts. Denotational Semantics. 讲义.
- Dana Scott. Continuous Lattices. 1972.
- Dana Scott. Data Types as Lattices. 1976.
- Dana Scott & Christopher Strachey. Towards a mathematical semantics for computer languages. 1971.
- Abramsky & Jung. Domain Theory. Handbook chapter.
- Glynn Winskel. The Formal Semantics of Programming Languages: An Introduction. 1993.
- Carl Gunter, Peter Mosses, Dana Scott. Semantic Domains and Denotational Semantics. 1989.
- Stoy J.E. Denotational semantics: The Scott-Strachey approach to programming language theory. 1977.
- Roberto M. Amadio, Pierre-Louis Curien. Domains and Lambda Calculi.
- Thomas Streicher. Domain-theoretic foundations of functional programming. 2023.

### 参考论文
- Dana Scott. "Outline of a mathematical theory of computation". 1971.
- Gordon Plotkin. "Pisa notes". 1983.
- Michèle Giry. "A Categorical Approach to Probability Theory". 1982.
- Eugenio Moggi. "Notions of computation and monads". 1991.
- Jean Goubault-Larrecq. "A Domain-theoretic Approach to Statistical Programming Languages". 2023.
- Claudio Di Gianantonio. "A Cartesian Closed Category for Random Variables". 2024.
- Abramsky, S. "Game Semantics". 1997.
- Abramsky & McCusker. "Full Abstraction for PCF". 1997.
- Berry, G. "Stable Models of Typed λ-Calculi". 1978.
- Hyland-Ong 等. "全抽象与博弈语义系列工作". 1990s-2000s.
- Jones & Plotkin 等. "概率幂域系列工作". 1990s-2000s.
- Edalat / Tix / Keimel. "域论与测度/积分相关工作". 1990s-2010s.

## 本学期安排
| 周次 | 日期 | 讨论内容 | 目标关联 | 主讲人 | 参考资料 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | 03/30 | 课程介绍与目标梳理 | --- | 陈俣旭 | --- |
| 1-2 | 04/13, 04/20 | Andrew Pitts, *Denotational Semantics* (讲义) 2.1, 2.3, 2.4 | 1.1 | 待定 | Pitts |
| 3-4 | 04/27, 05/04 | Dana Scott 相关论文： "Outline of a mathematical theory of computation" (1971) + "Continuous Lattices" (1972) | 1.3 | 待定 | Scott |
| 5-6 | 05/11, 05/18 | Dana Scott 相关论文： "Data Types as Lattices" (1976) + Scott & Strachey (1971) | 1.3 | 胡晓 | Scott |
| 7-8 | 05/25, 06/01 | Thomas Streicher, "Domain-theoretic foundations of functional programming" (2023) - 弄清楚来龙去脉 | 1.3 | 待定 | Streicher |
| 9-10 | 06/08, 06/15 | Eugenio Moggi (1991), *"Notions of computation and monads"* -  Monad介绍 | 1.4 | 待定 | Moggi |
| 11-12 | 06/22, 06/29 | Eugenio Moggi (1991), *"Powerdomains"* - 幂domain、自由代数与 Monad 关系 | 1.5 | 待定 | Moggi |
