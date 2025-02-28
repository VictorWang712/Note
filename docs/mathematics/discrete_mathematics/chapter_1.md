---
comments: true
---

# 第一章 - 基础：逻辑和证明

## 命题逻辑

### 命题

**命题** (proposition) 是一个陈述事实的语句，它或真或假，但不能既真又假。

**命题变量** (propositional variable)，或称为**语句变量** (
statement variable) 是一个命题的变量，常用字母来表示。

如果一个命题是真命题，则其**真值** (true value) 为真，用 T 表示；反之为假，用 F 表示。

不能用简单的命题来表示的命题称为**原子命题** (atomic proposition)。

设计命题的逻辑称为**命题逻辑**或**命题演算** (propositional calculus)。

许多数学陈述都是由一个或多个命题组合而来。由已知命题用**逻辑运算符** (logical operators) 组合而来的新命题也被称为**复合命题** (compound proposition)。

令 $p$ 为一命题，则 $p$ 的否定记作 $\neg p$ 或 $\bar{p}$，指“不是 $p$ 所指的情形”，其真值与 $p$ 的真值相反。

令 $p$ 和 $q$ 为命题，

- $p$、$q$ 的**合取** (conjunction) 即命题“$p$ 且 $q$”，记作 $p \wedge q$
- $p$、$q$ 的**析取** (disjunction) 即命题“$p$ 或 $q$”，记作 $p \vee q$
- $p$、$q$ 的**异或** (disjunction) 即命题“$p$ 或 $q$”，记作 $p \oplus q$

### 条件语句

语句 $p \to q$ 称为条件语句，即“若 $p$，则 $q$”。条件语句也称为**蕴含** (imply)，即“**$p$ 蕴含 $q$** ($p$ implies $q$)”。其**真值表** (truth table) 如下：

|$p$|$q$|$p \to q$|
|:-:|:-:|:-:|
|0|0|1|
|0|1|1|
|1|0|0|
|1|1|1|

???+ note

    有必要对这个真值表做出解释。当 $p$ 为真时的两种情况往往易于理解，而 $p$ 为假的情况就不是很显然了。一个常用的理解方法是，在认可 $p$ 为真的两种情况下，考察其逆否命题。

    举例来说：$p \to q$ 的逆否命题为 $\neg q \to \neg p$，当 $p = 0, q = 0$ 时，$\neg q = 1, \neg p = 1$，故该命题为真命题。

由条件语句 $p \to q$ 可以构成一些新的条件语句。

- 命题 $p \to q$ 称为逆命题
- $\neg p \to \neg q$ 称为否命题
- $\neg q \to \neg p$ 称为逆否命题

原命题的真值并不能决定其逆命题和否命题的真值，但很重要的一条性质是：原命题与其逆否命题的真值总是相等的。

当两个复合命题的真值表相同时，我们称这两个命题具有**等价关系** (equivalence relation)，即两者是等价的。

另一种表示两个命题具有相同真值的命题符合方式是**双条件** (biconditional) 语句或双向蕴含，记作 $p \leftrightarrow q$，即“$p$ 当且仅当 $q$”。其真值表如下：

|$p$|$q$|$p \leftrightarrow q$|
|:-:|:-:|:-:|
|0|0|1|
|0|1|0|
|1|0|0|
|1|1|1|

通过简单的推导可以得到 $p \leftrightarrow q$ 与 $(p \to q) \wedge (q \to p)$ 等价。

### 复合命题

我们已经定义了五个重要的逻辑联结词：合取、析取、异或、蕴含、双条件，同时我们还定义了否定。用这些联结词，我们可以构造含有一些命题变量的复合命题。

### 逻辑运算符的优先级

一个通用的优先级规则如下：

|运算符|优先级|
|:-:|:-:|
|$\neg$|1|
|$\wedge$|2|
|$\vee$|3|
|$\to$|4|
|$\leftrightarrow$|5|

???+ warning

    但是请注意，$\to$ 和 $\leftrightarrow$ 的作用顺序往往有歧义，这种情况下我们鼓励使用括号来明确表达式。

## 命题逻辑的应用

### 逻辑电路

这部分请参考[数字逻辑设计 - 第二章 - 组合逻辑电路](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_2/)。

## 命题等价式

### 复合命题的分类

根据可能的真值，我们可以将所有复合命题分成如下三类：

- **永真式** (tautology)：永远为真的复合命题，也常称作重言式。
- **矛盾式** (contradiction)：永远为假的复合命题
- **可能式** (contingency)：既不是永真式也不是矛盾式的复合命题

### 逻辑等价式

若 $p \leftrightarrow q$ 是永真式，即两个复合命题在所有可能的情况下都具有相同真值，则称这两个是**逻辑等价** (logically equivalent) 的，记作 $p \equiv q$，也可记作 $p \Leftrightarrow q$。

???+ warning

    请注意，$\equiv$ 和 $\Leftrightarrow$ 不是逻辑联结词，$p \equiv$ 不是一个复合命题，而是代表“$p \leftrightarrow q$ 是永真式”这一语句。

一个常用的判定两个命题是否等价的方法是考察其真值表。只要两个命题的真值表完全一致，那么这两个命题就是等价的。通过这种方法我们可以得到一个非常重要的逻辑等价式：**德摩根定律** (De Morgan's laws)。

- $\neg (p \wedge q) \equiv \neg p \vee \neg q$
- $\neg (p \vee q) \equiv \neg p \wedge \neg q$

德摩根定律可以推广到任意优先多的命题：

- $\neg \left( \bigvee_{i = 1}^{n} p_{i} \right) \equiv \bigwedge_{i = 1}^{n} \neg p_{i}$
- $\neg \left( \bigwedge_{i = 1}^{n} p_{i} \right) \equiv \bigvee_{i = 1}^{n} \neg p_{i}$

遵循这种方式，我们还可以给出若干基础的逻辑恒等式：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/chapter_1_1.png" width="70%" style="margin: 0 auto;">
</div>

在分析更加复杂的复合命题时，对于有 $n$ 个变量的复合命题需要考察具有 $2^{n}$ 种情况的真值表。这种指数级的增加是实际情况中不能接受的。因此我们常基于已经给出的逻辑恒等式，对复杂的表达式进行变形化简。

### 可满足性

对于一个含有若干变量的复合命题，若存在一种变量的赋值方式，使其真值为真，则称这个命题是**可满足的** (satisfiable)。

一个不可满足的命题即为一个矛盾式。

## 谓词和量词

命题逻辑提供了一种完备的逻辑语句表示方法，但仍不足以表达所有数学语句和自然语句。为此，我们引入一种表达能力更强的逻辑，即**谓词逻辑** (predicate logic)。

### 谓词

一般地，涉及 $n$ 个变量 $x_{1}, x_{2}, \cdots, x_{n}$ 的语句可以表示成 $P(x_{1}, x_{2}, \cdots, x_{n})$。形式为 $P(x_{1}, x_{2}, \cdots, x_{n})$ 的语句是**命题函数** (propositional function) $P$ 在 $n$ 元组 $(x_{1}, x_{2}, \cdots, x_{n})$ 下的值，$P$ 也称为 $n$ 元**谓词** (predicate)。