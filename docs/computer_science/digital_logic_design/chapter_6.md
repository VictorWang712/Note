---
comments: true
---

# 第六章 - 寄存器与寄存器传输

在数字系统中，数据通路和控制单元通常在设计的较高层次上出现。**数据通路** (datapath) 包括数据处理逻辑和一组用于执行数据处理的寄存器。**控制单元** (control unit) 由一些逻辑单元构成，它决定着数据通路处理数据过程中各种操作的顺序。

寄存器传输记号描述了基本数据处理行为，也称作**微操作** (microoperation)。寄存器传输 (register transfer) 是指在寄存器之间、寄存器与存储器之间以及用过数据处理逻辑传输信息，由专门的传输硬件和称作**总线** (bus) 的共享传输硬件一起实现。

## 寄存器与加载使能

一个寄存器包含一组触发器，由于每一个触发器可以保存一位信息，因此由 $n$ 个触发器组成的 $n$ 位寄存器就可以保存 $n$ 位的二进制信息。一般而言，寄存器是指一组用于完成特定数据处理任务的触发器以及附加的组合门电路。其中，触发器用于锁存数据，而门电路则用于决定输入触发器的数据是还是经过转换的。

**计数器** (counter) 是指在时钟脉冲的激励下，能遍历预先规定好的状态序列的一种寄存器。计数器中按某种方式连接起来的逻辑门使得计数器能够生成规定顺序的二进制状态序列。

???+ note

    尽管计数器也算是一种特殊类型的寄存器，但一般而言，我们将其和寄存器区别对待。

将新信息传送至寄存器称作寄存器的**加载** (loading) 操作。如果寄存器中所有位都是在公用时钟脉冲下同时加载的，那么我们称这种加载为并行加载。

我们以下图中的 4 位寄存器为例：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_1.png" width="70%" style="margin: 0 auto;">
</div>

这个 4 位寄存器仅包含 4 个 D 触发器，没有额外的门电路。公用的 Clock 信号在每个脉冲的上升沿触发所有的触发器，此时二进制数据经过 4 个 $D$ 输入端存入 4 位寄存器中，4 个 $Q$ 输出端输出存在寄存器中的二进制数据。Clear 信号则用于异步地将寄存器清零。

### 并行加载寄存器

一般来说，时钟脉冲会经过所有的寄存器。但多数时候我们不希望所有寄存器的内容，在每一个时钟脉冲下都改变，因此一个常用的方法是阻止时钟到达寄存器的时钟输入端。

具体来说，我们用一个单独的控制信号 Load 来控制时钟脉冲对寄存器有影响的时钟周期，当不希望寄存器的内容改变时，就阻止时钟脉冲到达寄存器。在前文的 4 位寄存器中，就满足表达式

$$C\ \text{Imput} = \overline{\text{Load}} + \text{Clock}$$

为了使电路正常工作，Load 必须在 Clock 为 $0$ 期间稳定在正确值 $0$ 或 $1$。一种实现方法是使 Load 信号来自于时钟上升沿触发的触发器，系统中所有触发器都用时钟上升沿来触发。由于使在寄存器 $C$ 输入利用逻辑门来控制始终开关，因此这种技术称作**门控时钟** (clock gating)。

在时钟脉冲路径上通常存在其它门，这会导致在带有门控时钟和不带有门控时钟的触发器的 Clock 和输入之间产生不同的传输延时。如果时钟信号到达不同触发器或寄存器的时间不同，就会存在**时钟偏移** (clock skew)。但是为了得到一个真正的同步系统，必须保证所有时钟脉冲同时到达，以保证所有触发器能同时触发。

一个带并行加载的 4 位寄存器如下所示：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_2.png" width="70%" style="margin: 0 auto;">
</div>

可见，我们利用带有使能的 D 触发器，实现了「加载」这一功能。同时在这个电路中，所有触发器都是在同一个时钟的上升沿实现了数据从输入到寄存器的传输，这样做避免了时钟偏差，是优于传统的门控时钟方法的。

## 寄存器传输

在大多数数字系统设计中，我们将系统划分为两种模块：**数据通路** (datapath) 和**控制单元** (control unit)，前者完成数据处理操作，后者决定这些操作的执行顺序。它们间的基本关系如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_3.png" width="70%" style="margin: 0 auto;">
</div>

其中，**控制信号** (control signal) 是二进制信号，用于激活各种各样的数据处理操作。为使这些操作按照顺序执行，控制单元传送正确的控制信号序列给数据通路。桶式控制单元接受来自数据通路的状态信息，这些状态信息描述了数据通路当前状态的各个方面，控制单元用状态信息来决定下一步执行的操作。

