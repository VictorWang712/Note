---
comments: true
---

# 第五章 - 层次化存储

## 引言

在实际执行计算机程序时，都遵循**局部性原理** (principle of locality)。局部性原理表明，在任意一段时间内程序都指挥访问地址空间中相对较小的一部分内容。局部性有两种：

- **时间局部性** (temporal locality)：如果某个数据项被访问，那么在不久的将来它可能再次被访问。
- **空间局部性** (spatial locality)：如果某个数据项被访问，与它地址相邻的数据项可能很快也将被访问。

我们可以利用局部性原理来构建计算机的存储系统，称作**存储层次结构** (memory hierarchy)。存储层次结构包括不同速度和容量的多级存储。存储速度越快，价格越昂贵，但容量越小。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_1.png" width="70%" style="margin: 0 auto;">
</div>

上图是典型的层次化存储的基本结构。可见，速度越快的存储越靠近处理器；月满的存储成本越低，离处理器越远。这样做既能一相对低的价格提供大容量的存储，同时访问速度和最快的存储相当。

同样，数据也有相似的层次性：靠近处理器的那一层中的数据是那些较远层次中数据的子集，而所有的数据都被存在最远的那一层。

层次化存储可以有不同的层次组成，但是数据只能在两个相邻层次之间进行复制。我们每次只关注相邻的两个层次，在相邻两层之间进行信息交换的最小单元称作**块** (block) 或**行** (line)，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_2.png" width="70%" style="margin: 0 auto;">
</div>

如果处理器所叙的数据在本层的存储中找到，称作**命中** (hit)。如果没在本层存储中找到所需数据，称作**失效** (miss)，将访问下一级存储。**命中率** (hit rate) 指的是在访问本层存储时命中的次数占总次数的比例，通常作为存储层次结构的性能衡量指标之一。**失效率** (miss rate) 指的是在访问本层存储时失效的次数占总次数的比例。

由于性能是引入层次化存储的主要原因，数据命中和失效的处理时间是非常重要的。**命中时间** (hit time) 是访问本层存储的时间，包括判断访问命中或失效的时间。**失效损失** (miss penalty) 指的是将相应的块从下层存储替换到上层存储中的时间，加上将数据块返回给处理器的时间。由于上层存储容量更小，并由速度更快的存储组成，命中时间也比下层存储的访问时间短，而访问下层存储的时间是失效损失的重要组成部分。

## 存储技术

在当今的层次化存储中有四种主要技术。主存采用**动态随机访问存储** (Dynamic Random Access Memory, DRAM) 器件实现，靠近处理器的存储层次使用**静态随机访问存储** (Static Random Access Memory, SRAM) 器件实现。DRAM 的访问速度慢于 SRAM，但它的没每比特成本也要低很多。两者的价格差主要源于 DRAM 的每比特占用面积远远小于 SRAM，因而 DRAM 能在等量的硅上实现更大的存储容量。第三种技术称作**闪存** (flash memory)，这种非易失性存储一般作为个人移动设备的二级存储。第四种技术是**磁盘** (magnatic disk)，用来实现服务器上最大也是最慢的存储层次。

### SRAM 存储技术

SRAM 存储是一种存储阵列结构的简单集成电路，通常有一个读写端口。虽然读写操作的访问时间不同，但对于任意位置的数据，SRAM 的访问时间是固定的。SRAM 不需要刷新电路，所以访问时间可以和处理器的时钟周期接近。

过去，大多数个人电脑和服务器使用独立的 SRAM 芯片作为一级、二级甚至三级高速**缓存** (cache)。如今由于摩尔定律，所有的高速缓存都被集成到处理器芯片上，因此独立的 SRAM 芯片不再流行。

### DRAM 存储技术

在 SRAM 中，只要提供电源，数值会被一直保存。而在 DRAM 中，使用电容保存电荷的方式来存储数据。采用单个晶体管来访问存储的电荷，或读，或写。DRAM 的每个比特仅使用单个晶体管来存储数据，它比 SRAM 的密度更高，每比特价格更低廉。由于 DRAM 在单个晶体管上存储电荷，因此不能长久保持数据，必须进行周期性的刷新。与 SRAM 相比，这也是该结构被称作动态的原因。

DRAM 的内部结构如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_3.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，其采用重合译码的方式，即先给出行地址，再给出列地址进行访问。这种**行** (row) 结构有助于 DRAM 的刷新，也有助于改善性能。为提高性能，DRAM 中缓存了行数据以便重复访问。

