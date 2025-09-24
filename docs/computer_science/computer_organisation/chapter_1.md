---
comments: true
---

# 第一章 - 计算机概要与技术

## 计算机系统结构中的 8 个伟大思想

1. 面向摩尔定律的设计：**摩尔定律** (Moore' Law) 指出单芯片上的集成度每 18 ~ 24 个月翻一番。这一定律驱使计算机设计者在以年为单位的项目中，必须在设计时预测其设计完成时的工艺水平，而不是设计开始时的。
2. 使用抽象简化设计：提高硬件和软件生产率的主要技术之一是使用**抽象** (abstraction) 来表示不同的设计层次，在高层次中看不到低层次的细节，只能看到一个简化的模型。
3. 加速大概率事件：**加速大概率事件** (common case fast) 远比优化小概率事件更能提高性能。大概率事件通常比小概率事件简单，从而易于提高。这一规则也意味着设计者需要知道什么事件是经常发生的。
4. 通过并行提高性能：从计算的诞生开始，计算机设计者就通过并行执行操作来提高性能。这类操作称作**并行性能** (parallel performance)。
5. 通过流水线提高性能：在计算机系统结构中，一个特别的并行场景就是**流水线** (pipelining)。在流水线中每个流程同时进行，这比等一个流程完全结束再开始下一个流程会快很多；
6. 通过预测提高性能：如果在某些情况下，从误预测恢复执行代价不高且预测的准确率相对较高，则通过**预测** (prediction) 的方式提前开始操作有利于优化性能。
7. 存储器层次：通过**存储器层次** (hierarchy of memory) 可以解决硬件成本和性能间的矛盾。
8. 通过冗余提高可靠性：计算机不仅需要速度快，还需要工作可靠。通过冗余部件可以提高系统的**可靠性** (dependable)。

## 程序概念入门

现代计算机程序基本遵循如下的架构：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_1_1.png" width="70%" style="margin: 0 auto;">
</div>

可以看到，由人类程序员编写的**高级编程语言** (high-level programming language) 经**编译程序** (compiler) 编译后得到**汇编语言** (assembly language)。随后，汇编语言经**汇编程序** (assembler) 汇编后得到计算机可以理解的**机器语言** (machine language)。

这一流程便于程序员用更自然的语言来思考，从而提高程序员的生产率。同时，采用高级语言编写程序提高了程序相对于计算机的独立性。

## 硬件概念入门

组成计算机的 5 个经典部件是：

- **输入部件** (input)
- **输出部件** (output)
- **控制器** (control)：负责指导数据通路、存储器和 I/O 设备按照程序的指令正确执行
- **数据通路** (datapath)：负责完成算术运算
- **存储器** (memory)：程序运行时的存储空间，同时保存程序运行时所使用的数据，由**动态随机访问存储器** (dynamic random access memory, DRAM) 芯片组成

其中控制器与数据通路共同组成**处理器** (processor)，也称作**中央处理单元** (central processor unit, CPU)。在处理器内部使用的存储器是**缓存** (cache memory)，采用的是**静态随机访问存储器** (static random access memory, SRAM)。

另一个重要的抽象结构是硬件和底层软件之间的接口，即计算机的**指令集体系结构** (instruction set architexture)。这包括程序员正确编写二进制机器语言程序所需的全部信息，提供给应用程序员的基本指令集和操作系统接口合称为**应用二进制接口** (application binary interface, ABI)。

存储器可以分为两类：即**易失性存储器** (volatile memory) 和**非易失性存储器** (nonvolatile memory)。基于存储器层次，前者也称作**主存储器** (main memory, primary memory)，后者称作**二级存储器** (secondary memory)。

## 处理器和存储器制造技术

**晶体管** (transistor) 是一种受电流控制的开关。**集成电路** (integrated circuit, IC) 是由成千上万个晶体管组成的芯片。如今计算机领域普遍采用的是**超大规模集成电路** (very larg-scale integrated circuit, VLSI)。

下图表示了集成电路制造的全过程：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_1_2.png" width="70%" style="margin: 0 auto;">
</div>

集成电路的成本，可以用以下公式定量表示：

- $\text{每芯片的价格} = \frac{\text{每晶圆的价格}}{\text{每晶圆的芯片数} \times \text{成品率}}$
- $\text{每晶圆的芯片数} \approx \frac{\text{晶圆面积}}{\text{芯片面积}}$
- $\text{成品率} = \frac{1}{(1 + \frac{\text{单位面积的瑕疵数} \times \text{芯片面积}}{2})^{2}}$

## 性能

### 性能的定义

在定义性能前，我们先引入两个定义：

- **响应时间** (response time)：也称**执行时间** (execution time)，指计算机完成某任务所需的总时间。
- **吞吐率** (throughput)：也称**带宽** (bandwidth)，指单位时间内完成的任务数量。

从本课程的角度出发，我们在讨论计算机性能时主要考虑响应时间方面。为了使性能最大化，我们希望任务的响应时间最小化。于是对于某个计算机 X，我们可以定义：

$$\text{性能}_{X} = \frac{1}{\text{执行时间}_{X}}$$

基于这个定义，我们就可以量化地比较不同计算机间的性能。

### 性能的度量

程序的执行时间一般以秒为单位，然而时间可以根据我们的计量方法选用不用的表示方法。对时间最直接的定义是**墙上时钟时间** (wall clock time)，即响应时间、**消逝时间** (elapsed time)。

但很多时候，一个处理器需要同时运行多个程序，此时系统可能侧重于优化吞吐率，而非最小化一个程序的响应时间。基于此，我们提出其它几个概念：

- **CPU 执行时间** (CPU execution time)：简称 CPU 时间，只包括任务在 CPU 上花费的时间，而不把等待 I/O 或其它的时间。
- **用户 CPU 时间** (user CPU time)：在程序本身所花费的 CPU 时间。
- **系统 CPU 时间** (system CPU time)：为执行程序而花费在操作系统上的时间。

同时，在深入研究计算机的细节是，常用的时间度量是**时钟周期** (clock cycle)，即计算机时钟一个周期的时间。其倒数称作**时钟频率** (clock rate)。

### CPU 性能及其因素

在提出了以上定义后，我们就有如下的公式：

$$\begin{aligned}
\text{CPU 执行时间} & = \text{CPU 时钟周期数} \times \text{时钟周期时间} \\ & = \frac{\text{CPU 时钟周期数}}{\text{时钟频率}}
\end{aligned}$$

### 指令的性能

进一步地，我们考察指令的平均时间。**指令数** (instruction count) 是一个程序的指令总数，**CPI** (clock cycle per instruction) 指执行每条指令所需的时钟周期数的平均值。于是又有公式：

$$\text{CPU 时钟周期数} = \text{指令数} \times \text{CPI}$$

### 经典的 CPU 性能公式

结合以上两部分，我们可以得到基本的性能公式：

$$\begin{aligned}
\text{CPU 执行时间} & = \text{指令数} \times \text{CPI} \times \text{时钟周期时间} \\ & = \frac{\text{指令数} \times \text{CPI}}{\text{时钟频率}}
\end{aligned}$$

### 性能的改进

根据前面的公式，我们容易知道改变哪些参数有利于改进性能。但是在实际情况中，我们需要遵循**加速大概率事件**的思想，更精确地评估改进对性能的影响：

$$\text{改进后的执行时间} = \frac{\text{受改进影响的执行时间}}{\text{改进量}} + \text{不受影响的执行时间}$$

这一公式被称作 **Amdahl 定律** (Amdahl's law)，其表明了对于特定改进的性能提升可能由所使用的改进特征的数量所限制这一客观规律。

### 其它度量性能的方法

根据前述的分析，简单地只用时钟频率、指令数和 CPI 去比较性能可能不一定能得到合理的结论。于是一个用于取代时间以度量性能的指标被提出，即**每秒百万条指令** (million instructions per second, MIPS)，其计算公式为：

$$\begin{aligned}
\text{MIPS} & = \frac{\text{指令数}}{\text{执行时间} \times 10^{6}} \\
& = \frac{\text{时钟频率}}{\text{CPI} \times 10^{6}}
\end{aligned}$$

这一指标易于理解且符合直觉，但仍然存在一些问题。首先，MIPS 只考察了指令执行的速率，但没有考虑不同指令的复杂度；其次，MIPS 不能用于比较使用不同指令集的计算机。因此，综合各项指标进行评估，永远是评估性能的合理举措。

## 功耗墙

通常来说，一个晶体管的能耗取决于其负载电容和工作电压，即：

$$\text{能耗} \propto \text{负载电容} \times \text{电压}^{2}$$

由于该公式考察的是 $0 \to 1 \to 0$ 这一完整过程的能耗，而每个晶体管的功耗是一次翻转需要的能耗和开关频率的乘积，因此有：

$$\text{功耗} \propto \frac{1}{2} \times \text{负载电容} \times \text{电压}^{2} \times{开关频率}$$

一直以来，工程师们采用各种技术降低工作电压，从而使功耗得到显著降低。但随着技术革新，当下遇到的问题是，电压继续下降会使晶体管泄漏电流过大，而这是难以处理的。这一情况即称作功耗墙。这也驱动着工程师们探索新的方法改进功耗。
