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

令 $p$ 为一命题，则 $p$ 的否定记作 $\neg p$ 或 $\bar{p}$，指「不是 $p$ 所指的情形」，其真值与 $p$ 的真值相反。

令 $p$ 和 $q$ 为命题，

- $p$、$q$ 的**合取** (conjunction) 即命题「$p$ 且 $q$」，记作 $p \wedge q$
- $p$、$q$ 的**析取** (disjunction) 即命题「$p$ 或 $q$」，记作 $p \vee q$
- $p$、$q$ 的**异或** (disjunction) 即命题「$p$ 或 $q$」，记作 $p \oplus q$

### 条件语句

语句 $p \to q$ 称为条件语句，即「若 $p$，则 $q$」。条件语句也称为**蕴含** (imply)，即「**$p$ 蕴含 $q$** ($p$ implies $q$)」。其**真值表** (truth table) 如下：

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

另一种表示两个命题具有相同真值的命题符合方式是**双条件** (biconditional) 语句或双向蕴含，记作 $p \leftrightarrow q$，即「$p$ 当且仅当 $q$」。其真值表如下：

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

    但是请注意，$\to$ 和 $\leftrightarrow$ 的作用顺序往往有歧义，这种情况下我们推荐并鼓励使用括号来明确表达式。

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

    请注意，$\equiv$ 和 $\Leftrightarrow$ 不是逻辑联结词，$p \equiv q$ 不是一个复合命题，而是代表「$p \leftrightarrow q$ 是永真式」这一语句。

