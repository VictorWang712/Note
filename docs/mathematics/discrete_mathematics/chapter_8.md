---
comments: true
---

# 第八章 - 图

## 图和图模型

这部分请参考[数据结构基础 - 第六章 - 图论算法](https://victorwang712.github.io/Note/computer_science/data_structure_basics/chapter_6/#_2)。

我们给出一个表格供参考：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_8_1.png" width="70%" style="margin: 0 auto;">
</div>

## 图的术语

我们先约定如下记号。

图 $G = (V, E)$ 中，顶点 $v$ 的所有相邻顶点的集合记作 $N(v)$。若 $A$ 是 $V$ 的子集，我们用 $N(A)$ 表示图 $G$ 中至少和 $A$ 中一个顶点相邻的所有顶点的集合，即 $N(A) = \cup_{v \in A} N(v)$。

顶点 $v$ 的**度** (degree) 是与该顶点相关联的边的数目，记作 $\deg (v)$。在带有有向边的图里，以 $v$ 作为终点的边数称作顶点 $v$ 的入度，记作 $\deg^{-} (v)$；以 $v$ 作为起点的边数称作顶点 $v$ 的出度，记作 $\deg^{+} (v)$。

根据这些定义，我们可以得到许多有关图的性质。

设 $G = (V, E)$ 是有 $m$ 条边的无向图，则 $2m = \sum_{v \in V} \deg (v)$。这个结论被称作**握手定理** (handshaking lemma)。

无向图有偶数个度为奇数的顶点。

对于有向图 $G = (V, E)$，有 $\sum_{v \in V} \deg^{-} (v) = \sum_{v \in V} \deg^{+} (v) = |E|$。

这些性质都是容易从定义得到的。

## 几种特殊的图

在每对不同顶点间恰有一条边的简单图称作**完全图** (complete graph)，有 $n$ 个顶点的完全图记作 $K_{n}$。

由 $n (n \geq 3)$ 个顶点 $v_{1}, v_{2}, \cdots, v_{n}$ 以及边 $\{ v_{1}, v_{2} \}, \{ v_{2}, v_{3} \}, \cdots, \{ v_{n - 1}, v_{n} \}, \{ v_{n}, v_{1} \}$ 组成的图称作**圈图** (cycle graph)，记作 $C_{n}$。

对于圈图 $C_{n}, n \geq 3$，添加一个新顶点，并且该顶点与 $C_{n}$ 中的 $n$ 个顶点均相连，则得到**轮图** (wheel graph)，记作 $W_{n}$。下图展示了一些轮图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_8_2.png" width="70%" style="margin: 0 auto;">
</div>

若一个图含有 $2^{n}$ 个顶点，且两个顶点相邻当且仅当其下标数的二进制表示仅有一位不同，则这样的图称作**$n$ 立方体图** ($n$-cube graph)。下图展示了一些立方体图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_8_3.png" width="70%" style="margin: 0 auto;">
</div>

若简单图 $G$ 的顶点集可以被分成两个不相交的非空集合 $V_{1}$ 和 $V_{2}$，使得图中的每一条边的两个端点刚好分别属于 $V_{1}$ 和 $V_{2}$，则称 $G$ 为**二分图** (bipartite graph)。此时称 $(V_{1}, V_{2})$ 为 $G$ 的顶点集的一个二部划分。

一个简单图是耳根图，当且仅当能够对图中的每个顶点赋予两种不同的颜色之一，并使得没有两个相邻的顶点被赋予相同的颜色。

若简单图的顶点集划分成分别含有 $m$ 和 $n$ 个顶点的两个子集，且两个顶点之间有边当且仅当两个顶点分别属于两个子集，则称该图为**完全二分图** (complete bipartite graph)，记作 $K_{m, n}$。

在简单图 $G = (V, E)$ 中的一个**匹配** (matching) $M$ 是边集 $E$ 的子集，该自己种没有两条边关联相同的顶点。包含最多边数的一个匹配称作**最大匹配** (maximum matching)。若一个二分图的划分为 $(V_{1}, V_{2})$，且 $|M| = |V_{1}|$，则称匹配 $M$ 是从 $V_{1}$ 到 $V_{2}$ 的一个**完全匹配** (complete matching)。

带有二部划分 $(V_{1}, V_{2})$ 的二分图 $G = (V, E)$ 中存在从 $V_{1}$ 到 $V_{2}$ 的一个完全匹配，当且仅当对于 $V_{1}$ 的所有子集 $A$，有 $|N(A)| \geq |A|$。这一定理称作**霍尔婚姻定理** (Hall's marriage theorem)。


