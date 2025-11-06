---
comments: true
---

# 第七章 - 存储器基础

## 存储器定义

存储器是数字计算机的主要组成部分，它在所有的数字系统中都占有很大比例。**随机访问存储器** (Random-Access Memory，RAM) 只能暂时性地存储数据，而**只读存储器** (ReadOnly Memory，ROM) 可以永久地存储数据。ROM 是众多**可编程逻辑器件** (Programmable Logic Device，PLD) 的一种形式，PLD 通过存储的信息来定义逻辑电路。

## 随机访问存储器

存储器是二进制存储单元和控制信息输入输出存储单元的电路集合。存储器的任何一个存储单元的内容都可以被存取，存取时间是相同的，而与存储单元的物理位置无关，因而命名为随机访问存储器。相反，**顺序存储器** (serial memory)，如磁盘访问信息时需要不同的时间，时间的长短与指定的位置与当前磁头所处的物理位置有关。

二进制信息被分组存储在存储器中，每个组称为一个**字** (word)。8 位一组叫做一个**字节** (byte)。存储部件的容量通常定义为它能存储的总字节数。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_1.png" width="70%" style="margin: 0 auto;">
</div>

上图是存储器的框图。由图可见，要存储的信息从 $n$ 位数据输入线输入，处理好的信息从位数据输出线输出，$k$ 位地址线用来指定当前处理信息的地址，两个控制输入信号用来指定信息的传输方向：`Write` 信号控制将二进制数据输人存储器，而 `Read` 信号控制将二进制数据从存储器输出。

存储器件由它所包含字的个数和每个字的位数来表示。字由地址线进行选择：存储器中的每个字都会被分配一个唯一的编号，叫做**地址** (address)，其范围为 $0 \sim 2^{k - 1}$，其中 $k$ 是地址线的数目。因此，通过把 $k$ 位二进制地址传送给地址线，译码器接收此地址并打开指定路径，就可以访问存储器中对应的字。

### 读写操作

随机访问存储器能执行读和写两种操作。**写** (write) 操作指的是将要存储的字送到存储器中保存，**读** (read) 操作是从存储器中取出已保存字的副本。写信号控制存入操作，读信号控制取出操作。存储器内部电路在这些信号控制下执行指定的功能。

写操作必须执行如下步骤:

1. 将目标字的二进制地址加载到地址线。
2. 将要存入存储器的数据信息位加载到数据输入线。
3. 激活写输入信号。

然后，存储器单元就从数据输入线上得到数据，并将其存储到地址线所确定的目标单元中。

读操作必须执行如下步骤:

1. 将要读出的字所对应的二进制地址加载到地址线。
2. 激活读输入信号。

然后，存储器根据地址找到对应目标字，将对应的数据信息加载到数据输出线上。对字的读操作不改变存储器中的内容。

### 定时波形

存储器单元的操作由其外部设备来控制，如 CPU。CPU 用自己的时钟脉冲进行同步，但存储器不使用 CPU 时钟，它的读写操作定时通过改变控制输入的值来确定。

存储器的读操作**访问时间** (access time) 为从地址请求到数据输出的最大时间间隔，而**写周期时间** (write cycle time) 为从地址请求到完成存储一个字所需的所有存储器内部操作的最大时间间隔。存储器写操作可以在时钟周期间隔内连续进行，CPU 必须在它的内部时钟与存储器读写操作同步的情况下提供存储器控制信号。这就要求存储器的访问时间和写周期时间必须等于 CPU 时钟周期的固定倍数。

下图为一存储周期定时图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_2.png" width="70%" style="margin: 0 auto;">
</div>

### 存储器特征

集成电路 RAM 可以是静态的或动态的。静态 RAM (SRAM) 由存储二进制信息的内部锁存器构成，信息会一直被存储直到断电。动态 RAM (DRAM)以电容电荷的形式存储信息，通过 $n$ 沟道 MOS 管访问电容，存储的电容电荷会随时间放电。通过刷新 DRAM 对电容进行周期性充电，每隔几毫秒循环地对存储字进行读写来恢复衰减的电荷。DRAM 存储芯片功耗较低，单存储器芯片的存储容量较大，而 SRAM 易于使用，读写周期短，且不需要刷新。

掉电就会丢失存储信息的存储器称为**易失性存储器** (volatile memory)，集成电路 RAM（包括 SRAM 和 DRAM）都属于这类存储器，因为它们都需要用外部电源来维持存储的二进制信息。相反，**非易失性存储器** (non volatile memory)，如磁盘，掉电后仍能保持原存储的信息，这是因为磁性元件用磁化方向来表示所存储的数据，而磁化方向在掉电后仍能保留下来。

## SRAM 集成电路