为更好地优化与处理器的接口，DRAM 添加了时钟，因此被称作**同步 DRAM** (Synchronous DRAM, SDRAM)。SDRAM 的好处在于，使用始终消除了内存和处理器之间的同步问题。同步 DRAM 的速度优势来自于，进行**突发传输** (burst transfer) 时无须指定额外地址位，而是通过时钟来突发传输后续数据。速度最快的结构称作**双倍数据传输率** (Double Data Rate, DDR) SDRAM，这种结构在时钟的上升沿和下降沿都可以进行数据传输。因此，如果仅考虑时钟频率和数据尾款，使用该结构可以预期获得双倍的数据带宽。

要维持这样的高带宽，需要对 DRAM 的内部结构进行精心组织。现代 DRAM 以 bank 的方式来组织结构，即将 DRAM 划分为若干个 bank。DRAM 可以在内部组织对多个 bank 进行读或写，每个 bank 对应各自的行缓冲，而不仅仅是添加一个快速行缓冲。对多个 bank 发送一个地址允许同时对这些 bank 进行读或写，只需要一次访问时间，之后一轮转到方式对多个 bank 进行访问，就获得了若干倍的带宽。这种轮转的访问方式称作**交叉地址访问** (address interleaving)。

服务器的存储通常都是集成在小电路板上售卖，这种结构被称作**双列直插式内存模块** (Dual Inline Memory Modules, DIMM)。

### 闪存

闪存是一种**电可擦除的可编程只读存储器** (Electrically Erasable Programmable Read-only Memory, EEPROM)。

与磁盘和 DRAM 不同，对于闪存这类 EEPROM 技术，闪存的写操作会对期间本身产生磨损。为应对这种限制，大多数闪存产品都包括一个控制器，用来将发生多次写的块重新映射到较少被写的块，从而使得写操作尽量分散。该技术被称作**耗损均衡** (wear leveling)。具有孙浩俊亨的闪存控制器也能够通过重新映射，将生产制造中出现故障的存储单元屏蔽掉，从而改善产品的**良率** (yield)。

### 磁盘

磁性硬盘由若干盘片组成，每个磁盘表面被分为若干的同心圆，称作**磁道** (track)，每个盘面上通常有几万条磁道。每条磁道按序划分为上千个保存信息的**扇区** (sector)，每个扇区的容量一般为 $512 \sim 4096$ 字节。记录在磁介质上的内容依次为：扇区号、间隙、该扇区的信息（包括纠错码）、下一个扇区的扇区号等。

每个盘面都配有一个磁头，这些磁头互相连接并一起移动，每个磁头都可以读写每个盘面的每一条磁道。某磁头在给定点能够访问到的所有磁道集合称作**柱面** (cylinder)。

操作系统通过三步完成对磁盘的数据访问。

第一步，将磁头定位在正确的磁道上方，这个操作称作**寻道** (seek)，将磁头移动到所需刺刀上方是时间称作**寻道时间** (seek time)。

第二步，当磁头到达正确的磁道后，我们需要等待所需扇区旋转到读写磁头下，这段时间称作**旋转延时** (rotational latency)。平均旋转延时为磁盘旋转半周的时间，即

$$\text{平均旋转延时} = \frac{0.5 \text{转}}{\text{转速}}$$

第三步，在磁头到达正确的扇区后，**数据块** (block) 仍然需要一定的**传输时间** (transfer time)。传输时间和扇区大小、旋转速度和磁道记录密度有关。

与闪存相同，磁盘也是非易失性存储，但是相较闪存没有写损耗问题。

## cache 基础

我们从一个简单的**高速缓存** (cache) 开始。我们假设处理器每次请求为一个字，且每个数据块由单个字组成。下图给出了这种简单 cache 在响应初始不在 cache 中的数据访问请求前后的情况：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_4.png" width="70%" style="margin: 0 auto;">
</div>

具体来说，在响应请求前，该 cache 中包含了最近访问的数据集合 $X_{1}, X_{2}, \cdots, X_{n - 1}$，处理器请求的字 $X_{n}$ 并不在 cache 中。这个请求会产生一次失效，字 $X_{n}$ 从内存取到 cache 中。

