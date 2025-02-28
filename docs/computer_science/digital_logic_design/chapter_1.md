---
comments: true
---

# 第一章 - 数字系统和信息

## 计算机系统设计的抽象层次

|现代计算系统典型的抽象层次|
|:-:|
|算法|
|编程语言|
|操作系统|
|指令集结构|
|微结构|
|寄存器传输|
|逻辑门|
|晶体管电路|

抽象的一个重要特点是修改低层抽象不需要改变它上层的内容。

本课程主要关心从逻辑门到操作系统的抽象层次，重点关注从硬件到硬件与软件之间的接口的设计。

## 数字系统、计算机及其他

### 模拟信号和数字信号

**模拟信号** (analog signal) 和**数字信号** (digital signal) 是携带信息的两种信号。

模拟信号在数值和时间上都是**连续的** (continuous)，而数字信号在数值和时间上都是**离散的** (discrete)。

### 数字系统

**数字系统** (digital system) 基于离散的输入信息和离散的内部信息（即系统状态），生成离散的输出信息。

一个嵌入式系统的模块图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_1.png" width="70%" style="margin: 0 auto;">
</div>

### 模拟数字转换器

**模拟数字转换器** (Analog-To-Digital Converters, ADC) 将（连续的）模拟信号转换为（离散的）数字信号。它为传感器的模拟世界和信号处理的数字世界建立了联系。

ADC 的结果是比特串，例如 `010`, `110`, `100`, `001`。

## 信息表示

### 信号

当前绝大多数电子数字系统的信号都采用两个离散值，称为**二进制** (binary, BIN)。

二进制的两个值可以抽象为：

- 数字：0 和 1
- 逻辑：**真** (TRUE, T) 和**假** (FALSE, F)
- 电平：**高** (HIGH, H) 和**低** (LOW, L)

> 一般地，我们约定 T 和 1 表示高电平，F 和 0 表示低电平。这种约定称为**正逻辑** (positive logic)。

二进制的两个值由物理量的值或值的范围决定。

### 由电压决定的 1 位信号

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_2.png" width="70%" style="margin: 0 auto;">
</div>

**阈值区域** (throshold region) 内的电压所对应的电平是未定义的，会导致该位的状态无效，这被称为**浮动** (floating)。

如果输出引脚的电压在此范围内浮动，那么其输出的信号将是不确定的，会在高电平和低电平间波动。

可以发现，输入和输出信号对电压的容差是不同的。输入信号的电压容差宽于输出信号的电压容差，这是为了保证电路在不断变化和存在不良**噪声** (noise) 的情况下仍能正常工作。

输入和输出信号的电压容差间的差异被称作**噪声容限** (noise margin)。

### 使用二进制的原因

- 电子元件天然具有双态性。

> - 一个开关要么开，要么关
> - 一个晶体管要么导通，要么不导通

- 二进制所需的电路最少，从而占用的空间最少、能耗最少、成本最少。

> 例如为了表示 100 以内的数字，用十进制表示需要 20 个状态，二进制只需要 14 个状态。

???+ note

    事实上从这一点出发，理论最优的进制应当是 $e$ 进制，理论最优的整数进制应当是三进制。但三进制与电子元件的双态性相悖，故难以在现实中大规模应用。

## 数制

**数制** (number systems) 是通过一个正数作为**基底** (radix, base) 和各位数码来表示所有数字的系统。

一个基底为 $r$ 的进制系统使用 $r$ 个不同的数码：$0, 1, \cdots, r - 1$，并可以用如下 $r$ 的不同次幂的多项式表示：

$$A_{n - 1}r^{n - 1} + \cdots + A_{1}r^{1} + A_{0}r^{0} + A_{-1}r^{-1} + \cdots + A_{-m}r^{-m}$$

其中，$0 \leq A_{i} < r$。

采用按位计数法表示数字时，上式对应的数字即为：

$$A_{n - 1} \cdots A_{1}A_{0}.A_{-1} \cdots A_{-m}$$

其中，$.$ 为**小数点** (radix point)，$A_{n - 1}$ 为**最高有效位** (most significant digit, MSD)，$A_{-m}$ 为**最低有效位** (least significant digit, LSD)。

## 进制转换

### 常用进制

|进制|基底|数码|
|:-:|:-:|:-:|
|二进制|2|0, 1|
|**八进制** (Octal, OCT)|8|0, 1, 2, 3, 4, 5, 6, 7|
|**十进制** (Decimal, DEC)|10|0, 1, 2, 3, 4, 5, 6, 7, 8, 9|
|**十六进制** (Hexadecimal, HEX)|16|0, 1, 2, 3, 4, 5, 6, 7, 8, 9, A, B, C, D, E, F|

### 转换方法

- 转换整数部分：用目标基底除原数，并记录余数，重复这一过程。将所有余数**逆序**排列即可得到原数在目标基底下的整数表示。
- 转换小数部分：重复用目标基底乘该数，并记录乘积的整数部分，重复这一过程。将所有整数部分**正序**排列即可得到原数在目标基底下的小数表示

> 大部分十进制下的有限小数在转换为二进制（八进制、十六进制）后会变为无限小数。一般的，我们会指定小数部分的保留位数，并四舍五入或截断得到一个含有限位小数的数字。

???+ note

    这里放一下小数部分在有限位进制转换时不能被精确表示的原因：

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_3.png" width="70%" style="margin: 0 auto;">
    </div>

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_4.png" width="70%" style="margin: 0 auto;">
    </div>

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_5.png" width="70%" style="margin: 0 auto;">
    </div>

需要注意的是，这种由小数进制转换产生的数值差异，是出现计算误差的关键因素。

