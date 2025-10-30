---
comments: true
---

# 第四章 - 处理器

本章将概括地介绍实现处理器所要用到的原理和技术。首先从一个高度抽象和简化的概述开始，之后以此为基础为 RISC-V 指令系统构建数据通路，并设计一种简单的、能够实现指令系统的处理器。之后，我们将探讨更接近实际情况的流水线 RISC-V。

## 一种基本的 RISC-V 实现

我们将实现 RISC-V 的一个核心子集：

- 存储器访问指令 load doubleword (`ld`) 和 store doubleword (`sd`)
- 算术逻辑指令 `add`、`sub`、`and` 和 `or`
- 条件分支指令 branch if equal (`beq`)

这个子集说明了简历数据通路和设计控制的关键原理，其余指令的实现也与这个子集类似。

对于这三类指令，其实现每条指令的前几个步骤是类似的：

1. 程序计数器（PC）发送到指令所在的存储单元，并从中取出指令。
2. 根据指令的某些字段选择要读取的 1 个或 2 个寄存器。
3. 使用算术逻辑单元（ALU）：存储器访问指令用 ALU 进行地址计算，算术逻辑指令用 ALU 执行运算，条件分支指令用 ALU 进行比较。

但在经过 ALU 后，完成各类指令所需的操作就不同了。存储器访问指令需要访问存储器以读取数据或存储数据，算术逻辑指令或载入指令需要将来自 ALU 或存储器的数据写回寄存器，条件分支指令需要很具比较结果更改下一条指令的地址（否则下一条指令的地址通过 PC 加 $4$ 来获得）。

在这个过程中，许多地方会存在两个来自不同源的数据流向同一个单元。此时就涉及到数据的选择，我们使用**多选器** (multipleor)，或称**数据选择器** 来完成。此外，一些功能单元的控制依赖于当前执行的指令类型。因此我们还需要引入**控制单元** (functional unit) 来确定如何设置控制线。

基于以上分析，我们可以得到这样的一个抽象的实现图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_1.png" width="70%" style="margin: 0 auto;">
</div>

在后续内容中，我们能将基于这个实现图继续改进并补充细节，并通过添加时序控制使得处理器可以有序运行指令。

## 逻辑设计的一般方法

RISC-V 实现中的数据通路包含两种不同类型的逻辑单元：处理数据值的单元和存储状态的单元。处理数据值的单元是**组合逻辑** (combinational logic)，它们的输出仅依赖于当前输入。设计中的其它单元不是组合逻辑，而是包含**状态** (state) 的。如果一个单元有内部存储功能，它就包含状态，称其为**状态单元** (state elements)。这些逻辑部件也被称作**时序** (sequential) 的，因为其输出取决于输入和内部状态。

### 时钟同步方法

**时钟同步方法** (clocking methodology) 规定了信号可以读出和写入的时间。为简单起见，假定我们采用**边沿触发的时钟** (edge-triggered clocking)，即存储在时序逻辑单元中的所有值仅在时钟边沿更新。如果状态单元在每个有效时钟边沿都进行写入，则可忽略写**控制信号** (control signal)。更进一步地，我们规定仅在时钟上升沿写入。

我们将用术语**有效** (asserted) 表示信号为逻辑高，用**使有效** (assert) 表示信号应为逻辑高，用**无效** (deasserted) 或**使无效** (deassert) 表示信号为逻辑低。

???+ note

    这样规定是因为在进行硬件实现时，数字 $1$ 有时表示逻辑高，又是表示逻辑低。

## 建立数据通路

设计数据通路的合理方法是，先分析每类 RISC-V 指令需要哪些主要执行单元。本节首先讨论每条指令需要哪些**数据通路单元** (datapath element)，然后逐渐降低抽象的层次。在设计数据通路单元的同时，也会设计它们的控制信号。

### 各指令所需的数据通路单元

下图是三个核心的单元：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_2.png" width="70%" style="margin: 0 auto;">
</div>