在这个场景中，我们需要思考这样一个问题，即如何知道数据项是否存在于 cache 中？进一步来说，如果知道数据项存在于 cache 中，我们又该如何找到这个数据项？这两个答案是有关联的。如果每个字能够位于 cache 中的确定位置，只要它在 cache 中，那么找到它就是简单的。

在 cache 中为每个存储中的数据子进行位置分配的最简单方式，就是基于它在存储中的地址来分配 cache 中的位置，这种 cache 结构称作**直接映射** (direct mapped)。直接映射 cache 中，存储地址和 cache 位置之间的典型映射关系通常非常简单，例如下述映射关系：

$$\text{cache 块号} = (\text{块地址}) \mod (\text{cache 中的数据块数量})$$

如果 cache 的块数是 $2$ 的幂，则取模运算很简单，只需要取地址的低 $N$ 位即可，其中 $N = \log_{2} (\text{cache 的块数})$。一个 8 个字的直接映射 cache 如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_5.png" width="70%" style="margin: 0 auto;">
</div>

由于每个 cache 块中能够保存不同存储地址的内容，如何知道对应请求的数据字是够在 cache 中呢？这需要我们在 cache 中添加一组**标签** (tag)，这些标签保存了所需的地址信息，这些信息用来确定请求字是否在 cache 中。标签中只需要保存地址的高位部分，这部分地址不会用来作为 cache 的索引。例如在上图中，只需要使用 5 位地址中的高 2 位作为标签，低 3 位作为地址的索引字段来选择数据块。

同时，还需要一种方法能够判断 cache 中的数据块中是否保存有效信息。最常用的方法就是添加**有效位** (valid bit)，用来表示该表项中是否保存有效的数据。一般置 $0$ 表示对应数据块不能使用，置 $1$ 表示可以使用。

### cache 访问

我们对 cache 访问的讨论从下面这个示例开始，这是对一个大小为 8 个数据块的空 cache 进行 9 次存储访问的操作序列：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_6.png" width="70%" style="margin: 0 auto;">
</div>

我们看一看第一次访问前后 cache 的变化：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_7.png" width="70%" style="margin: 0 auto;">
</div>

在整个过程中，许多 cache 中的内容也会发生覆写，完整的操作序列执行结束后，cache 应该如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_8.png" width="70%" style="margin: 0 auto;">
</div>

接下来我们讨论 cache 的容量。我们设定如下条件：

- $64$ 位地址
- 直接映射 cache
- cache 中有 $2^{n}$ 个数据块，因此索引字段为 $n$ 位
- 单个数据块大小为 $2^{m}$ 个单字，即 $2^{m + 2}$ 字节，因此在单个数据块中使用 $m$ 位来索引单字，再使用地址的最低 $2$ 位来索引字节

于是，标签字段的大小为：

$$64 - (n + m + 2)$$

该 cache 的总容量为：

$$2^{n} \times (\text{单个数据块容量} + \text{标签字段大小} + \text{有效位大小})$$

由于单个数据块的大小为 $2^{m}$ 个单字，每个单字有 $2^{5} = 32$ 位，并使用 $1$ 位来表示有效位，因此以上 cache 的容量大小为：

$$2^{n} \times (2^{m} \times 32 + (64 - n - m - 2) + 1)$$

> 假设 $64$ 位的存储地址，对于直接映射 cache，如果数据大小为 $16 \mathrm{KiB}$，每个数据块为 $4$ 字大小，求该 cache 的容量。
>
> 数据大小 $16 \mathrm{KiB}$ 为 $2^{12}$ 个字。单个数据块大小为 $2^{2}$ 字，则共有 $2^{10}$ 个数据块。代入公式有
>
> $$2^{10} \times (2^{2} \times 32 + (64 - 10 - 2 - 2) + 1) = 2^{10} \times 179 = 179 \mathrm{Kib}$$

除了会计算 cache 的容量，我们还需要会计算地址的映射。我们看如下例题：

> 假设 cache 有 $64$ 个数据块，每个数据块的大小为 $16$ 字节。对于字节地址 $1200$，会映射到哪个基本块？
>
> $$\text{块地址} = \left\lfloor \frac{\text{字节地址}}{\text{每块中的字节数}} \right\rfloor$$
>
> 题目中即为 $\frac{1200}{16} = 75$。再根据公式
>
> $$\text{cache 块号} = (\text{块地址}) \mod (\text{cache 中的数据块数量})$$
>
> 题目中即为 $75 \mod 64 = 11$。事实上，从 $1200$ 到 $1215$ 的字节地址都映射到这个块号。