包含 $m$ 个字和每个字 $n$ 位的 RAM 芯片由 $mn$ 个二进制单元组成的阵列和相关电路构成。RAM 单元是 RAM 芯片中的基本二进制存储单元，它通常设计成电子电路而不是逻辑电路。

#### SRAM 芯片

我们以静态 RAM 芯片为例进行讨论。首先介绍一位 RAM 单元逻辑，然后用层次结构中的一位 RAM 逻辑单元描述 RAM 芯片。下图给出了 RAM 单元的逻辑模型。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_3.png" width="70%" style="margin: 0 auto;">
</div>

其存储部分用一个 SR 锁存器来模拟，Select 为锁存器的输入使能控制。若 Select 为 $0$，则其内容保持不变；若 Select 为 $1$，则其内容由 $B$ 和 $\overline{B}$ 的值决定。锁存器的输出由 Select 选通来产生单元输出 $C$ 和 $\overline{C}$。若 Select 为 $0$，则 $C$ 和 $\overline{C}$ 都为 $0$；若 Select 为 $1$，则 $C$ 为存储值，而 $\overline{C}$ 为 $C$ 取反后的结果。

未得到简化的静态 RAM 图，我们把一组 RAM 单元和读写电路组成 RAM **位片** (bit slice)。位片包括与一组 RAM 字中同一个位相关的所有电路。其逻辑图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_4.png" width="70%" style="margin: 0 auto;">
</div>

图中灰色部分表示每个 RAM 单元。锁存器单元的加载由字选输入信号控制。若字选输入为 $0$，则 S 和 R 都为 $0$，锁存器单元的内容保持不变；若字选输入为 $1$，则写入存储器的值由写逻辑的两个信号 $B$ 和 $\overline{B}$ 来决定。为了使这两个信号中的某一个为 $1$ 并可以改变一寸处的值，$\text{Read} / \overline{\text{Write}}$ 信号必为 $0$，位选信号必为 $1$。数据输入和它的补分别加载到 $B$ 和 $\overline{B}$，以置位或复位所选择的 RAM 单元。若数据输入为 $1$ 则锁存器置位为 $1$；若数据输入为 $0$ 则锁存器复位为 $0$，这样写操作就完成了。

一次仅进行一个字的写操作，即只有一条字选择线置为 $1$，其它字选择线置为 $0$，只对一个连接到 $B$ 和 $\overline{B}$ 的 RAM 单元进行写操作。字选择也通过共享读逻辑控制对 RAM 单元的读操作。若字选择为 $0$，则通过与门阻止 SR 锁存器中的存储信息输出到读逻辑的一对或门上；若字选择为 $1$，则读逻辑读出信息传送到 RAM 位片的数据输出线上。

图片中也给出了 RAM 位片符号用来表示 RAM 芯片的内部结构，每条字选择线延长超出位片，当并排放置多个位片时，相应的字选择线就连接到一起。

有了 RAM 位片，我们就可以得到更大规模的 RAM 芯片，下图给出了 RAM 芯片的符号和框图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_5.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，芯片对于每 16 个 1 位字都有 4 条地址输入，还有数据输入、数据输出和 $\text{Read} / \overline{\text{Write}}$ 信号。芯片及的片选信号与由多个芯片构成的 RAM 级的存储器使能信号对应，芯片内部由一个具有 16 个 RAM 单元的 RAM 位片组成。在控制的 16 条字选择选通线中，有且只有一条信号值为 $1$，所以要使用一个 4-16 译码器将 4 位地址译码成 16 位的字选择选通信号。

#### 重合选择

RAM 芯片中，译码器可以直接简单地设计成：具有 $k$ 个输入和 $2^{k}$ 个输出，需要 $2^{k}$ 个具有 $k$ 个输入的与门。另外，若字数很多，因每个字都有一位包含于一个 RAM 的位片中，所以共享读写电路的单元数量也很多。在这两种情况下，相应的电路特征都会导致 RAM 的读写周期时间变长，这是我们不希望的。

用两个译码器使用**重合选择** (coincident selection) 模式可以减少译码器中门的个数、每个门的输入个数和每个位片的 RAM 单元数。一种可能的配置时：可以用两个 $\frac{k}{2}$ 输入的译码器代替一个 $k$ 输入的译码器，一个译码器用来控制字选择，另一个译码器用来控制位选择，组成二维阵列模式。若 RAM 芯片有 $m$ 个字，每字一位，则该模式下被选择的是位于字选择行和位选择列交点处的 RAM 单元。字选择不再严格用于对字进行选择，所以被改为**行选择** (row select)，而另一个译码器输出信号用于选择一个或多个位片，被称作**列选择** (column select)。

$16 \times 1$ 的 RAM 结构的重合选择如下图所示：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_6.png" width="70%" style="margin: 0 auto;">
</div>