首先是存储单元，用于存储程序的指令，并根据给定地址提供指令。然后是程序计数器（PC），用于保存当前指令的地址。最后还需要一个加法器来增加 PC 的值以获得下一条指令的地址，在实际情况中，这一单元通常使用 ALU，并将控制信号常设为加法来实现。

要执行任意一条指令，首先要从存储器中取出指令。为准备执行下一条指令，必须增加程序计数器的值，使其指向下一条指令。这一操作的数据通路如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_3.png" width="70%" style="margin: 0 auto;">
</div>

现在考虑 R 型指令或算术逻辑指令。这类指令读两个寄存器，对它们的内容执行 ALU 操作，再将结果写回寄存器。这些指令包括 `add`、`sub`、`and` 和 `or` 指令。

处理器的 32 个通用寄存器位于结构**寄存器堆** (register file) 中。寄存器堆是寄存器的集合，其中的寄存器可以通过指定相应的寄存器号来进行读写。寄存器堆包含了计算机的寄存器状态。另外，还需要一个 ALU 对从寄存器读出的值进行运算。

由于 R 型指令有 3 个寄存器操作数，每条指令需要从寄存器堆中读出两个数据字，再写入一个数据字。为读出一个数据字，需要一个输入指定要读的存储器号，以及一个从寄存器堆读出的输出。为写入一个数据字，寄存器堆需要两个输入，一个输入指定要写的寄存器号，另一个提供要写入寄存器的数据。其对应的硬件单元如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_4.png" width="70%" style="margin: 0 auto;">
</div>

下面考虑 RISC-V 的存取指令，其一般形式为 `ld x1, offset(x2)` 和 `sd x1, offset(x2)`。这类指令通过将基址寄存器 `x2` 与指令中包含的 12 位有符号偏移量相加，得到存储器地址。对于存储指令，从寄存器 `x1` 中读出要存储的数据；如果是载入指令，那么从存储器中读出的数据要写入指定的寄存器 `x1` 中。

因此为实现存取指令，除了前述的寄存器堆和 ALU 外，还需要一个单元将指令中的 12 位偏移量**符号扩展** (sign-extend) 为 64 位有符号数，以及一个执行读写操作的数据存储单元。数据存储单元在存储指令时被写入，所以它有读写控制信号、地址输入和写入存储器的数据输入。下图给出了这两个单元：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_5.png" width="70%" style="margin: 0 auto;">
</div>

`beq` 指令有 3 个操作数，其中两个寄存器用于比较是否相等，另一个是 12 位偏移量，用于计算相对于分支指令所在地址的**分支目标地址** (branch target address)。其指令格式是 `beq x1, x2, offset`。为实现 `beq` 指令，需将 PC 值与符号扩展后的指令偏移量相加以得到分支目标地址。

???+ note

    这里我们再次提醒，基于第二章中分支指令的定义，有 2 个必须注意的细节：

    - 指令系统体系结构规定了计算分支目标地址的基址是分支指令所在地址。
    - 指令系统体系结构还说明了计算分支目标地址时，将偏移量左移 $1$ 位以表示半字为单位的偏移量，这样偏移量的有效范围就扩大到 $2$ 倍。

在计算分支目标地址的同时，必须确定是顺序执行下一条指令，还是执行分支目标地址处的指令。当分支条件为真时，分支目标地址成为新的 PC，我们就称**分支发生** (branch is taken)。如果条件不成立，如果条件不成立，自增后的 PC 成为新的 PC，此时就称**分支未发生** (branch is not taken)。

因此，分支指令的数据通路需要执行两个操作：计算分支目标地址和检测分支条件。下图即为分支指令的数据通路：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_6.png" width="70%" style="margin: 0 auto;">
</div>

### 建立一个简单的数据通路

我们已经分别讨论了几类指令需要的数据通路单元，现在可将它们组合成一个完整的数据通路并添加控制信号以完成实现。

