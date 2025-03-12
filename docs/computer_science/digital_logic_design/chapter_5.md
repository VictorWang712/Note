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

如果一个门的扇出超过其允许的最大数目或产生了比较大的延迟，则必须采用多个们来并行实现或在输出端增加缓冲器。

#### 成本

对于集成电路，基本们的成本通常与电路布局单元所占的面积有关。布局单元的面积与晶体管的大小以及门的布局布线成比例。若忽略布线面积，则门的面积正比于门中晶体管的数目，而晶体管数目又正比于门输入成本。