由图可知，此芯片由 4 个位片组成，每个位片包含 4 位，共有 16 个 RAM 单元构成二维阵列。最高两位地址通过 2-4 行译码器选择阵列中 4 行中的某一行，最低两位地址通过 2-4 列译码器选择阵列中 4 列（位片）中的一列。片选作为列译码器的是能控制信号。若片选为 $0$，不作选择操作，译码器的所有输出为 $0$，用来组织对阵列中任何 RAM 单元的写操作；若片选为 $1$，对 RAM 中的某一位进行访问。通过行列选择，$\text{Read} / \overline{\text{Write}}$ 信号决定要执行的操作，读操作期间（$\text{Read} / \overline{\text{Write}} = 1$），被选行中的被选位通过或门传到三态缓冲器。由于缓冲器用片选作为使能控制，所以读取值出现在数据输出上。写操作时（$\text{Read} / \overline{\text{Write}} = 0$），数据输入线上的位传输到目标 RAM 单元中，而没被选择的 RAM 单元处于无效状态，维持原来存储的信息。

下图则是用同一 RAM 单元阵列构成 $8 \times 2$ 的 RAM 芯片（共 8 个字，每字 2 位）。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_7.png" width="70%" style="margin: 0 auto;">
</div>

可见该结构的行译码和 $16 \times 1$ 的结构一致，仅仅改变了列译码器和输出逻辑。

### SRAM 芯片阵列

当前集成电路 RAM 容量大小不一。若应用中需要存储容量大于当前所使用芯片的存储容量，则必须将数块芯片组合起来以达到存储容量要求。存储容量取决于两个参数：字数和每个字的位数。增加字数需要增加地址长度，地址长度每增加一位，存储器的字数增加一倍。增加每个字中的位数需要增加数据输入线和数据输出线的数量，而地址长度保持不变。

为了说明 SRAM 芯片阵列，我们首先用简化的输入输出表示来介绍 RAM 芯片，其标识图符号如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_8.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，该芯片的容量为 64K 字，每个字 8 位，需要 16 位地址和 8 位输入输出线。在方框图中，16 根地址线、8 根输入线和 8 根输出线分别同三条线来表示，这三条线上各有一条斜杠，并标有一个数字以表示这条线所表示的线的根数。片选（CS）信号选择特定的 RAM 芯片，$\text{Read} / \overline{\text{Write}}$ 信号控制芯片进行都还是写操作，输出端的小三角形是三态输出的标准图形符号。片选信号控制数据输出线的行为，若 $\text{CS} = 0$，芯片不被选中，其所有的数据输出处于高阻状态；若 $\text{CS} = 1$，数据输出线传送所选择字的 8 位数据。

假设我们想通过使用两个或更多 RAM 芯片来增加存储系统的字数。因为每增加一位地址可以使所表示的二进制数加倍，所以增加一位地址自然就使存储容量增加到两倍字数。

考虑如何用 4 个 $64 \mathrm{K} \times 8$ 的 RAM 芯片构成一块 $256 \mathrm{K} \times 8$ 的 RAM 芯片。如下图所示：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_9.png" width="70%" style="margin: 0 auto;">
</div>

由图，8 位数据输入线连接到所有芯片上。将所有的三态输出连接起来形成整个存储系统的 8 位数据输出线，这种类型的输出连接方式可能仅仅适用于三态输出，任何时候只有一个芯片的输入被激活，其它芯片处于无效状态。被选择芯片的 8 位输出为 $0$ 或 $1$，而其它芯片的输出处于高阻状态，只允许所选芯片的二进制输出信号作为整个存储系统的输出。

我们也可以把两块芯片组合成包含相同字数的符合存储系统，其中每个字的位数扩展为原来的两倍。下图所示为两块 $64 \mathrm{K} \times 8$ 的芯片构成一个 $64 \mathrm{K} \times 16$ 的存储系统的内部连接：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_10.png" width="70%" style="margin: 0 auto;">
</div>

由图，16 位的输入输出数据线分布于两个芯片上，两个芯片共享 16 位地址线、CS 和 $\text{Read} / \overline{\text{Write}}$ 信号。

上面介绍的两种存储容量扩展技术仅仅介绍了将若干个相同的芯片组成新的大容量存储系统。此新存储系统的字长（字的位数）是单个芯片的单个字长的若干倍，字数是单个芯片字数的以 $2$ 为因子的倍数。外部译码器需要根据此新存储系统的地址来选取特定的芯片。

为了减少封装芯片的引脚数，许多 RAM 芯片通过**双向** (bidirectional) 端口来复用数据输入输出端，这就意味着，复用端口在读操作时为输出端，在写操作时为输入端。双向信号线由三态缓冲器构成，需要通过片选和 $\text{Read} / \overline{\text{Write}}$ 对三态缓冲器进行控制才能使用双向信号。