这个最简单的数据通路在每个时钟周期执行一条指令。这意味着每条指令在执行过程中的任何数据通路单元都只能使用一次，如果需要多次使用某数据通路单元，则要将其复制多份。因此，需要一个指令存储器和一个与之分开的数据存储器。尽管还有一些功能单元需要多份，但很多功能单元可以在不同的指令流动中被共享。

为在两个不同类指令之间共享数据通路单元，需要允许一个单元有多个输入，我们用多路选择器和控制信号在多个输入中进行选择。

于是，我们可以构造存储类指令和 R 型指令的数据通路，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_7.png" width="70%" style="margin: 0 auto;">
</div>

最后，我们将前述的取指令数据通路、R 型指令和存储类指令数据通路、分支指令数据通路合并，就可以得到 RISC-V 指令系统核心集的一个简单数据通路，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_8.png" width="70%" style="margin: 0 auto;">
</div>

## 一个简单的实现方案

现在我们已经有了这个简单处理器的数据通路，我们将基于此并增加一个简单的控制单元来实现。

### ALU 控制

ALU 的控制是容易的，我们先明确其所有的控制信号：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_9.png" width="70%" style="margin: 0 auto;">
</div>

据此，我们可以采用多级译码的方式，得到控制信号的真值表：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_10.png" width="70%" style="margin: 0 auto;">
</div>

### 设计主控制单元

现在我们考虑控制的其他部分。对于主控制单元，其需要处理不同的指令，因此要能够有效「解读」指令。所以首先，我们先来回顾四类指令的格式：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_11.png" width="70%" style="margin: 0 auto;">
</div>

经过一些整理，我们可以引入 6 个控制信号：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_12.png" width="70%" style="margin: 0 auto;">
</div>

设置这些控制信号的对应的真值表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_13.png" width="70%" style="margin: 0 auto;">
</div>

于是，在我们引入了这些控制信号后，就可以得到带有控制单元的简单数据通路：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_14.png" width="70%" style="margin: 0 auto;">
</div>

### 数据通路操作

根据前述的数据通路，我们可以设计控制单元的逻辑。但在此之前，我们可以先明确，各类指令是如何使用数据通路的。

R 型指令的执行可以分为 4 个步骤：

1. 取出指令，PC 自增。
2. 从寄存器堆读出两个寄存器 `x2` 和 `x3`，同时主控制单元在此步骤计算控制信号。
3. 根据部分操作码确定 ALU 的功能，对从寄存器堆读出的数据进行操作。
4. 将 ALU 的结果写入寄存器堆中的目标寄存器 `x1`。

load 指令的执行可以分为 5 个步骤：

1. 从指令存储器中取出指令，PC 自增。
2. 从寄存器堆读出寄存器 `x2` 的值。
3. ALU 将从寄存器堆中读出的值和符号扩展后的指令中的 12 位（偏移量）相加。
4. 将 ALU 的结果用作数据存储器的地址。
5. 将从存储器读出的数据写入寄存器堆 `x1`。

branch-if-equal 指令的执行可以分为 4 个步骤：

1. 从指令存储器中取出指令，PC 自增。
2. 从寄存器堆中读出两个寄存器 `x1` 和 `x2`。
3. ALU 将从寄存器堆读出的两数相减。PC 与左移一位、符号扩展的指令中的 12 位（偏移量）相加，结果是分支目标地址。
4. ALU 的零输出决定将哪个加法器的结果写入 PC。

### 控制的结束

我们已经了解了指令如何按步骤操作，现在继续讨论控制单元的实现。控制单元的功能可以根据控制信号精确定义，其输出是控制线，输入是操作码。因此，可以根据操作码的二进制编码为每个输出建立一个真值表，如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_15.png" width="70%" style="margin: 0 auto;">
</div>

### 为什么现在不使用单周期实现

截至目前，我们已经实现了一个单周期的 RISC-V 核心集处理器。因此在进入后文对流水线处理器的探讨前，我们来简单讨论一下单周期处理器的一些问题。

