---
comments: true
---

# 第一章 - 概率论的基本概念

## 样本空间与随机事件

对随机现象进行观察、记录或试验，称为**随机试验** (random experiment)。其具有以下特点：

1. 可以在相同的条件下重复进行；
2. 每次试验可能出现的结果是不确定的，但能事先知道试验的所有可能结果；
3. 每次试验完成前不能预知哪一个结果会发生。

称随机试验的所有可能结果构成的集合为**样本空间** (sample space)，常记作 $S$ 或 $\Omega$。$S$ 中的每一个元素，即试验的每一个结果称作**样本点** (sample point)。样本空间的任一子集称作**随机事件** (random event)，简称**事件** (event)，常用字母 $A, B, C$ 表示。特别地，只含有一个样本点的时间称作**基本事件** (elementary event)。

在一次试验完成时，当试验所出现的结果（即样本点）属于某一事件，就称**该事件发生**，否则称**该事件不发生**。

特别地，若将样本空间 $S$ 亦视为一事件，由于试验的所有可能结果都在 $S$ 中，故在任何一次试验中事件 $S$ 一定会发生，因此常称 $S$ 为**必然事件** (certain event)。相对应地，空集 $\varnothing$ 中没有任何元素，故在任何一次试验中事件 $\varnothing$ 一定不发生，因此常称 $\varnothing$ 为**不可能事件** (impossible event)。

对应于集合运算，我们作出如下定义：

- **和事件** (union of events)：$A \cup B$
- **积事件** (intersection of events)：$A \cap B$
- **逆事件** (complementary events)：$\overline{A}$ 或 $A^{C}$，也称**对立事件**
- **差事件** (difference of events)：$A - B$ 或 $A \cap \overline{B}$

特别地，当 $A \cap B = \varnothing$ 时，称事件 $A$ 和事件 $B$ **互斥** (disjoint) 或**互不相容** (mutually exclusive)。

## 频率与概率

在相同条件下进行 $n (n \geq 1)$ 次重复试验，若事件 $A$ 在这 $n$ 次重复试验中发生 $n_{A} (0 \leq n_{A} \leq n)$ 次，称 $n_{A}$ 为 $A$ 在这 $n$ 次试验中发生的**频数**，则称比值 $\frac{n_{A}}{n}$ 为事件 $A$ 在这 $n$ 次试验中发生的**频率** (frequency)，记作 $f_{n} (A)$。

由这一定义，易得频率的性质：

1. $\forall A, 0 \leq f_{n} (A) \leq 1$
2. $f_{n} (S) = 1$
3. 若 $A \cap B = \varnothing$，则 $f_{n} (A \cup B) = f_{n} (A) + f_{n} (B)$

接下来我们定义概率。设某一随机试验所对应的样本空间为 $S$，对 $S$ 中的任一事件 $A$，定义一个实数 $P(A)$，若它满足以下三条公理：

1. 非负性：$P(A) \geq 0$
2. 规范性：$P(S) = 1$
3. 可列可加性：对 $S$ 中可列个两两互斥的事件 $A_{1}, A_{2}, \cdots, A_{n}, \cdots$，有 $P(\cup_{j = 1}^{+\infty} A_{j}) = \sum_{j = 1}^{+\infty} P(A_{j})$

则称 $P(A)$ 为事件 $A$ 发生的**概率** (probability)。

根据概率的公理化定义，易得概率的性质：

1. 有限可加性：对 $S$ 中有限个两两互斥的事件 $A_{1}, A_{2}, \cdots, A_{n}$，有 $P(\cup_{j = 1}^{n} A_{j}) = \sum_{j = 1}^{n} P(A_{j})$
2. $P(A) = 1 - P(\overline{A})$
3. 当 $A \supset B$ 时，$P(A - B) = P(A) - P(B)$，由此可推出 $P(A) \geq P(B)$
4. $P(A \cup B) = P(A) + P(B) - P(AB)$