## DRAM 芯片

### DRAM 单元

动态 RAM 单元电路结构由电容 C 和晶体管 T 组成。电容用来存储电荷，若电容存储足够电荷，则可认为其逻辑值为 $1$；若电容存储的电荷不够，则其逻辑值为 $0$。

进一步地，存储器单元的读写操作可以类比为流体力学中的例子，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_12.png" width="70%" style="margin: 0 auto;">
</div>

### DRAM 位片

DRAM 位片模型的与 SRAM 位片模型类似，如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_11.png" width="70%" style="margin: 0 auto;">
</div>

由图可知，除了单元结构不同外，两种 RAM 位片在逻辑上是相同的。但不能忽视的是，每位 SRAM 单元比 DRAM 单元大约复杂三倍。因此 DRAM 更适用于大规模存储器。

进一步地，我们来讨论 DRAM 中如何进行地址处理。大的 DRAM 系统可能需要 20 或更多的地址位，为了减少引脚数量，可以将 DRAM 地址分为行地址和列地址两部分，串行地先加载行地址，再加载列地址。基于这一点，我们可以得到包括刷新逻辑的 DRAM 框图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_13.png" width="70%" style="margin: 0 auto;">
</div>

DRAM 的读写定时也有针对性的设计。为了支持刷新，要附加一些逻辑电路以实现对刷新的控制。具体来说，激活刷新周期的标准方式和相应的刷新类型如下：

1. 按行刷新。行地址加载到地址线上，RAS 由 $1$ 变为 $0$ 时刷新。在这种情况下，刷新地址必须由 DRAM 芯片外部提供，通常由被称为 DRAM 控制器的芯片来提供。
2. 按列先行后方式刷新。CAS 先从 $1$ 变为 $0$，之后 RAS 由 $1$ 变为 $0$ 时刷新。CAS 保持不变，RAS 变化可以完成一个刷新周期。这种情况下的刷新地址由刷新计数器提供，完成一个刷新周期后，刷新计数器加 $1$。
3. 隐式刷新。正常读写周期结束后刷新，CAS 保持为 $0$，RAS 循环变化，不断进行列先行后方式刷新。在每个隐式刷新期间，前一个读出的数据仍保持有效，所以称这种刷新方式为隐式刷新。隐式刷新所需的时间较长，因此会延迟下一个读写操作。

基于此，我们可以得到 DRAM 读和写操作的定时图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_14.png" width="70%" style="margin: 0 auto;">
</div>

## DRAM 分类

### 同步 DRAM (SDRAM)

采用钟控传输方式是 SDRAM 区别于传统 DRAM 的一大特点。下图是一个 SDRAM 集成芯片的框图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_15.png" width="70%" style="margin: 0 auto;">
</div>

由图可知，除了同步操作的时钟信号外，其输入输出信号与 DRAM 几乎没有区别，但其实两者的内部结构存在很多不同。从外部来看，因为 SDRAM 要实现同步，所以在其地址输入和数据输入输出端口都设有同步寄存器。另外，增加的列地址寄存器是 SDRAM 操作的关键。SDRAM 与普通 DRAM 的控制逻辑看起来类似，但因为 SDRAM 有一个可以从地址总线加载的模式控制字，所以其控制要复杂得多。

下图给出了 SDRAM 的一个定时图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_16.png" width="70%" style="margin: 0 auto;">
</div>

可见其极速读的字节速率较 DRAM 要高。

### 双倍数据速率 SDRAM (DDR SDRAM)

第二种类型 DRAM 是双倍数据速率 SDRAM (DDR SDRAM)，它能在不增加始终开销的前提下克服 DRAM 的速率限制。与 SDRAM 不同，DDR SDRAM 在时钟的上升沿和下降沿均能读取数据。

### RAMBUS DRAM (RDRAM)

最后讨论 RAMBUS DRAM (RDRAM)。RDRAM 芯片继承于基于包总线的存储系统中，为 RDRAM 芯片和处理器的存储总线提供互联。其时序图如下例：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_7_17.png" width="70%" style="margin: 0 auto;">
</div>

## 动态 RAM 芯片阵列

DRAM 控制器应具有下述功能：

1. 将地址分为行地址和列地址，并在适当的时间提供它们。
2. 在适当的时间提供 $\overline{\text{RAS}}$ 和 $\overline{\text{CAS}}$ 信号控制读、写和刷新操作。
3. 在规定时间间隔内执行刷新操作。
4. 提供其它一些状态信号，如表示存储器是否忙于执行刷新操作等。

DRAM 控制器是一个复杂的同步时序逻辑电路，由外部 CPU 时钟控制其同步操作。