尽管单周期设计可以正确工作，但是在现代设计中不采取这种方式，因为它的效率太低。究其原因，是在单周期设计中时钟周期对于每条指令必须等长。这样，处理器中的最长路径决定了时钟周期。这样即使 CPI 为 $1$，但单个时钟周期太长，实现的整体性能可能很差。

???+ note

    在多数时候，这条最长路径很可能是一条 load 指令，它连续地使用 5 个功能单元：指令存储器、寄存器堆、ALU、数据存储器和寄存器堆。

使用单周期设计的代价是显著的，但对于小指令集而言，或许是可以接受的。历史上，早期具有简单指令集的计算机确实采用这种实现方式。但是，如果要实现浮点单元或更复杂的指令集，单周期设计根本无法正常工作。

## 流水线概述

### 面向流水线的指令系统

**流水线** (pipelining) 是一种能使多条指令重叠执行的实现技术。流水线的概念是朴素的，其核心在于，流水线中每个步骤的时间并没有缩短，但流水线通过并行地执行各个步骤，提高了系统的**吞吐率** (throughput)，从而能够在单位时间内完成更多的工作。

这一原则同样可以用于处理器，即采用流水线方式执行指令。RISC-V 指令执行通常包含 5 个步骤：

1. 取指（IF）:从存储器中取出指令。
2. 译码（ID）:读寄存器并译码指令。
3. 执行（EX）:执行操作或计算地址。
4. 访存（MEM）访问数据存储器中的操作数（如有必要）。
5. 写回（WB）:将结果写入寄存器（如有必要）。

因此，接下来要探讨的 RISC-V 流水线有 5 个阶段。为了使讨论具体化，我们先建立一个流水线。之后我们考虑的是这 7 条指令：`ld`、`sd`、`add`、`sub`、`and`、`or`、`beq`。

我们先来给出这些指令在各功能单元的处理时间：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_16.png" width="70%" style="margin: 0 auto;">
</div>

基于这些数据，我们先给出一个执行指令的示例，以直观地感受非流水线和流水线执行的区别：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_17.png" width="70%" style="margin: 0 auto;">
</div>

可见，尽管在每个功能单元执行的每一步时间没有减少，但是指令的平均执行时间却从 $800 \mathrm{ps}$ 降低到了 $200 \mathrm{ps}$，即提供了 $4$ 倍的性能改进。

我们可以将这种性能加速比归纳为一个公式。如果流水线各阶段操作平巷，那么在理想条件下，流水线处理器上的指令执行时间满足

$$\text{指令执行时间}_{\text{流水线}} = \fracP{\text{指令执行时间}_{\text{非流水线}}}{\text{流水线级数}}$$

也就是说，在理想的条件和有大量指令的情况下，流水线带来的加速比约等于流水线级数。

流水线技术通过提高指令吞吐率来提高性能，而不是减少单个指令的执行时间。因此指令吞吐率是评估流水线性能的重要指标。

### 流水线冒险

那么我们现在就开始考虑真正的流水线设计中可能遇到的问题。一个容易想到的情况就是，在下一个时钟周期中下一条指令无法执行。这种情况被称作**冒险** (hazard)，具体来说有三种情况。

#### 结构冒险

第一种冒险称作**结构冒险** (structural hazard)，即硬件不支持多条指令在同一时钟周期执行。

当然，RISC-V 指令系统是面向流水线设计的，这使得设计人员在多数情况下容易避免结构冒险。唯一可能面对的情况是，硬件的数量有限导致对同一硬件的复用。但总的来说是容易处理的。

#### 数据冒险 

第二种冒险称作**数据冒险** (data hazard)，即由于一个步骤必须等待另一个步骤完成而导致的流水线停顿。

在计算机流水线中，数据冒险源于一条指令依赖于前面一条尚在流水线中的指令。在不做任何干预的情况下，数据冒险通常会严重地阻碍流水线。

