---
comments: true
---

# 第二章 - 基本结构：集合、函数、序列、求和与矩阵

## 集合

**集合** (set) 是最基本的离散结构。有关集合的基本数学性质我们在数学学习中已经非常熟悉了，我们在这里讨论一些有关集合的不一样的内容。

在我们先前的学习中，集合被定义为若干**元素** (element) 的聚集，这是由康托尔最早提出的，这种定义方法被称作**朴素集合论** (naive set theory)。但是朴素集合论是基于对于对象的直觉概念，这种直觉概念的使用会导致**悖论** (paradox) 或逻辑不一致性的出现。于是最后就出现了为人所熟知的**罗素悖论** (Russell's paradox)。

罗素悖论的出现一方面否定了朴素集合论的完备性，另一方面推动了构造集合论的出现和发展。但是我们需要指出的是，朴素集合论已经足够完成本课程的学习，而对于构造集合论的研究太过艰深，此处就不展开叙述，留与感兴趣的读者自行探索。

基于本课程的受众，接下来我们介绍几个对读者可能较为陌生的，有关集合的数学概念。

### 幂集

对于集合 $S$，$S$ 的**幂集** (power set) 是集合 $S$ 所有子集的集合，记作 $\mathcal{P}(S)$。

> 举例来说，集合 $\{0, 1, 2\}$ 的幂集是 $\{\varnothing, \{0\}, \{1\}, \{2\}, \{0, 1\}, \{0, 2\}, \{1, 2\}, \{0, 1, 2\}\}$

### 笛卡尔积

集合 $A_{1}, A_{2}, \cdots, A_{n}$ 的**笛卡尔积** (Cartesian product) 记作 $A_{1} \times A_{2} \times \cdots \times A_{n}$，指所有有序 $n$ 元组 $(a_{1}, a_{2}, \cdots, a_{n})$ 的集合，其中 $a_{i} \in A_{i}, i = 1, 2, cdots, n$。

我们将 $A \times A$ 简记为 $A^{2}$，这种记法可以推广到任意多个集合。

### 带量词的集合符号

我们通过特定的符号来显式地限定一个量化命题的论域。

$\forall x \in S(P(x))$ 表示 $P(x)$ 在集合 $S$ 所有元素上的全称量化，即为 $\forall x (x \in S \to P(x))$ 的简写；$\exist x \in S(P(x))$ 表示 $P(x)$ 在集合 $S$ 所有元素上的存在量化，即为 $\exist x (x \in S \to P(x))$ 的简写。

## 集合运算

鉴于数学学习的一般情况，读者对集合的有关基本运算应当是熟悉的。这里我们还是讨论一些更深层次的内容。

### 集合恒等式

容易发现，集合和逻辑是有对应关系的。那么基于[逻辑等价式](https://victorwang712.github.io/Note/mathematics/discrete_mathematics/chapter_1/#_10)，我们就可以给出对应的集合恒等式。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_2_1.png" width="70%" style="margin: 0 auto;">
</div>

### 多重集

在某些情况下，我们需要考察元素在集合中出现的次数，因此我们要引入**多重集** (multiset)，即集合内元素可以出现多于一次的集合。一般地，我们将多重集记作 $\{m_{1} \cdot a_{1}, m_{2} \cdot a_{2}, \cdots, m_{r} \cdot a_{r} \}$，其中 $m_{i}$ 称作元素 $a_{i}$ 的**重复数** (multiplicity)。

有必要对多重集间的运算进一步说明：

- 两个多重集的并是一个多重集，其中每个元素的重复数是其在两个多重集中重复数的最大值
- 两个多重集的交是一个多重集，其中每个元素的重复数是其在两个多重集中重复数的最小值
- 两个多重集的和是一个多重集，其中每个元素的重复数是其在两个多重集中重复数的和
- 两个多重集的查是一个多重集，其中每个元素的重复数是其在两个多重集中重复数的差

## 函数

**函数** (function)，也称作 **映射** (mapping) 或**变换** (transformation)，是数学中的基本概念之一。同样我们认为有关函数的基本数学性质读者应当在数学学习中已经非常熟悉了，我们在这里讨论一些有关函数的不一样的内容。

### 部分函数

若函数 $f$ 的**域** (domian) 是 $A$、**陪域** (codomain) 是 $B$，但其 **定义域** (domain of definition) 是 $A$ 的真子集，则称 $f$ 是从 $A$ 到 $B$ 的**部分函数** (partial function)。此时称 $f$ 对于 $A$ 中不在 $f$ 的定义域中的元素**无定义** (undefined)。对应地，当 $f$ 的定义域等于 $A$ 时，称 $f$ 是从 $A$ 到 $B$ 的**全函数** (total function)。

## 序列

**序列** (sequence)，即数列，同样是数学中的基本概念之一。

## 基数

在很多情况下，我们需要考察一个集合的「大小」，所以我们引入了**基数** (cardinality) 这个概念。但由于无限集的存在，基数的定义并不如直观上那么简单，为此我们要给出对应的一套数学规则。

集合 $A$ 和集合 $B$ 有相同的基数，当且仅当存在 $A$ 和 $B$ 间的一个双射，记作 $|A| = |B|$。

若存在从 $A$ 到 $B$ 的单射，则 $A$ 的基数小于等于 $B$ 的基数，记作 $|A| \leq |B|$。

### 可数集合

若一个集合是有限集或与自然数集基数相同，则称该集合是**可数的** (countable)，反之则称该集合是**不可数的** (uncountable)。

若一个无限集 $S$ 是可数的，则将其基数记作 $|S| = \aleph_{0}$。

因此，只需要找到一个无限集和自然数集间能建立双射，就能证明该集合是可数集。容易证明，整数集、有理数集都是可数集。

### 不可数集合

一个最具代表性的不可数集合是实数集，关于其不可数的证明是相当经典且重要的，我们这里要予以介绍。该方法称作**康托尔对角论证法** (Cantor's diagonal argument)，具体证明如下：

!!! abstract "Proof"

    假设实数集合是可数的，那么在 $0$ 和 $1$ 之间的实数集合也是可数的，即 $0$ 和 $1$ 之间的实数可以按照某种顺序列出。设这些实数的十进制表示为：

    $$r_{1} = 0.d_{11}d_{12}d_{13} \cdots, r_{2} = 0.d_{21}d_{22}d_{23} \cdots, r_{3} = 0.d_{31}d_{32}d_{33} \cdots, \cdots$$

    其中 $d_{ij} \in \{0, 1, 2, 3, 4, 5, 6, 7, 8, 9\}$。根据假设，这种表示已经包含了 $0$ 和 $1$ 之间所有的实数。

    但是，我们可以构造这样一个数 $r = 0.d_{1}d_{2}d_{3} \cdots$，其中

    $$
    d_{i} = \begin{cases}
    1 ,& d_{ii} \mod 2 = 0 \\
    0 ,& d_{ii} \mod 2 = 1
    \end{cases}
    $$

    容易发现，$r$ 和任意的 $r_{i}$ 在小数点后第 $i$ 位上都不同，即 $r$ 和任意的 $r_{i}$ 都不同。这与假设矛盾！

    故实数集合是不可数的。

如果我们将证明中的 $r_{i}$ 以一个表格的形式排列，则我们构造 $r$ 时考察的即为该表格中对角线上的所有数。这便是其「对角论证法」的由来。

这一证明方法的思想非常经典，后来被推广到用于证明很多相关命题。因此我们认为，读者应当完全掌握这一证明过程。

### 有关基数的定理

> 若 $A$ 和 $B$ 是可数集合，则 $A \cup B$ 也是可数集合。

这一定理的证明是简单的。

> 若集合 $A$ 和 $B$ 满足 $|A| \leq |B|$ 且 $|B| \leq |A|$，则 $|A| = |B|$。

这一定理也被称作**施罗德-伯恩斯坦定理** (Schröder–Bernstein theorem)。与直观感觉上不同，这一定理的证明是非常不容易的。这里我们就不给出具体的证明，有兴趣的读者可以参阅集合论相关教科书或[网络资料](https://zh.wikipedia.org/wiki/%E5%BA%B7%E6%89%98%E5%B0%94-%E4%BC%AF%E6%81%A9%E6%96%AF%E5%9D%A6-%E6%96%BD%E7%BD%97%E5%BE%B7%E5%AE%9A%E7%90%86)。

> 一个集合的基数总是小于其幂集的基数，即 $|S| < |\mathcal{P}(S)|$。

这一定理称作**康托尔定理** (Cantor's theorem)，我们给出其证明：

!!! abstract "Proof"

    假设存在映射 $f: S \to \mathcal{P}(S)$ 使得 $f$ 是满射。
    
    记 $T = \{x \in S | x \notin f(S)\}$，则 $T \subseteq S$，从而 $T \subseteq \mathcal{P}(S)$。

    由 $f$ 是满射，可知存在 $\xi \in S$ 使得 $f(\xi) = T$。

    (1) 若 $\xi \in T$，则 $\xi \notin f(\xi) = T$，矛盾！

    (2) 若 $\xi \notin T$，则 $\xi \in f(\xi) = T$，矛盾！

    综上，假设不成立，故不存在满射 $f: S \to \mathcal{P}(S)$。

    故 $|S| < |\mathcal{P}(S)|$。

### 可计算性

对于一个函数，若存在某个程序能够计算该函数的值，则称该函数为**可计算的** (computable)，反之则称其为**不可计算的** (uncomputable)。

对于这一定义，我们需要做一些补充说明。首先，所有程序构成的集合是可数的，这是由任何程序都可以看作由有限字母表构造的字符串所保证的。其次，从一个可数无限集到一个可数无限集可以建立的映射集合是不可数无限的，因此存在不可计算的函数。

这一定义是集合论在计算机科学中的重要应用。尽管如此，这里对「程序」、「字母表」、「字符串」的定义仍然比较暧昧，读者在这里可以先记住这一定义并理解其含义，更加严谨的定义和表述会在以后的学习中给出。

### 连续统假设

最后，让我们讨论一个著名的有关基数的猜想。

由康托尔定理可知，$|\mathbb{Z}| < |\mathcal{P}(\mathbb{Z})|$，即 $\aleph_{0} < 2^{\aleph_{0}}$。

记 $c = |\mathbb{R}|$，则 $|\mathcal{P}(\mathbb{Z})| = |\mathbb{R}|$，即 $2^{\aleph_{0}} = c$，从而得到 $\aleph_{0} < c$。

可以证明最小的无限基数形成了一个无限序列 $\aleph_{0} < \aleph_{1} < \aleph_{2} < \cdots$。

基于以上推理，康托尔提出了**连续统假设** (contimuun hypothesis)，即不存在集合 $A$ 使得 $\aleph_{0} < |A| < c$。据此可以推出 $c = \aleph_{1}$，则 $2^{\aleph_{0}} = \aleph_{1}$。

我们先前介绍了朴素集合论下的罗素悖论，以及为了避免悖论而出现的构造集合论。但是在现代数学的标准集合论公理，即 Zermelo-Fraenkel 公理下，连续统假设是一个不可判定命题。因此，这一猜想也引发了对 Zermelo-Fraenkel 公理合理性的争论以及对其它集合论公理的探索。正如历史上其他那些著名的数学猜想一样（费马大定理、黎曼猜想），连续统假设也作为一个重要的助力，推动着数学不断发展。

## 矩阵

矩阵是一个重要的数学概念，但是此处我们就不展开介绍了。对矩阵不甚熟悉的读者可以参阅线性代数相关教科书或网络资料。
