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

因此，只需要将 $I$ 输入固定，就可以用一个有 $n$ 个选择输入、$w^{n}$ 个数据输入的多路复用器来实现一个有 $n$ 个变量的布尔函数。进一步来说，一个 $m$ 位输出函数可以通过将一个 $m$ 位多路复用器的 $m$ 位信息向量的值固定来实现。

## 分配

**分配** (distribution) 是选择的逆操作，实现这一功能的组合电路称作**多路分配器** (demultiplexer)，其由 $n$ 个选择输入的组合控制，将 1 个输入信息传送到 $2^{n}$ 个输出。

事实上，一种常见的多路分配器的实现方式就是采用带使能的译码器。让我们先重新考察前文提到的带使能的 2-4 译码器：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_3_10.png" width="70%" style="margin: 0 auto;">
</div>

前文中，我们主要关注这一电路的译码功能，因此考察的是在不同使能下译码的变化，即固定 $A_{0}$ 和 $A_{1}$，改变 EN。

但是，如果我们固定 EN，改变 $A_{0}$ 和 $A_{1}$，我们就实现了通过改变 2 个选择输入 $A_{0}, A_{1}$，将 1 个输入信息 EN 传送到 4 个输出。这正是我们期望多路分配器所实现的功能！

因此，多路分配器与带使能的译码器的电路实质上是一致的。
