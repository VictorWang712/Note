---
comments: true
---

# 第五章 - 数字硬件实现

## 设计空间

对于一个给定的设计，通常可以用某一种技术来实现，这种技术定义了可用的基本元件及其属性。**设计空间** (design space) 描述了所有技术与表征它们的参数。

### 集成电路

数字电路采用**集成电路** (integrated circuit, IC) 构建而成。集成电路是一个硅半导体警惕，也通常被称作**芯片** (chip)，包含用来构建逻辑门和存储单元的电子元件。

我们常根据集成度来划分集成电路：

- **小规模集成** (SSI) 电路在一个封装中仅包含几个独立的基本们，门的输入和输出与输出与封装的引脚直接相连。门的数目一般少于 10 个。
- **中规模集成** (MSI) 电路在一个封装中包含 10~100 个门，他们通常执行基本的数字功能。
- **大规模集成** (LSI) 电路在一个封装中包含 100 至几千个门，它们包括数字系统，如小型处理器、小型存储器和可编程模块。
- **超大规模集成** (VLSI) 电路在一个封装中包含几千至几亿个门，他们本身往往就是复杂的微处理器和数字信号处理芯片。

### CMOS 电路工艺

**互补金属氧化物半导体** (complementary metal–oxide–semiconductor, CMOS) 工艺具有高密度、高性能、低功耗的优势，是当下电路工艺中最主流的工艺类型。

#### CMOS 晶体管

CMOS 工艺的基础是 MOS（金属氧化物半导体）晶体管。晶体管以及他们之间的相互连接被制造成**裸片** (die)，也可简称之为芯片，他是集成电路的元件。每个矩形裸片都是从被称作**晶圆** (wafer) 的、非常波的晶体硅片上切割而来的。

晶体管的简略图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_1.png" width="70%" style="margin: 0 auto;">
</div>

据图可见，导电多晶硅**栅极** (gate) 处在一个非常薄的二氧化硅绝缘层之上。最后的结构由两个对称的到点区域组成，即**源极** (source) 与**漏极** (drain)。它们之间有一间隙，位于栅极下方，通常称之为**沟道** (channel)。

#### CMOS 晶体管模型

MOS 晶体管模型的行为取决于晶体管的类型。CMOS 工艺引入了两种类型的晶体管：**n 沟道** (n-channel) 和 **p 沟道** (p-channel)。其模型如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_2.png" width="70%" style="margin: 0 auto;">
</div>

#### 完全互补的 CMOS 电路

完全互补的 CMOS 电路是 CMOS 电路的一个子系列，也是最通用的 CMOS 结构，其一般结构与部分实例如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_3.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，这类 CMOS 分为上下两部分：上半部分接电源，由 PMOS 设计出 $F$ 的逻辑；下半部分接地，由 NMOS 设计出 $\overline{F}$ 的逻辑。如此，这个 CMOS 就能同时实现 $F$ 和 $\overline{F}$，即实现了「互补」。

