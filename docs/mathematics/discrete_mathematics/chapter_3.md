---
comments: true
---

# 第三章 - 算法

## 算法

**算法** (algorithm) 是进行一项计算或解决一个问题的精确指令的有限序列。

算法一般需要满足以下性质：

- 输入：算法从一个指定的集合得到输入值。
- 输出：对每个输入值集合，算法都要从一个指定的集合中产生输出值。
- 确定性：算法的步骤必须是准确定义的。
- 正确性：对于任何输入，算法都应得到正确的输出值。
- 有限性：对于任何输入，算法都应在有限步后产生输出值。
- 有效性：算法的每一步都应该在有限时间内完成。
- 通用性：算法应当对所有合法的输入有效，而不是只对若干特定的输入有效。

### 搜索算法

这一部分知识相对基础故不再展开，不熟悉的读者可以参阅算法设计相关教科书或[网络资料](https://oi-wiki.org/basic/binary/)。

### 排序算法

这一部分知识相对基础故不再展开，不熟悉的读者可以参阅算法设计相关教科书或[网络资料](https://oi-wiki.org/basic/sort-intro/)。

### 字符串匹配算法

这一部分知识相对基础故不再展开，不熟悉的读者可以参阅算法设计相关教科书或[网络资料](https://oi-wiki.org/string/match/)。

### 贪心算法

大部分算法用于解决**最优化问题** (optimisation problem)，这类问题的目标是寻找使某个参数最小或最大的解。

一个常见的用于解决最优化问题的算法称作**贪心算法** (greedy algorithm)，即在每一步都选择局部最优的策略。容易意识到每一步局部最优并不一定能得到全局最优，因此贪心算法并不能用于解决所有的最优化问题。因此，当我们能够证明贪心算法得到的解是全局最优解时，就可以应用贪心算法解决问题。

限于篇幅我们不再展开对贪心算法的说明，读者可以参阅算法设计相关教科书或[网络资料](https://oi-wiki.org/basic/greedy/)进一步学习。

### 停机问题

**停机问题** (halting problem) 是一个经典的不可解问题。其询问是否存在一个**过程** (procedure)，使得以一个计算机程序和该程序的一个输入作为输入，并判断该程序在给定输入运行时是否能最终停止。

我们采用反证法证明这个问题是不可解的。

!!! Proof

    假设停机问题存在解，设这个解为 $H(P, I)$，其中 $P$ 是程序，$I$ 是程序 $P$ 的一个输入。如果 $H$ 判定 $P$ 在给定输入 $I$ 时能停止，则 $H$ 输出「停机」，否则输出「死循环」。

    需要注意的是，程序作为一个字符串，本身也可以作为输入，即我们可以考察 $H(P, P)$。

    接下来我们构造这样一个过程 $K(P)$，其流程如下：

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_3_1.png" width="70%" style="margin: 0 auto;">
    </div>

    接下来我们考察 $H(K, K)$。根据流程可以推知，如果 $H(K, K)$ 的输出是「死循环」，那么 $K(K)$ 就应该停机，矛盾！如果 $H(K, K)$ 的输出是「停机」，那么 $K(K)$ 就应该死循环，矛盾！

    综上，$H$ 的存在性总是能推导出矛盾，故不存在这样的 $H$。

## 函数的增长

这部分请参考[数据结构基础 - 第一章 - 算法分析](https://victorwang712.github.io/Note/computer_science/data_structure_basics/chapter_1/)。

## 算法复杂度

### 时间复杂度与空间复杂度

这部分请参考[数据结构基础 - 第一章 - 算法分析](https://victorwang712.github.io/Note/computer_science/data_structure_basics/chapter_1/)。

### P 与 NP 问题

**P 类** (polynomial time class) 问题指可以在多项式时间内求解的问题，**NP 类** (nondeterministic polynomial class) 问题指可以在多项式时间内验证解的问题。

**NP 完全问题** (NP-complete problem) 是一类具有特定性质的 NP 问题，即只要这类问题中任意一个问题可以用多项式时间求解（即为 P 类问题），那么所有 NP 类问题都已用多项式时间求解（即 $\text{P} = \text{NP}$）。

**P 与 NP 问题** (P versus NP problem) 就是考察 P 是否等于 NP。这一问题是理论计算机科学中重要的开放问题。