容量更大的块可以通过挖掘空间局部性来降低失效率，因此随着块大小的增长，失效率通常都在下降。但如果单个快大小占 cache 容量的比例增加到一定程度，失效率最终会随之上升，这是因为 cache 中可存放的块数变少了。这一关系如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_5_9.png" width="70%" style="margin: 0 auto;">
</div>

增大快容量时，另一个更严重的问题是失效损失。失效损失是从下一级存储获得数据块并加载到 cache 的时间，分为两部分：访问命中的时间和数据的传输时间。容易知道，数据的传输之间将随着数据块容量的增大而增大，而且这会消解数据块容量增大待来的失效率改善的手艺。最终的结果是，失效损失增大引起的性能下降超过了失效率降低带来的手艺，cache 的性能也随之下降。当然，如果能设计出高效的传输大数据快的存储，就可以增大数据块的容量，并得到更大的性能改善。

### 处理 cache 失效

在考虑真是系统的 cache 之前，我们先来讨论一下控制单元如何处理 cache 失效。控制单元必须能够检测到失效，然后通过从下一级存储中取得所需的数据来处理失效。

cache 的失效处理需要两部分协同工作：一部分是处理器的控制单元；另一部分是单独的控制器，用来初始化内存访问和重填 cache。cache 的失效处理会引发流水线的停顿，这与例外或者中断处理不同，后者需要保存所有寄存器的状态，而 cache 失效将会停顿整个处理器流水线来等待下一级内存返回数据。

我们先回顾如何处理指令失效。如果一条指令访问引发了失效，那么指令寄存器的内容将被置为无效。我们可以用相同的方法处理数据失效。为了将正确的指令写入 cache 中，必须能够对下一级存储发出读操作。由于程序计数器 (PC) 是在执行的第一个时钟周期递增，引发指令 cache 失效的指令地址就等于程序计数器的数值减 $4$。一旦确定了地址，就需要知道主存进行读操作。等待内存响应，然后将含有所需指令的字写入指令 cache 中。

一旦发生指令 cache 失效，可以定义如下处理步骤：

1. 将 PC 的原始值（当前 PC 减 $4$）发送到内存；
2. 对主存进行读操作，等待贮存完成本次访问；
3. 写 cache 表项，将从内存获得的数据写入到该表项的数据部分，将地址的高位（来自 ALU）写入标签字段，并将有效位置为有效；
4. 重启指令执行，这将会重新取指，本次取指将在指令 cache 中命中。

以上叙述的是指令 cache 失效的情况。数据访问的 cache 控制本质上是相同的，一旦失效，简单地暂停处理器，直到内存返回数据。

### 处理写操作

写操作有一些不同。例如对于存储指令，只把数据写入数据 cache 而不改变主存。完成写入操作后，主存中的数据将和 cache 中的数据不同。这种情况称作 cache 和主存**不一致** (inconsistent)。保持 cache 和主存一致的最简单方法是，总是将数据写回内存和 cache。这样的写策略称作**写穿透**或**写直达** (write-through)。

写操作的另一个关键点是写失效的处理。我们先从主存中取来对应数据块中的数据，之后将其写入 cache 中，覆盖引发失效的数据块中的数据。同时，也会使用完整地址将数据写回主存。

虽然上述设计方案能够简单地处理写操作，但是其性能不佳。在写穿透策略中，每次写操作都会引起写主存操作，这种写操作的延时很长。

解决这个问题的方法之一是使用**写缓冲** (write buffer)。写缓冲中保存着等待写回主存的数据。数据写入 cache 的同时也写入写缓冲中，之后处理器继续执行。当写入主存的操作完成后，写缓冲中的表项将被释放。如果写缓冲满了，处理器必须停顿流水线直到写缓冲中出现空闲表项。

然而即使采用写缓冲策略，当写操作**成簇** (burst) 发生时，也会发生停顿。为减少这样的停顿发生，处理器通常会增多写缓冲的表项数。

相对于写穿透或者写直达策略，另一种写策略称作**写返回** (write-back)。基于写返回策略，当发生写操作时，新值只被写入 cache 中，被改写的数据块在替换出 cache 时才被写道下一级存储，写返回策略能够改善性能，但是其具体实现相对复杂。