一种基本的解决方案是基于一个发现，即不需要等待指令完成就可以尝试解决数据冒险。这通过向内部资源添加额外的硬件，以提前从缓冲区中取到后一步需要的数据，而不是等到前一个指令执行完毕，数据到达程序员可见的寄存器或存储器。这种方法称作**前递** (forwarding) 或**旁路** (bypassing)。

> 我们来看这样一个例子，对于以下两条指令：
>
> ```asm
> add x1, x2, x3
> sub x4, x1, x5
> ```
>
> 我们如下图这样来构造流水线：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_18.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 即将 `add` 指令 EX 阶段的输出前递到 `sub` 指令 EX 阶段的输入，替换 `sub` 指令在第二阶段读出的寄存器 `x1` 的值。

当然，尽管前递的效果很好，但是不能避免所有的流水线停顿，仅当目标阶段在时间上晚于源阶段时，前递路径才有效。这种问题通常出现在**载入-使用型数据冒险** (load-use data hazard) 中，对应于我们考察的指令就是在后一条指令中使用了前一条 `ld` 指令的载入值。因此，这种情况下流水线也不得不停顿一个阶段来应对，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_19.png" width="70%" style="margin: 0 auto;">
</div>

这张图中包含了流水线的一个重要概念，即**流水线停顿** (pipeline stall)，也通常称作**气泡** (bubble)。在之后的章节我们会详细介绍如何解决这类冒险。

#### 控制冒险

第三种冒险称作**控制冒险** (control hazard)，即一个步骤如何执行需要根据另一个步骤的执行结果，而那个步骤还未执行完毕。

容易意识到，这种问题主要出现在条件分支指令的处理上。解决这类冒险的主要方法是**预测** (prediction)，即假设一个预期结果，并按照预期结果先行流水线执行之后的步骤。如果实际的执行结果和预期不同，再重新开始执行对应的后续步骤。这样，处理器就仅在预期结果不正确的时候，才会发生停顿。

显然，这个方法的有效性取决于预测的正确性。在当下，成熟的分支预测可以预测一些条件分支指令发生跳转，而另一些不发生跳转。更进一步地，动态硬件预测其可以根据每个条件分支指令的行为进行预测，并在程序生命周期内可能改变条件分支的预测结果，并根据最近的成功预测调整下一次的预测。

这种动态预测的一种常用实现方法是保存每个条件分支是否发生分支的历史记录然后根据最近的过去行为来预测未来。在后面的章节我们将指出，当历史记录的数量和类型足够多时，动态分支预测器的正确率可以达到 $90\%$。

### 小结

流水线技术是一种在顺序指令流中开发指令间**并行性** (parallelism) 的技术。与多处理器编程相比，其优点在于它对程序员是不可见的。

在接下来，我们将开始详细地介绍，对于上述各种问题的具体技术处理方式。

## 流水线数据通路和控制

### 流水线的图形化表示

首先，我们给出两种流水线图。我们以下述指令为例进行说明：

```asm
ld x10, 40(x1)
sub x11, x2, x3
add x12, x3, x4
ld x13, 48(x1)
add 14, x5, x6
```

第一种是**多时钟周期流水线图** (multiple-clock-cycle pipeline diagram)，如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_20.png" width="70%" style="margin: 0 auto;">
</div>

其中，图形的左半边阴影表示写入，右半边阴影表示读取，全阴影表示两者皆有，无阴影表示实际上不经过该阶段。

第二种是**单时钟周期流水线图** (single-clock-cycle pipeline diagram)，下图是上述指令流程中第 5 个时钟周期的单时钟周期图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_4_21.png" width="70%" style="margin: 0 auto;">
</div>

### 流水线控制

现在我们要将控制添加到流水线数据通路中，这一部分可以类比我们[在单周期处理器中的做法](https://victorwang712.github.io/Note/computer_science/computer_organisation/chapter_4/#_7)。