这类 CMOS 的具有设计上的优越性。由第二章中有关[反函数](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_2/#_8)的知识可知，其 PMOS 和 NMOS 的电路是对偶的，只需设计出其中一个，就可以通过对偶直接得到另一个。

### 工艺参数

对于每一个具体的实现工艺，其电子电路设计的细节与电路参数都不同。用来表征一个实现工艺的最重要的参数如下：

- **扇入** (fan-in)：一个门可能的输入数。
- **扇出** (fan-out)：一个门输出驱动的标准负载数。一个输出的最大扇出是指输出在不削弱门性能的前提下可以驱动的删除。
- **噪声容限** (noise margin)：在不使输出产生不良变化的情况下，正常输入允许叠加的最大的外部噪声电压。
- **门的成本** (cost)：该门在包含它的集成电路总成本中所占比例的度量。
- 传播延迟：信号发生变化时从输入传播到输出所需要的时间。电路的操作速度反比于电路中最长通路的传播延迟。
- **功耗（能量损耗）** (power consumption dissipation)：被门消耗的来自于电源的功率。

这里我们将详细讨论扇入、扇出和成本三个参数。

#### 扇入

对于高速工艺，扇入通常不超过 4 或 5 个，这主要是出于对门速度的考虑。而当需要实现一个多于 5 个扇入的门（即「大扇入门」）时，往往使用扇入不多于 5 个的门（即「低扇入门」）连接而成。

#### 扇出

一种度量删除的方法是考察**标准负载** (standard load)。每个被驱动的门的输入在驱动门的输出上提供了一个用标准负载单元度量的负载。一个门的输出负载决定了其输出电压变化所需要的时间。如果输出负载增加，则**转换时间** (transition time) 随之增加。

???+ warning

    请注意区分「传播延迟」和「转换时间」的区别。传播延迟考察的是输入和输出两个门间信号变换的时间差；转换时间考察的是单独一个门电平变化所需的时间。

如果一个门的扇出超过其允许的最大数目或产生了比较大的延迟，则必须采用多个门来并行实现或在输出端增加缓冲器。

#### 成本

对于集成电路，基本门的成本通常与电路布局单元所占的面积有关。布局单元的面积与晶体管的大小以及门的布局布线成比例。若忽略布线面积，则门的面积正比于门中晶体管的数目，而晶体管数目又正比于门输入成本。

## 可编程实现技术

到目前为止，所有实现出来的电路都是固定不变的，即一旦电路设计完毕，其功能就不可再改变。容易想到，这样的实现方式不利于应对复杂的环境变化所带来的功能变化。因此我们要讨论另一种实现技术，即**可编程实现技术** (programmable logic device, PLD)。

在讨论具体的 PLD 前，简单介绍一下 PLD 支撑技术的发展。

- 第一代 - 熔丝和反熔丝：即使用最简单的物理手段
- 第二代 - **掩膜编程** (mask programming)：在芯片中导电的金属层进行适当的连接，以实现对电路的控制
- 第三代 - 存储单元：用一位存储单元驱动一个 $n$ 沟道 MOS 晶体管
- 第四代 - 晶体管开关控制：利用**可擦除** (erasable) 或**电可擦除** (electrically erasable) 方法控制晶体管的导通情况

在这四代技术中，前两代技术是永久的，即器件在编程确定功能后，不能重编程。第三代技术可以重编程，但是具有易失性，即编程逻辑在电源断开后将丢失。第四代技术允许重编程，且不具有易失性。

在具体讨论每种 PLD 之前，我们先给出各种 PLD 能够编程的部分，读者可以在这里进行一些理解记忆，并带着这些内容继续阅读下文。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_4.png" width="70%" style="margin: 0 auto;">
</div>

### 只读存储器

**只读存储器** (read-only memory, ROM) 本质上是一个「永久」存储二进制信息的器件。这些信息由设计者指定，一旦确定后无论电源断开或接通，信息都一直保存在 ROM 中，即 ROM 具有非易失性。

ROM 器件的框图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_5.png" width="70%" style="margin: 0 auto;">
</div>

可以看到，其有 $k$ 个输入，$n$ 个输出。输入提供存储器的**地址** (address)，输出则给出由地址选定的存储字的数据位。一个 ROM 的字数由地址输入决定，$k$ 个地址输入决定有 $2^{k}$ 个字。注意，ROM 没有数据输入，因为其没有写操作。

我们以一个 $2^{5} \times 8$ 的 ROM 为例：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_6.png" width="70%" style="margin: 0 auto;">
</div>

该 ROM 有 $2^{5} = 32$ 个字，每个字 8 位，有 5 根输入线，以产生 $0$ 到 $31$ 的二进制地址。5 个输入通过 5-32 译码器译码成 32 个不同的输入，译码器的每个输入表示一个**存储地址** (memory address)。32 个输出通过可编程连接点连接到 8 个或门上。

由此不难得到，一般情况下，一个 $2^{k} \times n$ 的 ROM 包括一个 $k$-$2^{k}$ 译码器和 $n$ 个或门，每个或门有 $2^{k}$ 个输入，它们通过可编程连接点连接到译码器的每个输出。

### 可编程阵列逻辑器件

**可编程阵列逻辑器件** (programmable array logic, PAL) 是一个或门阵列固定、与门阵列可编程的 PLD。由于只有与门可以编程，并且多个函数不能共用与门的输出，因此利用 PAL 器件进行设计是容易的，但灵活性则相对较弱。

我们以下图的 PAL 为例进行说明：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_7.png" width="70%" style="margin: 0 auto;">
</div>

可以看到，图中器件有 4 个输入、4 个输出，每个输入连接至一个缓冲-反相器，每个输出由固定的或门产生。具体地，图中各输出的值为：

- $W = A B \overline{C} + \overline{A} \overline{B} C \overline{D}$
- $X = A + B C D$
- $Y = \overline{A} B + \overline{B} \overline{C} + C D$
- $Z = A \overline{C} \overline{D} + \overline{A} \overline{B} \overline{C} D + W$

值得注意的是，$Z$ 的输出依赖于 $W$ 的输出，这样的方式有助于减少乘积项，以符合电路中某些门可能的扇入限制。当然，如果要用这种迭代的形式做电路实现，$W$ 的值就不能变动了。

???+ note

    一般这样的迭代最多迭代一层。

### 可编程逻辑阵列

**可编程逻辑阵列** (programmable logic array, PLA)，与 ROM 在概念上类似，区别在于 PLA 不提供变量的全译码，不生成所有的最小项。PLA 用一个与门阵列代替译码器，已变成产生输入变量的乘积项。这些乘积项可选地连接到或门，以便生成所需布尔表达式的积之和。

我们以下图中的 3 输入、2 输出 PLA 为例：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_8.png" width="70%" style="margin: 0 auto;">
</div>

可以看到，每个输入连接至一个缓冲-反相器，然后和与门阵列相连输出所有需要的乘积项，再和或门阵列输出每个输出所需的乘积项。特殊的是，信号在最后输出前，和一个常量一起通过异或门，这样便可以输出积之和整体本身（即与 0 异或）或者整体的反（即与 1 异或）。具体地，图中个输出的值为：

- $F_{1} = A \overline{B} + A C + \overline{A} B \overline{C}$
- $F_{2} = \overline{A C + B C}$

可以发现，在最后与常量进行异或的操作，有利于减少在电路前部需要输出的乘积项，这同样是为符合电路中某些门可能的扇入限制而采取的方法。

基于这一点，当我们用 PLA 实现组合电路时，我们需要考察每个输出的原函数和反函数并合理选择采用哪一个，以期望各输出间共用的乘积项尽量多。

推广到一般情况，对于一个有 $n$ 个输入、$k$ 个乘积项和 $m$ 个输出的 PLA，其内部由 $n$ 个缓冲-反相器、$k$ 个与门、$m$ 个或门和 $m$ 个异或门组成。在输入和异或门之间有 2n \times k$$ 个可编程连接点，在与门和或门之间有 $k \times m$ 个编程连接点，在或门和异或门之间有 $m$ 个可编程连接点。

### 现场可编程门阵列

**现场可编程门阵列** (field-programmable gate array, FPGA) 是当下最为广泛应用的 PLD。尽管各个厂商所生产的 FPGA 具有不同的特性，但基本上都可以分为三个可编程部件：

- 可编程逻辑块
- 可编程互联
- 可编程输入/输出引脚

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_5_9.png" width="70%" style="margin: 0 auto;">
</div>

#### 可编程逻辑块

绝大多数 FPGA 中的可编程逻辑块是通过**查找表** (Look-Up Table, LUT) 实现的。一个查找表是一个 $2^{k} \times 1$ 的存储器，用来实现带有 $k$ 个变量的函数的真值表，称作 $k$-LUT。

可以想到，小规模的查找表可以用多路复用器实现，大规模的查找表可以用小规模的查找表实现。

???+ note

    实际情况中，直接由 MUX 实现的查找表一般是 4 输入或 6 输入的。

#### 可编程互联

可编程互联，即 FPGA 中的逻辑块之间是可以连接的。这么做的原因也是不难理解的：查找表的数量是随函数的输入而指数级增加的，一味增加查找表的数量是不可行的。于是通过逻辑块之间的连接，就可以提供更多的函数实现。

### 可编程输入/输出引脚

这一部分和实际环境有关，即用于满足 FPGA 和外部世界的联通。为了模块的通用性，大多数 FPGA 应当由大量可以配置的引脚，这些引脚既可配置成输入，又可配置成输出，而且能够支持不同的电气接口标准。