## 等可能概型

一个随机试验如果满足如下两个条件：

1. 有限性：样本空间中的样本点数有限
2. 等可能性：出现每一个样本点的概率相等

则称这个试验为**等可能概型**，又称**古典概型**。

在等可能概型中，任一事件 $A$ 的概率为

$$P(A) = \frac{A \text{ 所包含的样本点数}}{S \text{ 中样本点总数}}$$

## 条件概率

如果 $P(B) > 0$，那么在 $B$ 发生的条件下 $A$ 发生的**条件概率** (conditional probability) 为

$$P(A | B) = \frac{P(AB)}{P(B)}$$

根据概率的性质，条件概率也有如下性质。当 $P(C) \neq 0$ 时，有

1. $P(A | C) \geq 0$
2. $P(S | C) = 1$
3. $P(B | C) = 1 - P(\overline{B} | C)$
4. 当 $A \supset B$ 时，$P(A | C) \geq P(B | C)$
5. $P(A \cup B | C) = P(A | C)  + P(B | C) - P(AB | C)$

特别地，若 $AB = \varnothing$，则 $P(A \cup B | C) = P(A | C) + P(B | C)$

由条件概率的定义知，当 $P(A) \neq 0, P(B) \neq 0$ 时，有

$$P(AB) = P(A) \cdot P(B | A) = P(B) \cdot P(A | B)$$

这称作概率的**乘法公式** (multiplication formula)。

设 $S$ 为某一随机试验的样本空间，$B_{1}, B_{2}, \cdots, B_{n}$ 为该试验的一组事件，且满足：

1. $B_{i} B_{j} = \varnothing, i, j = 1, 2, \cdots, n, i \neq j$
2. $B_{1} \cup B_{2} \cup \cdots \cup B_{n} = S$

则称 $B_{1}, B_{2}, \cdots, B_{n}$ 为 $S$ 的一个**划分**，或 $S$ 的一个**完备事件组**。

此时对任一事件 $A$，有

$$P(A) = \sum_{j = 1}^{n} P(B_{j}) P(A | B_{j})$$

这称作概率的**全概率公式** (law of total probability)。

而反之有

$$P(B_{k} | A) = \frac{P(B_{k} A)}{P(A)} = \frac{P(B_{k} P(A | B_{k}))}{\sum_{j = 1}^{n} P(B_{j}) P(A | B_{j})}, k = 1, 2, \cdots, n$$

这称作概率的**贝叶斯公式** (Bayes formula)，或**逆概公式**。

通常地，我们称 $P(B_{j})$ 为**先验概率** (prior probability)，$P(B_{j} | A)$ 为**后验概率** (posterior probability)。

## 事件的独立性与独立试验

设 $A, B$ 为两随机事件，当 $P(AB) = P(A) \cdot P(B)$ 时，称事件 $A, B$ **相互独立** (independent)。

当 $P(A) \cdot P(B) \neq 0$ 时，事件 $A, B$ 相互独立等价于 $P(B | A) = P(B)$ 或 $P(A | B) = P(A)$。

当事件 $A, B$ 相互独立时，$A$ 与 $\overline{B}$、$\overline{A}$ 与 $B$、$\overline{A}$ 与 $\overline{B}$ 均相互独立。

设 $n$ 个事件 $A_{1}, A_{2}, \cdots, A_{n} (n \geq 2)$，若对其中任意 $k$ 个事件 $A_{i_{1}}, A_{i_{2}}, \cdots, A_{i_{k}} (2 \leq k \leq n)$，都有 $P(A_{i_{1}} A_{i_{2}} \cdots A_{i_{k}}) = \prod_{j = 1}^{k} P(A_{i_{j}})$ 成立，则称事件 $A_{1}, A_{2}, \cdots, A_{n} (n \geq 2)$ **相互独立**。

常用的一个原理是：概率很小的事件在一次试验中几乎不发生。这称作**实际推断原理**。