## 二进制编码

需要编码的信息通常可以分为两类，对应二进制编码的需求也有所不同：

- 数字
    - 需要涵盖所表示数据的全部范围
    - 能够满足简单、普遍的运算
    - 和二进制数值本身有紧密关联
- 非数字
    - 因为不需要满足运算法则而相对灵活，只需保证信息和编码间构成双射
    - 和二进制数值本身不需要有紧密关联

根据编码的方式，可以将二进制编码分为以下两类：

- 有权码：二进制每位都有确定位权值的编码
- 无权码：二进制每位没有确定位权值的编码

有权码的优势在于编码和数字间有固定的计算方式。

### BCD 码

**BCD 码** (binary-coded decimal)，又称 **8, 4, 2, 1 码**，是一种用二进制对十进制数字编码的常用形式，其直接用十进制数作进制转换后得到的二进制数作为编码。

显然 BCD 码是一种有权码。

|十进制数字|BCD 码|十进制数字|BCD 码|
|:-:|:-:|:-:|:-:|
|0|`0000`|5|`0101`|
|1|`0001`|6|`0110`|
|2|`0010`|7|`0111`|
|3|`0011`|8|`1000`|
|4|`0100`|9|`1001`|

### 余三码

**余三码** (Excess-3 code) 是对 BCD 码的改进。其核心思路是在 BCD 码的基础上，增加一个大小为 3 的偏移量。这导致余三码是一种无权码。

这种编码方式的优势在于，十进制下相加进位的两个数，在余三码下相加也刚好进位。同时，余三码还是一种补码，和为 $10$ 的两个数的编码可以通过按位取反得到，这可以使计算更加便携。

|十进制数字|余三码|十进制数字|余三码|
|:-:|:-:|:-:|:-:|
|0|`0011`|5|`1000`|
|1|`0100`|6|`1001`|
|2|`0101`|7|`1010`|
|3|`0110`|8|`1011`|
|4|`0111`|9|`1100`|

### 8, 4, -2, -1 码

8, 4, -2, -1 码即通过给二进制的前四位分别赋权 $8, 4, -2, -1$，从而通过计算得到在该位权下与原十进制数字相等的数码。

8, 4, -2, -1 码是一种有权码，同时其还是一种补码。

|十进制数字|余三码|十进制数字|余三码|
|:-:|:-:|:-:|:-:|
|0|`0000`|5|`1011`|
|1|`0111`|6|`1010`|
|2|`0110`|7|`1001`|
|3|`0101`|8|`1000`|
|4|`0100`|9|`1111`|

### 独热码和独冷码

**独热码** (one-hot code) 指的是只有一个比特为 1，其他全为 0 的一种编码；对应的可以定义**独冷码** (one-cold code)。一种可能的独热码与独冷码编码如下：

|十进制数字|独热码|独冷码|
|:-:|:-:|:-:|
|0|`0001`|`1110`|
|1|`0010`|`1101`|
|2|`0100`|`1011`|
|3|`1000`|`0111`|

独热码或独冷码的优势在于，决定或改变状态机当前状态的成本很低，容易设计也容易检测非法行为等。相应的，其缺点在于信息表示率很低，非法状态多、有效状态少，对存储的浪费较为严重。

???+ warning

    需要注意的是，不能将**数制转换**和**编码**混为一谈。

### 格雷码

**格雷码** (Grey code) 指的是这样一类编码：对于任意相邻的两个数，其编码只有一位不同。

格雷码的编码方式不止一种。最常见的是**二进制反射格雷码** (binary reflected Grey code)，其编码方式极其简洁：

$$n_\text{grey} = n\ \mathrm{XOR}\ (n >> 1)$$

得益于格雷码的特性，其在工程领域应用广泛，对减小能耗起到了一定的作用。

## 字符编码

目前国际上采用的字母数字字符的标准编码为 **ASCII** (American Standard Code for Information Interchange)。它采用 7 位二进制编码，可表示 128 个字符，其包含内容如下：

- 可打印字符（94 个）
    - 大写字母（26 个）
    - 小写字母（26 个）
    - 阿拉伯数字（10 个）
    - 特殊可打印字符（32 个）
- 不可打印字符（34 个）

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_1_6.png" width="70%" style="margin: 0 auto;">
</div>

特别的，如果在 ASCII 下作字母大小写转换，只需对编码的第 6 位取反。

考虑到一个字节有 8 位，往往会在 ASCII 前用第 8 位作校验位。

## 错误侦测

### 冗余

在真实的通信系统中，编码既包括**信源编码** (soruce coding)，还包括**信道编码** (channel coding)。

在信道编码中，由于噪声的存在，可能导致编码在传输过程中发生变化。因此建立一个**错误侦测** (error-detection) 机制就显得很重要。

一种常见的方法是**冗余** (redundancy)，即在传输过程中加入一些额外的信息用以校验。

### 校验位

为了检测出数据传送过程中可能出现的错误，通常在二进制编码中额外加上一个**校验位** (parity bit)。

最常见的校验方式是 **偶校验** (even parity) 和**奇校验** (odd parity)。

在偶校验下，当字符编码中 `1` 的个数为偶数时，校验位为 `0`；奇校验则反之。一个例子如下：

> ||偶校验|奇校验|
> |:-:|:-:|:-:|
> |`1000001`|`01000001`|`11000001`|
> |`1010100`|`11010100`|`01010100`|

一般应用中只需要采用奇偶校验中的一种，偶校验用得更广泛。

???+ warning

    在做题过程中，请一定注意题目要求的是偶校验还是奇校验，以及校验位是加到原编码的最高位前还是最低位后！