一个常用的判定两个命题是否等价的方法是考察其真值表。只要两个命题的真值表完全一致，那么这两个命题就是等价的。通过这种方法我们可以得到一个非常重要的逻辑等价式：**德摩根定律** (De Morgan's laws)。

- $\neg (p \wedge q) \equiv \neg p \vee \neg q$
- $\neg (p \vee q) \equiv \neg p \wedge \neg q$

德摩根定律可以推广到任意有限多个命题：

- $\neg \left( \bigvee_{i = 1}^{n} p_{i} \right) \equiv \bigwedge_{i = 1}^{n} \neg p_{i}$
- $\neg \left( \bigwedge_{i = 1}^{n} p_{i} \right) \equiv \bigvee_{i = 1}^{n} \neg p_{i}$

遵循这种方式，我们还可以给出若干基础的逻辑恒等式：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_1.png" width="70%" style="margin: 0 auto;">
</div>

在分析更加复杂的复合命题时，对于有 $n$ 个变量的复合命题需要考察具有 $2^{n}$ 种情况的真值表。这种指数级的增加是实际情况中不能接受的。因此我们常基于已经给出的逻辑恒等式，对复杂的表达式进行变形化简。

### 可满足性

对于一个含有若干变量的复合命题，若存在一种变量的赋值方式，使其真值为真，则称这个命题是**可满足的** (satisfiable)。

一个不可满足的命题即为一个矛盾式。

## 谓词和量词

命题逻辑提供了一种完备的逻辑语句表示方法，但仍不足以表达所有数学语句和自然语句。为此，我们引入一种表达能力更强的逻辑，即**谓词逻辑** (predicate logic)。

### 谓词

一般地，涉及 $n$ 个变量 $x_{1}, x_{2}, \cdots, x_{n}$ 的语句可以表示成 $P(x_{1}, x_{2}, \cdots, x_{n})$。形式为 $P(x_{1}, x_{2}, \cdots, x_{n})$ 的语句是**命题函数** (propositional function) $P$ 在 $n$ 元组 $(x_{1}, x_{2}, \cdots, x_{n})$ 下的值，$P$ 也称为 $n$ 元**谓词** (predicate)。

谓词还可以用来验证计算机程序，也就是证明当给定合法输入时计算机程序总是能产生所期望的输出。描述合法输入的语句称作**前置条件** (precontdition)，而程序运行的输出应该满足的条件称作**后置条件** (postcondition)。

### 量词

从命题函数出发生成一个命题一般有两种做法。一种方法是将命题函数中的变量全部赋值；另一种方法被称作**量化** (quantification)，即表示谓词对于某种范围上的个体成立。

量化在语句中依赖**量词** (quantifier) 来描述，常见的量词有*所有*，*存在*等。处理谓词和量词的逻辑领域称作**谓词演算** (predicate calculus)。

我们主要考察的量词有如下几类：

- **全称量词** (universal quantifier)：许多数学命题断言某一性质对于变量在某一特定域内的所有值均为真，这一特定域称作变量的**论域** (domain of discourse) 或**全体域** (universe of discourse)，也简称作**域** (domain)。这类语句可以用全称量化表示。具体来说，$P(x)$ 的全称量化是语句「$P(x)$ 对 $x$ 在其论域的所有值为真。」符号 $\forall xP(x)$ 表示 $P(x)$ 的全称量化，其中 $\forall$ 是全称量词。
- **存在量词** (existential quantifier)：许多数学命题断言有一个个体使得某种性质成立。这类语句可以用存在量化表示。具体来说，$P(x)$ 的存在量化是命题「论语中存在一个个体 $x$ 满足 $P(x)$。」符号 $\exist xP(x)$ 表示 $P(x)$ 的存在量化，其中 $\exist$ 称为存在量词。

### 有限域上的量词

当一个量词的域是有限的时候，量化语句就可以用命题逻辑来表达。

设论域中的元素为 $x_{1}, x_{2}, \cdots, x_{n}$，其中 $n \in \mathbb{N}^{+}$，则全称量化 $\forall xP(x)$ 与合取式 $P(x_{1}) \wedge P(x_{2}) \wedge \cdots \wedge P(x_{n})$ 相同；存在量化 $\exist xP(x)$ 与析取式 $P(x_{1}) \vee P(x_{2}) \vee \cdots \vee P(x_{n})$ 相同。

### 变量绑定

当量词作用于变量 $x$ 时，我们称该变量的这次出现为**约束的** (bound)；如果没有被量词约束或被赋值，则称该变量的这次出现为**自由的** (free)。

要用命题函数生成命题，必须要求函数中的所有变量被量词约束或被赋值。

逻辑表达式中一个量词作用到的部分称作这个量词的作用域。据此，若一个变量在公式中所有约束该变量的量词作用域之外，则该变量是自由的。

### 涉及量词的逻辑等价式

对于两个涉及谓词和量词的语句，若无论用什么谓词带入这些语句，且无论为这些命题函数里的变量指定什么论域，它们都有相同的真值，则称这两个语句是逻辑等价的。

### 量化表达式的否定

全称量词和存在量词的一般形式如下：

- $\neg \forall x P(x) \equiv \exist x \neg P(x)$
- $\neg \exist x Q(x) \equiv \forall x \neg Q(x)$

这一量词否定的规则称作**量词的德摩根定律** (De Morgan's laws for quantifiers)。

## 嵌套量词

若一个量词出现在另一个量词的作用域内，则称该量词为**嵌套量词** (nested quantifier)。

### 嵌套量词的否定

要否定含有嵌套量词的语句，我们只需要递归地使用单个量词语句的否定规则。

## 推理规则

数学中的证明是建立数学命题真实性的有效论证，因此我们将围绕命题逻辑中的论证展开讨论。

### 命题逻辑的有效论证

在命题逻辑中，具体的相关定义如下：

- **论证** (argument)：按一定顺序排列的若干命题
- **结论** (conclusion)：论证中的最后一个命题
- **前提** (premise)：论证中除结论外的其他命题

若论证中所有前提 $p_{i}$ 为真蕴含着结论 $q$ 为真，即 $(p_{1} \wedge p_{2} \wedge \cdots \wedge p_{n}) \to q$ 是永真式时，则称该论证是**有效的** (valid)。

### 命题逻辑的推理规则

我们总是可以用一个真值表来证明一个论证是有效的，但这一方法显然难以推广到具有较多命题变量的论证中。故我们需要建立一些相对简单的论证形式，即**推理规则** (rule of inference)。

最常见的推理规则是**假言推理** (modus ponens)，或称**分离规则** (law of detachment)。该规则基于永真式 $(p \wedge (p \to q)) \to q$。

进一步地，从常见的永真式出发，我们可以给出更多的推理规则：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_2.png" width="70%" style="margin: 0 auto;">
</div>

### 消解律

在实际应用中，非常重要的一个推理规则是**消解律** (resolution)。该规则基于永真式 $((p \vee q) \wedge (\neg p \vee r)) \to (q \vee r)$，其中我们称式中被蕴含的 $q \vee r$ 为**消解式**(resolvent)。

消解律在基于逻辑规则的编程语言中扮演着重要角色，因为可以仅用消解律构建自动定理证明系统。为做到这一点，假设和结论必须表示为**子句** (clause)，即变量或其否定的一个析取式。

> 例如，对于语句 $\neg (p \vee q)$，我们应使用德摩根定律将其变形为 $\neg p \wedge \neg q$。

### 谬误

如果一个基于可满足式而非永真式构建推理规则，我们就可能出现**谬误** (fallacy)。了解谬误的常见模式有助于我们判断推理的有效性。

命题 $((p \to q) \wedge q) \to p$ 不是永真式，当 $p$ 为假而 $q$ 为真时该命题为假。基于这一命题构建的推理被称作**肯定结论的谬误** (fallacy of affirming the conclusion)。

> 举例来说：
>
> - 前提：如果你做离散数学课本的练习题，那你就学习离散数学。你学习离散数学。
> - 结论：你做了离散数学课本的练习题
>
> 显然这个推理是一个谬误。

命题 $((p \to q) \wedge \neg p) \to \neg q$ 不是永真式，当 $p$ 为假而 $q$ 为真时该命题为假。基于这一命题构建的推理被称作**否定假设的谬误** (fallacy of denying the hypothesis)。

> 举例来说：
>
> - 前提：如果你做离散数学课本的练习题，那你就学习离散数学。你没有做离散数学课本的练习题。
> - 结论：你没有学习离散数学。
>
> 显然这个推理也是一个谬误。

### 量化命题的推理规则

论述完命题的推理规则，现在我们关注含有量词的命题的推理规则。常见的量化命题的推理规则如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_3.png" width="70%" style="margin: 0 auto;">
</div>

### 命题和量化命题的推理规则的组合使用

在大部分论证中，我们既要使用命题推理规则，又要使用量化命题推理规则。接下来我们要讨论这种组合的常见模式。

其中最广泛的组合是将全称实例和假言推理一起使用，这种组合被称作**全称假言推理** (universal modus ponens)。描述如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_4.png" width="70%" style="margin: 0 auto;">
</div>

另一种常见的组合是将全称实例和取拒式，这种组合被称作**全称取拒式** (universal modus tollens)。描述如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_5.png" width="70%" style="margin: 0 auto;">
</div>

## 证明导论

在给出了各种概念和常见模式后，我们现在可以开始考察具体的证明了。

在截至目前的数学课程中学习的证明绝大部分是**非形式化证明** (informal proof)，这是为了方便人们阅读理解。但如果我们目标是建立证明的自动化系统，那么**形式化证明** (formal proof) 显然是更值得被采用的。

### 专用术语

先给出一些证明中会用到的术语：

- **定理** (theorem)：形式上就是一个能够被证明为真的命题，但数学描述中常用于专指那些有一定重要性的真命题。
- **事实** (fact)：不太重要的定理，有时也称作**结论** (result)。（请注意和 conclusion 区分）
- **证明** (proof)：建立定理真实性的一个有效论证。
- **引理** (lemma)：重要性略低但有助于证明其它结论的定理。
- **推论** (corollary)：从一个已经被证明的定理可以直接建立起来的一个定理。
- **猜想** (conjecture)：一个被提出认为是真，但尚未被证明的命题。

### 证明定理的方法

接下来我们将讨论常见的证明条件语句的方法。但在此之前，出于个人的强烈意愿，笔者希望宕开一笔，展示课本中的这样一段内容：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/discrete_mathematics/Chapter_1_6.png" width="70%" style="margin: 0 auto;">
</div>

对于非形式化证明的简略程度一直备受争论，笔者强烈支持课本上这种「从读者出发」的态度，即根据目标读者的知识程度确定证明的简略程度。

回到正题，我想这个小插曲也能一定程度上反映形式化证明的价值。

#### 直接证明法

用直接证明法证明条件语句 $p \to q$ 的一般步骤：

- 假设 $p$ 为真
- 用公理、定义和已证明的定理，并结合推理规则构造推理
- 证明 $q$ 也为真

#### 反证法

所有直接证明法之外的证明方法都称作间接证明法，即不以前提开始、以结论结束的证明方法。

间接证明法中最常用的一类方法是**反证法** (proof by contraposition)。反证法的正确性是建立在一个基本的逻辑事实，即 $p \to q$ 等价于逆否命题 $\neg q \to \neg p$。

用反证法证明条件语句 $p \to q$ 的一般步骤：

- 假设 $\neg q$ 为真
- 用公理、定义和已证明的定理，并结合推理规则构造推理
- 证明 $\neg p$ 也为真

#### 归谬证明法

在数学学习中我们一般不区分反证法和**归谬证明法** (proof by contradiction)，但是在形式化证明中，我们还是有必要加以区分并分别讨论。

假设我们要证明 $p$ 为真，再假设我们能找到一个矛盾式 $q$ 使得 $\neg \to q$ 为真。因为 $q$ 恒为假，所以我们能得到 $\neg p$ 为假，即证明了 $p$ 为真。

而常见的构造矛盾式 $q$ 的方法，就是另找一个命题 $r$，使得 $q = r \wedge \neg r$，也就是我们常说的「构造矛盾」。

系统地说，用反证法证明条件语句 $p \to q$ 的一般步骤：

- 假设存在某个命题 $r$ 使得 $\neg p \to (r \wedge \neg r)$ 为真
- 则 $p$ 为真

#### 等价证明法

为了证明形如 $p \leftrightarrow q$ 为真这样的命题，我们只需证明 $p \to q$ 和 $q \to p$ 都为真。其正确性是建立在重言式 $(p \leftrightarrow q) \leftarrow (p \to q) \wedge (q \to p)$ 的基础上的。

进一步地，我们可以将这一方法推广到 $n$ 个命题。当我们需要证明命题 $p_{1} \leftrightarrow p_{2} \leftrightarrow \cdots \leftrightarrow p_{n}$ 时，我们只需证明 $p_{1} \to p_{2}, p_{2} \to p_{3}, \cdots, p_{n - 1} \to p_{n}, p_{n} \to p_{1}$ 即可。

???+ note

    通过上式我们不难发现，在证明「推导链」的过程中，选取命题的顺序并不重要，只需要保证在遍历完「推导链」后每个命题都被涵盖了即可。在实际证明中，我们常根据命题间推出的难度，选取较为简单的路径进行证明。

### 空证明和平凡证明

介绍完常见的几种证明方法后，我们再稍微讨论一下两种特别的证明。

当 $p$ 为假时，对于任意的 $q$，$p \to q$ 一定为真。因此如果能证明 $p$ 为假，那么我们就得到了一个 $p \to q$ 的证明方法，这种证明称作**空证明** (vacuous proof)。

当 $q$ 为真时，对于任意的 $p$，$p \to q$ 一定为真。因此如果能证明 $q$ 为真，那么我们就得到了一个 $p \to q$ 的证明方法，这种证明称作**平凡证明** (trivial proof)。

空证明和平凡证明看似无甚意义，但实际上在证明定理的一些特例和数学归纳法中有特别的应用。这些我们会在以后讨论。

## 证明的方法和策略

前文中我们之间要讨论了构造证明的策略，接下来我们将讨论一些具体如何完成推理的方法和策略。

### 穷举证明法

有些定理可以通过检验相对少量的例子来证明，这要的证明称作**穷举证明法** (exhaustive proof, proof by exhaustion)。

### 分情形证明法

分情形证明是按照一定的标准，将命题中所有可能的情况分成若干情形分别加以证明。分情形证明法的关键在于各情形要能覆盖定理中所有可能出现的情况。

### 存在性证明

形如 $\exist x P(x)$ 的命题的证明称作**存在性证明** (existance proof)。存在性证明一般有两种方法：

- **构造性** (constructive) 证明：直接给出使得 $P(\xi)$ 为真的 $\xi$
- **非构造性** (nonconstructive) 证明：不直接给出使得 $P(\xi)$ 为真的 $\xi$，而是通过其他方式完成证明

???+ note

    最常见的非构造性证明是采用归谬证明，即假设不存在使得 $P(x)$ 为真的 $x$，再试图推导出矛盾。

### 唯一性证明

某些命题断言具有特定性质的元素唯一存在，这类命题的证明称作**唯一性证明** (uniqueness proof)，其一般步骤如下：

- 存在性：证明存在某个元素 $x$ 具有期望的性质
- 唯一性：证明如果 $x$ 和 $y$ 都具有期望的性质，则 $x = y$

### 正向和反向推理

无论选择什么证明方法，都需要为证明找一个起点，即前提。利用这些前提以及公理和已知定理，用导向结论的一系列步骤来构造证明。这类推理称为**正向推理** (forward reasoning)，是用来证明相对简单结论的一类最常见推理方式。

遗憾的是，正向推理常常难以用来证明更复杂的结论，因为得出想要的结论所需要的推理可能并不明显。在这种情况下使用**反向推理** (backward reasoning) 可能会有所帮助。例如我们要反向推理证明命题 $q$，我们就寻找一个命题 $p$ 满足 $p \to q$。

在实际情况中，我们一般综合使用正向推理和反向推理，并期望两者的「推导链」在某一命题处「交会」，这样就完成了完整的证明。
