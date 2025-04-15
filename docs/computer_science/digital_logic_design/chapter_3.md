---
comments: true
---

# 第三章 - 组合逻辑电路的设计

一般地，设计一个数字系统的过程为：

1. 指定所需的行为
2. 以布尔方程或真值表的方式对系统的输入和输出关系形式化
3. 优化逻辑行为的表示，减少所需逻辑门的数量
4. 将优化后的逻辑映射到可以实现的工艺上
5. 验证最后设计的正确性

本章我们将主要讨论其中的前四步。

## 分层设计

对于复杂的数字系统，一种典型的设计方法是**分层设计** (hierarchical design)，而不是将设计过程应用在整个系统层面上，由此产生的相关概念构成了电路设计的**层次** (hierarchy) 结构。

为了处理复杂电路，电路被我们分成称之为**模块** (block) 的多个部分，并按照前述的设计过程设计模块。模块之间相互连接构成电路。如果一个模块作为单一实体仍然太大而难以设计，则可以将这个模块分成多个更小的模块。

分层设计可以极大程度上简化复杂电路的表示。我们进一步给出如下定义：分层设计末端的模块称作**原子模块** (primitive block)，我们认为原子模块都是**预定义** (predefine) 的，在电路图中用符号而不用逻辑图来表示，其功能用程序或语言描述而不用电路图来定义。

分层设计的另一个特性是模块的**可重用** (reuse) 性，即在同一电路中，可以有许多模块的功能是一致的。实现这个目标的先决条件是电路必须是**规整** (regularity) 的，即这个**规整电路** (regular circuit) 可以通过重用一定数量的不同模块来实现；而**不规整电路** (irregular circuit) 则没有这个特性。

对于一个给定的可重用的模块，其设计只需要一次。出现在设计中的模块称作这个模块的一个**实例** (instance)，其应用称作**实例化** (instantiation)。

显然各种电路的规整程度都不一样，我们常这样衡量电路的规整度，即考察最终电路中原子模块的数量与分层设计框图中基本模块（包括原子模块）的数量之比。比值越大，该电路就越规整。

接下来我们将讨论位于分层逻辑设计较低层的预定义和可重用模块。这些中等大小的模块在在数字设计中提供基本功能，并允许设计者在原子模块（即逻辑门）上进行大部分的设计工作。我们称这些模块为**功能模块** (functional block)，即预定义的门级互联电路。

