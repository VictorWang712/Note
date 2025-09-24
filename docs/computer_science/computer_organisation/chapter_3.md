---
comments: true
---

# 第三章 - 计算机的算术运算

## 加法和减法

二进制的加法和减法是简单的，需要了解的是如何判断**溢出** (overflow)。

对于有符号数在补码下的运算，我们可以得到这样的溢出条件：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_1.png" width="70%" style="margin: 0 auto;">
</div>

而对于无符号数，我们则将溢出视作进位或借位后的正常结果，所以一般忽略而无需进一步的操作。

能够实现加法和减法运算的硬件称作**算术逻辑单元** (Arithmetic Logic Unit, ALU)。接下来我们来构造这一硬件。

### 1 位 ALU

1 位 ALU 的和与或运算是容易实现的，只需要引入对应逻辑门即可。而加法运算则需要 1 位[全加器](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_3/#_19) 实现，减法运算只需要在执行加法运算前取补码。

于是将这三部分组合在一起即可实现 1 位 ALU。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_2.png" width="70%" style="margin: 0 auto;">
</div>

### 64 位 ALU

类似于[行波进位加法器](https://victorwang712.github.io/Note/computer_science/digital_logic_design/chapter_3/#_20)，我们只需要将 64 个 1 位 ALU 相连，即可得到 64 位 ALU。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_3.png" width="70%" style="margin: 0 auto;">
</div>

### 修改 64 位 ALU 以适应 RISC-V

目前设计的 ALU 已经支持加、减、与、或四种操作，而且实际上也顺带实现了其他一些逻辑操作。作为逻辑电路其功能已经足够了，但在实际的指令集中这一设计还不完整。

还需支持的一条指令是小于置位指令 `slt`。如果 $rs1 < rs2$，则操作产生 $1$，否则返回 $0$。为实现这一点，首先需要为 ALU 添加一个输入 Less。此时，只需将除最低位外的 Less 均置 $0$，并将减法运算结果的最高位（符号位，即图中的 Set）连接到最低位的 Less 即可。此时得到的 1 位 ALU 如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_4.png" width="70%" style="margin: 0 auto;">
</div>

此外，ALU 还需要能够进行相等判断，以支持条件分支指令。这一操作也是简单的，只需判断减法运算的结果是否为 $0$。

同时，由于每次使用 ALU 做减法时，要将 CarryIn 和 Binvert 都设置为 $1$，其余时候都设置为 $0$。因此也常将这两条控制线合成为一条控制线 Bnegate。于是最终的完整 ALU 如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_5.png" width="70%" style="margin: 0 auto;">
</div>

其控制线输入和对应的功能为：

|Ainvert|Bnegate|Operation|功能|
|:-:|:-:|:-:|:-:|
|`0`|`0`|`00`|与|
|`0`|`0`|`01`|或|
|`0`|`0`|`10`|加|
|`0`|`0`|`11`|减|
|`0`|`1`|`11`|小于比较复位|
|`1`|`1`|`00`|或非|

最后我们通常用如下的记号表示 ALU：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_3_6.png" width="70%" style="margin: 0 auto;">
</div>

### 超前进位

前面我们提到，行波进位是一种直观的实现方式度是不尽人意的。对应的一种机制，即**超前进位加法器** (vary-lookahead adder) 就是用于解决这一问题。