数据通路由一组寄存器以及对寄存器中所存储的二进制数的操作所定义。寄存器操作包括数据的装载、清除、移位和基数。寄存器是数字系统的基本单元。对寄存器中存储的数据进行移动和处理定义为**寄存器传输操作** (register transfer operation)。

一个寄存器可以完成一个或多个**基本操作** (elementary operation)，比如加载、计数、加法、减法和移位。对寄存器存储数据执行的基本操作称为**微操作** (microoperation)。

## 寄存器传输操作

我们先给出通常的记号。一般地，用大写字母（有时也带数字）来表示寄存器的功能，例如 $AR$ 表示地址寄存器、$PC$ 表示程序计数器。$n$ 位寄存器中的单个触发器通常从 $0$ 到 $n - 1$ 进行编号，从最低位 $0$ 位向最高位递增。$0$ 位位于最右端的编号称作**小端** (little-endian) 格式存储；反之 $0$ 位位于最左端的编号称作**大端** (big-endian) 格式存储。寄存器的框图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_4.png" width="70%" style="margin: 0 auto;">
</div>

将数据从一个寄存器传输到另一个寄存器用符号 $\gets$ 表示。语句 $R2 \gets R1$ 表示将寄存器 $R1$ 的内容传输到寄存器 $R2$，此时称 $R1$ 为**源** (source) 寄存器，$R2$ 为**目的** (destination) 寄存器。传输的结果只会改变目的寄存器 $R2$ 的内容，而不会改变源寄存器 $R1$ 的内容。

对于有条件的的寄存器传输操作，可以用 if-then 形式的条件语句进行定义，其一般形式为 $\text{if } (K_{1} = 1) \text{ then } (R2 \gets R1)$，此时称 $K_{1}$ 为控制单元产生的控制信号。上述语句也可以简写为 $K_{1}: R2 \gets R1$，表示只有当 $K_{1} = 1$ 时传输操作才会被执行。

我们假设所有的传输操作都出现在时钟发生跳变的情况下，也就是说尽管控制条件可能在两次时钟发生跳变间就被激活，但实际的传输操作是在触发器被时钟的下一个上升沿才发生的。

我们给出全部寄存器传输使用的基本符号：

|符号|含义|示例|
|:-:|:-:|:-:|
|字母（可带有数字）|代表一个寄存器|$AR, R2, DR, IR$|
|圆括号|代表寄存器的一部分|$R2(1), R2(7:0), AR(L)$|
|箭头|代表数据的传输|$R1 \gets R2$|
|逗号|隔开同时进行的传输操作|$R1 \gets R2, R2 \gets R1$|
|方括号|定义存储器的地址|$DR \gets M[AR]$|

## 微操作

微操作是指对寄存器或存储器中的数据进行基本的操作。数字系统中常见的微操作可分为 4 种类型：

1. 传输微操作：将二进制数据从一个寄存器传输到另一个寄存器
2. 算术微操作：对寄存器中的数据进行算术操作
3. 逻辑微操作：对寄存器中的数据进行位操作
4. 移位微操作：对寄存器中的数据进行移位

???+ note

    一个位操作可能不只属于一种微操作类型，例如，求反操作既是算术微操作，也是逻辑微操作。

### 算数微操作

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_5.png" width="70%" style="margin: 0 auto;">
</div>

可以注意到，我们没有直接定义减法运算的微操作，而是用加补码的方式定义减法运算。

### 逻辑微操作

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_6.png" width="70%" style="margin: 0 auto;">
</div>

### 移位微操作

移位微操作用于数据的横向移动。源寄存器的内容可以向右或向左移位，**左移** (left shift) 是向高位移位，**右移** (right shift) 是向低位移位。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_7.png" width="70%" style="margin: 0 auto;">
</div>

## 对单个寄存器的微操作

由于一个存储单元与微操作联系紧密，我们将实现微操作的组合逻辑当作寄存器的一部分，称作寄存器**专用逻辑** (dedicatedd logic)。而针对目的寄存器组来实现微操作的组合逻辑称作**共享逻辑** (shared logic)。

### 基于多路复用器的传输

在某些电路中，寄存器能够在不同时刻接受来自两个甚至多个不同源的数据。此时我们一般用 if-then-else 这样的条件语句进行表示，例如：

$$\text{if } (K_{1} = 1) \text{ then } (R0 \leftarrow R1) \text{ else if } (K_{2}) = 1 \text{ then } (R0 \leftarrow R2)$$

这等价于

$$K_{1}: R0 \leftarrow R1, \overline{K_{1}} K_{2}: R0 \leftarrow R2$$

这一传输一般使用多路复用器实现，其对应的电路框图为：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_6_8.png" width="70%" style="margin: 0 auto;">
</div>

显然这样的设计可以扩展到具有 $n$ 个源的多路复用器。