???+ note

    大部分功能模块属于[中规模集成电路](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_5/#_2)。

## 工艺映射

**工艺映射** (technology mapping) 是将逻辑图或网表转化成可以用工艺实现的新的图或网表的过程。

正如我们在第二章提到的，与非门和或非门都是[通用门](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_2/#_3)。而在线代晶体管技术中，与非门和或非门较与门和或门的性能也更好。因此我们将讨论如何将逻辑电路转化为仅有与非门（或或非门）与反相器实现的逻辑电路。

给定一个已经优化的，有与门、或门和反相器组成的电路，可以通过如下步骤将其变成由与非门（或或非门）组成的电路：

1. 用与非门（或或非门）和反相器替换原电路中的与门和或门，形成新的等效电路。
2. 消除所有反相器对。
3. 在不改变逻辑函数的前提下：
    1. 将能够前置的反相器置于逻辑门前。
    2. 用一个反相器替代所有并联的反相器。
    3. 重复以上两步。

下图是对以上步骤的可视化呈现：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_1.png" width="70%" style="margin: 0 auto;">
</div>

某种工艺映射的结果与原始电路或映射前的方程形式有关。例如，输出为或门的电路在与非门映射下会得到与非门，在或非门映射下会得到被或非门驱动的反相器。

鉴于这些差异的存在，积之和式更适于使用与非门；和之积式更适于使用或非门，以消去输出端的反相器。

## 基本逻辑函数

基本逻辑函数包括定值、传递、取反和使能。

### 定值、传递和取反

这三种逻辑函数都是单变量函数，其真值表如下：

|$X$|$F = 0$|$F = X$|$F = \overline{X}$|$F = 1$|
|:-:|:-:|:-:|:-:|:-:|
|0|0|0|1|1|
|0|0|1|0|1|

在表中，$F = 0$ 和 $F = 1$ 为**定值** (value fixing) 操作；$F = X$ 为**传递** (transferring)；$F = \overline{X}$ 为**取反** (inverting) 操作。

这四个函数的实现方式如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_2.png" width="70%" style="margin: 0 auto;">
</div>

对于正逻辑，习惯用电气接地符号表示常数 $0$，用电源电压符号表示常数 $1$，一般用 $V_{\text{CC}}$ 或 $V_{\text{DD}}$ 表示。传递用连接 $X$ 和 $F$ 的线表示。取反用反相器表示。

### 使能

一般地，**使能** (enable) 允许信号从输入传播到输出。非使能可以用高阻态、固定输出值 $0$ 或 $1$ 来代替输入信号。这个附加的输入信号通常记为 ENABLE 或 EN，用以决定输出是否被使能。

我们一般这样实现电路中的使能：

- 若非使能值为 $0$，则将输入与 EN 信号通过与门再输出
- 若非使能值为 $1$，则将输入与取反的 EN 信号通过或门再输出

两种情况分别对应下面两图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_3.png" width="70%" style="margin: 0 auto;">
</div>

## 译码

一种 $n$ 位二进制码可以表示 $2^{n}$ 个不同的编码信息。**译码** (decode) 是将一个 $n$ 位的输入码转换成一个 $m$ 位的输出码，其中 $n \leq m \leq 2^{n}$，以保证每一个有效的输入码都产生唯一的输出码。

实现译码功能的组合电路称作**译码器** (decoder)，具体地，对于一个 $n$ 输入 $m$ 输出的译码器，记为 $n$ - $m$ 译码器。

### $n$-$2^{n}$ 译码器

接下来我们讨论将 $n$ 位二进制数译码为 $2^{n}$ 位独热码的 $n$-$2^{n}$ 译码器的实现。

#### 1-2 译码器

1-2 译码器的实现是简单的，只需将输出独热码的两位分别对应原本的输入信号和取反后的输入信号即可。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_4.png" width="70%" style="margin: 0 auto;">
</div>

#### 2-4 译码器

从这里开始，更大规模的译码器便是由较小规模的译码器组合实现的了。2-4 译码器只需将两个 1-2 译码器相连即可。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_5.png" width="70%" style="margin: 0 auto;">
</div>

#### 3-8 译码器

沿用先前的思路，3-8 译码器只需将一个 1-2 译码器和一个 2-4 译码器相连即可。

但这里我们要进一步考虑一个问题。我们知道译码器的每一个输出可以看作是一个输入的最小项，自然地，随着译码器规模的增大，用于计算最小项的与门也就越多。

如果我们仍然简单增加与门的输入个数，不仅电路的门输入成本增加太快，还会由于门的[扇入限制](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_5/#_4)而无法实现过大的译码器。

此时我们可以应用分级的思想来构建电路，这样门输入成本的增加就相对较慢，且在相同的扇入限制下能实现更大规模的译码器。其具体实现如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_6.png" width="70%" style="margin: 0 auto;">
</div>

#### 任意的 $n$-$2^{n}$ 译码器

按照这样的思路，任意的 $n$-$2^{n}$ 译码器都可以由两个译码器驱动：

- 若 $n$ 为偶数，则两个译码器都有 $2^{k - 1}$ 个输出
- 若 $n$ 为奇数，则两个译码器分别有 $2^{\frac{k + 1}{2}}$ 个和 $2^{\frac{k - 1}{2}}$ 个输出

按照这一方法递归地分级实现译码器，直到使用 1 - 2 译码器为止。

### 带使能的译码器

带使能的译码器可以通过再译码器的输出端连接 $m$ 个使能电路来实现。

> 带使能的 2-4 译码器实现如下：
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_7.png" width="70%" style="margin: 0 auto;">
> </div>

需要说明的是，对于大规模的译码器，往往将使能电路放置在译码器的输入端及其反向端，而非每个译码器的输出端。这样做有助于减少门输入成本。

### 基于译码器的组合电路

一个 $n$ 输入变量的译码器可以产生 $2^{n}$ 个最小项。因为任何布尔函数都可以由最小项之和表示，所以可以使用一个译码器来产生这些最小项，并由一个额外的或门来实现最小项之和。按照这种方法，任何 $n$ 输入 $m$ 输出的组合电路都可以用 1 个 $n$-$2^{n}$ 译码器和 $m$ 个或门实现。

## 编码

**编码** (encode) 是译码的逆操作，实现这一功能的组合电路称作**编码器** (encoder)，其接受输入并输出相对应的二进制码。

### 优先编码器

在介绍优先编码器之前，我们先按照前述的 2-$2^{n}$ 译码器，设想一下其相对应的 $2^{n}$-2 编码器。不难想见，这一译码器有大量的无关项。这会造成一个问题，即一旦有多于一个输入为 `1` 时，输出就没有意义。

为此，我们采用优先编码器，即可以实现优先级函数的组合电路。具体地，当多于一个的输入为 `1` 时，优先级最高的输入将被优先处理。这样的实现不仅解决了问题，还很大程度上简化了真值表的复杂程度。我们以四输入优先级编码器为例，其真值表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_8.png" width="70%" style="margin: 0 auto;">
</div>

可见，这一真值表中的一行可以替代原真值表中的 $2^{p}$ 行，$p$ 是行中 $\times$ 的个数。我们据此真值表写出最小项之和，并利用卡诺图化简后，就可以设计出四输入优先编码器的电路。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_9.png" width="70%" style="margin: 0 auto;">
</div>

## 选择

在介绍完译码和编码这一对功能的逻辑电路后，我们接下来关注选择和分离这一对功能的逻辑电路。

在计算机中，对信息进行**选择** (selection) 是一个非常重要的功能，执行选择的电路通常由一组供选择的输入、一个单独的输入和一组决定选择的控制输入组成。

### 多路复用器

用于从多个输入中选择一个输入，并将信息传输到的输出的组合电路称作**多路复用器** (multiplexer, MUX)。具体的选择由一组输入变量控制，这些变量被称作**选择输入** (selection input)。多路复用器也称作**数据选择器** (data selector)，因为它从多个信息输入中选择一个，并将这个二进制信息传递到输出。

通常，有 $2^{n}$ 个待选择输入和 $n$ 个选择输入，选择输入的位组合决定选择哪个输入。

#### 2-1 多路复用器

最基本的多路复用器即为 2-1 多路复用器，其有 2 个信息输入 $I_{0}, I_{1}$，1 个选择输入 $S$ 和输出 $Y$。其真值表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_11.png" width="70%" style="margin: 0 auto;">
</div>

不难得到对应的表达式为 $Y = \overline{S} I_{0} + S \overline{I_{1}}$。

于是我们可以构建对应的电路：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_12.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，多路复用器可以分为译码器和使能电路两部分，这一结构会在更大规模的多路复用器中再次出现。另外，我们常将这一个多路复用器以右图的形式表示。

#### 4-1 多路复用器

从 2-1 多路复用器出发推广，一个 4-1 多路复用器应当有 4 个信息输入 $I_{0}, I_{1}, I_{2}, I_{3}$，2 个选择输入 $S_{0}, S_{1}$ 和输出 $Y$。我们可以用紧凑真值表来表示其功能：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_13.png" width="70%" style="margin: 0 auto;">
</div>

对应的表达式为 $Y = (\overline{S_{1}} \overline{S_{0}}) I_{0} + (\overline{S_{1}} S_{0}) I_{1} + (S_{1} \overline{S_{0}}) I_{2} + (S_{1} S_{0}) I_{3}$。

注意到这里我们采用了存在括号改变了运算顺序的形式，而非不含括号的最简积之和的形式。这样做虽然导致了门输入成本的上升，但却带来了结构更加规整和具有规律性的电路：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_14.png" width="70%" style="margin: 0 auto;">
</div>

可以看到，与 2-1 多路复用器一致，4-1 多路复用器也可以分为译码器和使能电路两部分。据此，我们可以继承这一结构扩展至更多输入位数的多路复用器。

### 基于多路复用器的组合电路

由前所述，将一个译码器和一个 $m \times 2$ 与或门组合在一起，就可以实现一个多路复用器。具体来说，译码器产生选择输入的最小项，与或门提供使能电路以判断最小项是否传递到或门。使能用信号输入 $I_{i}$ 作为使能信息，当 $I_{i} = 1$，最小项 $m_{i}$ 就传递到或门；当 $I_{i} = 0$，最小项 $m_{i}$ 就用 $0$ 代替。

因此，只需要将 $I$ 输入固定，就可以用一个有 $n$ 个选择输入、$2^{n}$ 个数据输入的多路复用器来实现一个有 $n$ 个变量的布尔函数。进一步来说，一个 $m$ 位输出函数可以通过将一个 $m$ 位多路复用器的 $m$ 位信息向量的值固定来实现。

## 分配

**分配** (distribution) 是选择的逆操作，实现这一功能的组合电路称作**多路分配器** (demultiplexer)，其由 $n$ 个选择输入的组合控制，将 1 个输入信息传送到 $2^{n}$ 个输出。

### 多路分配器实现

事实上，一种常见的多路分配器的实现方式就是采用带使能的译码器。让我们先重新考察前文提到的带使能的 2-4 译码器：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_10.png" width="70%" style="margin: 0 auto;">
</div>

前文中，我们主要关注这一电路的译码功能，因此考察的是在不同使能下译码的变化，即固定 $A_{0}$ 和 $A_{1}$，改变 EN。

但是，如果我们固定 EN，改变 $A_{0}$ 和 $A_{1}$，我们就实现了通过改变 2 个选择输入 $A_{0}, A_{1}$，将 1 个输入信息 EN 传送到 4 个输出。这正是我们期望多路分配器所实现的功能！

因此，多路分配器与带使能的译码器的电路实质上是一致的。

## 迭代组合电路

接下来我们将讨论算术功能模块。由于算术规则的一致性，对每一位的运算处理往往是相同的，因此完整的算术功能模块需要若干功能相同的子功能块。这些子功能块称作**单元** (cell)，整个模块的实现是一个**单元阵列** (array of cell)，也称**迭代阵列** (iterative array)。

概念的介绍总是抽象的，希望读者能对这些内容稍加记忆，在之后的实例中进一步理解。

## 二进制加法器

我们从最基本的算术电路，即二进制加法器开始介绍。

从最底层开始设计，即设计一个电路实现两个一位二进制数相加。容易想到这一运算的结果需要两位表示：进位与和，其中进位将加到下一个高位的有效位中。

因此，有两个基本的算术模块：

- **半加器** (half adder)：实现两位相加的组合电路
- **全加器** (full adder)：实现三个位（两个有效位和一个先前位产生的进位）相加的电路

### 半加器

半加器的实现是简单的。用 $X$ 和 $Y$ 表示两个输入，用 $S$（和）和 $C$（进位）表示两个输出。容易得到：

- $S = X \overline{Y} + \overline{X} Y = X \oplus Y$
- $C = X Y$

### 全加器

全加器可以由两个半加器实现（这也是其得名的原因）。我们用 $X$ 和 $Y$ 表示两个有效位输入，$Z$ 表示进位输入，输出 $S$ 和 $C$ 保持不变。可得：

- $S = X \overline{Y} \overline{Z} + \overline{X} Y \overline{Z} + \overline{X} \overline{Y} Z + X Y Z = X \oplus Y \oplus Z$
- $C = X Y + X Z + Y Z$

在电路实现中，我们常将表达式变形为 $S = (X \oplus Y) \oplus Z, C = X Y + Z (X \oplus Y)$，其中 $X Y$ 称作**进位生成** (carry generate)，$X \oplus Y$ 称作**进位传播** (carry propagate)，这样做的原因将在后文指出。于是全加器可以用下图中的电路实现：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_15.png" width="70%" style="margin: 0 auto;">
</div>

### 二进制行波进位加法器

一个并行加法器是一个仅采用组合逻辑计算出两个二进制数算术和的数字电路。其并行地连接 $n$ 个全加器，所有输入为同时加载至全加器以产生和。

并行加法器中的所有全加器用级联的方式来连接在一起，一个全加器的进位输出连接到下一个全加器的进位输入。由于加法器最低有效位产生的进位 `1` 可能经过多个全加器传递到最高有效位，就像一个小卵石丢入池塘激起的波浪一样，因此这种并行加法器又称作**行波进位加法器** (ripple carry adder)。

下图给出了由 4 个全加器级联形成的一个 4 位行波进位加法器：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_16.png" width="70%" style="margin: 0 auto;">
</div>

### 超前进位加法器

回顾全加器的进位传播和进位生成，如果我们定义如下两个函数：

- **传播函数** (generate function)：$P_{i} = A_{i} \oplus B_{i}$
- **生成函数** (propagate function)：$G_{i} = A_{i} B_{i}$

则 $S_{i} = P_{i} \oplus C_{i}, C_{i + 1} = G_{i} + P_{i} C_{i}$。

在行波加法器中，计算 $S_{i}, C_{i + 1}$ 必须等待 $C_{i}$ 计算完成，因此行波加法器的延迟和其位数线性相关。

为了解决这一问题，我们采用的改进方案称作**超前进位加法器** (carry lookahead adder)。

具体地，我们将除 $C_{0}$ 外的 $C_{i}$ 递归地代入表达式，使得最终每个 $C_{i}$ 都可用 $P_{i}$ 和 $C_{0}$ 表示，而这几个输入都是事先给出的。于是这样就避免了计算 $C_{i + 1}$ 对 $C_{i}$ 的依赖，也就解决了线性的传播延迟问题。

具体地，我们考察 4 位超前进位加法器，其对 $C_{i}$ 的表达式变形如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_17.png" width="70%" style="margin: 0 auto;">
</div>

对应的电路实现如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_18.png" width="70%" style="margin: 0 auto;">
</div>

如图中所示，因为剥离了每个全加器中原本的进位计算部分，因为现在电路中的算术模块称作**部分全加器** (partial full adder)。

更进一步地，我们还可以使用小规模的超前进位加法器组合得到大规模的超前进位加法器。

## 二进制减法

减法相较于加法，其困难点在于结果可能为负数，而我们现在没有特别好的表示方法。如果简单地进行大小比较并分类讨论，反映在电路设计上就会特别复杂，且硬件实现中会面临延迟较大、扇入扇出的负载有限、成本较高等问题。为此，我们需要给出一种更好的表示，才能得到便捷的减法计算的方式。

### 补码

每个 $r$ 进制系统都有两种补码表示：基数**补码** (complement) 和基数反码。前者称作 $r$ 进制补码，后者称作 $(r - 1)$ 进制补码，或 $r$ 进制反码。

接下来我们侧重探讨二进制的补码和反码。

给定一个 $n$ 位的二进制数 $N$，则其二进制反码定义为 $(2^{n} - 1) - N$。从结果上来说，二进制反码即将二进制数的所有 $1$ 变为 $0$，$0$ 变为 $1$，即对原数按位取反即可。中间的数学推导交给读者自行考虑。

给定一个 $n$ 位的二进制数，其二进制补码定义为：当 $N$ 不为 $0$ 时，$N$ 的补码为 $2^{n} - N$；当 $N$ 为 $0$ 时，其补码为 $0$。虽然从定义上我们似乎需要通过分类讨论才能求出补码，但考虑在具体的 $n$ 位运算中，$2^{n} - 0$ 的二进制表示为 $(1\underbrace{0 \cdots 0}_{n\ \text{zeros}})_{2}$，故只需保留后 $n$ 位并丢弃最高位即可。

在具体实现上，我们还会采用另外两种方法来求补码：

- 在反码基础上 $+ 1$（同样忽略最高位可能的进位）
- 保留所有地位的 $0$ 和第一个 $1$ 不变，将剩下所有高位的 $1$ 变为 $0$，$0$ 变为 $1$

这两种方法的数学推导同样交给读者自行考虑。

补码还有一个优点在于，一个数的补码的补码仍为原数，这一性质容易从定义上推出。

### 采用补码的二进制减法

这里我们讨论如何用补码实现两个 $n$ 位无符号数的减法。考虑 $M - N$：

1. 被减数 $M$ 加上减数 $N$ 的补码，即 $M + (2^{n} - N) = M - N + 2^{n}$。
2. 如果 $M \geq N$，则和产生一个进位位 $2^{n}$，丢弃这一进位后，结果即为 $M - N$。
3. 如果 $M < N$，则和不产生进位，此时结果为 $2^{n} - (N - M)$，即 $N - M$ 的补码。对结果求补并添上负号即得到 $- (N - M)$。

> 举例，给定二进制数 $X = 1010100, Y - 1000011$，财通二进制补码计算 $X - Y$ 和 $Y - X$。
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_19.png" width="70%" style="margin: 0 auto;">
> </div>

## 二进制加减法器

### 无符号二进制加减法器

通过前文的讨论，我们可以得到一种更加便捷的，同时实现无符号二进制数加法和减法运算的方法。即只在一个加法器中，根据运算的需要输入数据本身或其补码，并对最终结果作出修正即可。一个 4 位的加减法器如下所示：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_20.png" width="70%" style="margin: 0 auto;">
</div>

### 有符号二进制数

接下来，我们将进一步使用补码，将这一方法推广到有符号数。

要计算有符号数，首先就需要一种表示符号的方法。习惯上，我们在 $n$ 位数字的最高有效位前增加一位表示符号，并约定用 $0$ 表示正数，$1$ 表示负数。这种表示方法称作**符号-数值** (signed-magnitude) 表示法。但容易意识到，这种表示方法仍然需要分类讨论和对结果的修正。因此我们再给出另一种改进的表示方法。

我们仍然用符号-数值表示法表示正数，但使用**符号-补码** (signed-complement) 表示法来表示负数。为了直观地让读者感受到这两种表示方式，我们给出列举所有能用 4 位编码表示的有符号二进制数。

|十进制|符号-数值|符号-补码|
|:-:|:-:|:-:|
|7|`0111`|`0111`|
|6|`0110`|`0110`|
|5|`0101`|`0101`|
|4|`0100`|`0100`|
|3|`0011`|`0011`|
|2|`0010`|`0010`|
|1|`0001`|`0001`|
|0|`0000`|`0000`|
|-0|`1000`|-|
|-1|`1001`|`1111`|
|-2|`1010`|`1110`|
|-3|`1011`|`1101`|
|-4|`1100`|`1100`|
|-5|`1101`|`1011`|
|-6|`1110`|`1010`|
|-7|`1111`|`1001`|
|-8|-|`1000`|

通过这个例子，我们可以发现如下几个性质：

- 用 $n$ 位编码时，符号-数值表示法可以表示 $2^{n - 1} - 1$ 个正数、$2^{n - 1} - 1$ 个负数、$2$ 个有符号的 0；符号-补码表示法可以表示 $2^{n - 1} - 1$ 个正数、$2^{n - 1}$ 个负数、$1$ 个无符号的 0
- 在符号-补码表示法中，一个数的相反数即为按位取反再 $+ 1$

### 有符号二进制数加减法

符号-补码表示法在实现有符号数的加法和减法中有相当的优越性。我们接下来讨论在符号-补码表示法下如何实现加法和减法。

对于加法，只需要将两个二进制数连带符号位一起做加法，并丢弃符号位处产生的进位即可。

> 举例来说：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_21.png" width="70%" style="margin: 0 auto;">
> </div>

对于减法，只需要将减一个数转化为加这个数的相反数。求相反数的方法已在前文给出，即按位取反再 $+ 1$ 即可。

> 举例来说：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_22.png" width="70%" style="margin: 0 auto;">
> </div>

### 溢出

为了得到加减法运算的正确结果，我们必须确保有足够多的位来存放结果。如果两个 $n$ 位数产生的结果需要 $n + 1$ 位保存，那我们称发生了**溢出** (overflow)。

溢出的检测可以用过观察符号位的进位输入（即 $C_{n - 1}$）和符号位的进位输出（即 $C_{n}$）来判定。如果这两个值不相等（即 $C_{n - 1} \oplus C_{n} = 1$），则表明发生了溢出。

需要注意的是，溢出不仅会在加减法运算的过程中发生，对绝对值最大的负数取补时也会发生溢出。

???+ note

    事实上，如果考虑带余运算，溢出得到的结果可以看作是对结果取余后的结果。即将 $-2^{n - 1}$ 至 $2^{n - 1} - 1$ 周期延拓至全部数后再进行加减法运算得到的结果。

## 其它算术功能模块

除了基本的四则运算，诸如递增、递减、大小比较等算术功能也很重要。这些功能虽然也可以用基本的运算单元实现，但我们接下来将讨论一种更简便高效的实现方式，即对基本功能块进行压缩。压缩技术是从一个基本电路（如二进制加法器）出发，通过将已有的电路转换为有用的、较简单的电路来简化设计，从而避免这届设计电路本身。

### 压缩

对于已经设计好的功能块，通过将其输入端的值固定、传递和取反，即可实现新的功能。针对特定应用将已有电路简化成一个简单电路，我们成这个过程为**压缩** (contraction)。压缩的目的是采用以前的设计结果来完成逻辑电路或功能模块的设计。

### 递增

**递增** (incrementing) 意味着对一个算术变量加一个固定的值，通常这个固定值为 $1$。一个 $n$ 位**递增器** (incrementer) 执行 $A + 1$ 操作，它可以由一个执行 $A + B$ 且 $B = 0 \cdots 01$ 的二进制加法器实现。

在具体的电路实现中，由于对 $B$ 的固定，电路的大部分可以得到简化。以 3 位递增器为例：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_23.png" width="70%" style="margin: 0 auto;">
</div>

可见，由 3 位加法器压缩得到的 3 位递增器可以在原电路的基础上高度简化，但同时保证了电路设计的简便性。

### 递减

与递增类似，**递减** (decrementing) 意味着对一个算术变量加一个固定的负值，通常这个固定值为 $-1$。其设计方式与递增是类似的，只需在加法器中固定 $B$ 的值为 $-1$（二进制补码下为 $11 \cdots 1$）即可。

### 常数乘法

常数乘法依赖于对被乘常数的二进制位数分解与左移实现。可以意识到，乘以任何一个二进制下形如 $10 \cdots 00$ 的数，都等价于将原数左移若干位。因此只需将乘数分别左移被乘常数中为 $1$ 的位对应的位数并全部相加，即可得到正确的结果。

### 常数除法

事实上，由于进制转换的不精确性，除法是几种运算中相对难以精确实现的运算。为此，我们只限于讨论除以 $2$ 的幂次方，容易意识到这对应将原数右移若干位。

### 零填充与符号扩展

在常数乘法和除法中，一个重要的操作是左移和右移。因此我们需要引入一个重要的操作，**零填充** (zero fill)。零填充指在一个操作数的左边或右边添加若干个 $0$，用以实现数的左移或们组电路输入引脚的要求。

**符号扩展** (sign extension) 则是用于增加用补码表示的有符号数的位数，即将数的符号位向左扩展。

> 例如，将 $0110 1011$ 扩展为 $0000 0000 0110 1011$，将 $1001 0101$ 扩展为 $1111 1111 1001 0101$。

符号扩展的用途在于保护有符号数的补码表示，以避免其在左移或右移操作时符号位发生错误的改变。
