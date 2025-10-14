---
comments: true
---

# 第二章 - 指令

计算机语言中的基本单词称作**指令** (instruction)，一台计算机的全部指令称作该计算机的**指令集** (instruction set)。本章将基于 RISC-V 指令系统进行讲解。

## 计算机硬件的操作数

在 RISC-V 体系结构中，寄存器的大小为 64 位。成组的 64 位在 RISC-V 体系结构中称作**双字** (doubleword)，成组的 32 位在 RISC-V 体系结构中称作**字** (word)。

在当前 RISC-V 计算机上常见 32 个寄存器，约定用 `x` 后跟一个寄存器编号表示。

> 以赋值语句 `f = (g + h) - (i + j)` 为例，变量 `f`、`g`、`h`、`i`、`j` 分别分配给寄存器 `x19`、`x20`、`x21`、`x22`、`x23`。则编译后的 RISC-V 代码为：
>
> ```asm
> add x5, x20, x21 // register x5 contains g + h
> add x6, x22, x23 // register x6 contains i + j
> sub x19, x5, x6 // f gets x5 - x6, which is (g + h) - (i + j)
> ```

### 存储器操作数

RISC-V 指令中的算术运算只作用于寄存器，因此 RISC-V 必须包含在内存和寄存器之间传输数据的指令，即**数据传输指令** (data transfer instructions)。要访问内存中的字或双字，指令必须提供内存**地址** (address)。

计算机分为两种，一种使用最左边或**大端** (big end) 字节的地址作为双字地址，另一种使用最右端或**小端** (little end) 字节的地址作为双字地址。RISC-V 采用的是小端编址。

将数据从内存复制到寄存器的数据传输指令通常称作**载入指令** (load)。实际的 RISC-V 指令名称是 `ld`，表示取双字。

与载入指令相反的指令称作**存储指令** (store)，其从寄存器复制数据到内存。实际的 RISC-V 指令名称是 `sd`，表示存双字。

> 假设 变量 `h` 存放在寄存器 `x21` 中，数组 `A` 的**基址** (base address)，即起始地址存放在寄存器 `x22` 中。编译赋值语句 `A[12] = h + A[8]` 得到的 RISC-V 代码为：
>
> ```asm
> ld x9, 64(x22) // Temporary reg x9 gets A[8]
> add x9, x21, x9 // Temporary reg x9 gets h + A[8]
> sd x9, 96(x22) // Stores h + A[8] back into A[12]
> ```
>
> 其中存放基址的寄存器（`x22`）称作**基址寄存器** (base register)，数据传输指令中的常数（`8`）称作**偏移量** (offset)。
>
> 其中存放基址的寄存器（`x22`）称作**基址寄存器** (base register)，数据传输指令中的常数（`8`）称作**偏移量** (offset)。

### 常数或立即数操作数

有时我们希望将变量与常数进行运算，即算术指令的操作数是常数。实际的 RISC-V 指令名称是 `addi`，称作**立即数加** (add immediate)。

> 假设 变量 `h` 存放在寄存器 `x22` 中，编译赋值语句 `h = h + 4` 得到的 RISC-V 代码为：
>
> ```asm
> addi x22, x22, 4 // h = h + 4
> ```

???+ Warning

    请注意，没有 `subi` 指令，减立即数是通过加一个负立即数实现的。

常数操作数在实际指令中经常出现，而常数 $0$ 尤甚。于是 RISC-V 中专门使用寄存器 `x0` 作为常 $0$ 寄存器，即其存放的值始终为 $0$。

## 计算机中的指令表示

计算机识别的指令是有特定的表示方式的，这种指令的设计称作**指令格式** (instruction format)。

在 RISC-V 中，所有指令都是 32 位长的二进制数。为了将其和汇编语言区分开来，我们将指令的数字称作**机器语言** (machine language)，把这样的指令序列称作**机器码** (machine code)。

### RISC-V 字段

RISC-V 的指令被分为若干个**字段** (field)。每个字段具有不同的含义：

- opcode：操作码，用于区分各种**指令格式** (instruction format)
- funct3：额外的操作码字段，用于区分属于同一指令格式的不同指令
- funct7：额外的操作码字段，用于区分属于同一指令格式的不同指令
- rd：目的操作数寄存器，用于存放操作结果
- rs1：第一个源操作数寄存器
- rs2：第二个源操作数寄存器
- immediate：立即数，即常数，以二进制补码形式存储

对于计算机可能面对的各种指令，我们根据功能将其分为了几种类别，并给出每种类别的指令对应的字段分布。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_1.png" width="70%" style="margin: 0 auto;">
</div>

每个指令对应不同的操作码，这可以通过查表得到。

## 逻辑操作

RISC-V 中也有**逻辑操作** (logical operations) 对应的指令。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_2.png" width="70%" style="margin: 0 auto;">
</div>

需要注意的是，逻辑右移（`srl`、`srli`）用零填充高位（零扩充），算术右移（`sra`、`srai`）用符号位填充高位（符号扩充）。

## 用于决策的指令

计算机与简单计算器的区别在于其决策能力，即能够执行条件分支、循环语句等。在 RISC-V 中，有几类决策指令。

### if-then-else 语句

RISC-V 中实现 if-then-else 语句的方法是采用类似于 go to 语句的方式实现的。

```asm
beq rs1, rs2, L1
```

该指令表示如果寄存器 `rs1` 中的值等于寄存器 `rs2` 中的值，则转到标签为 `L1` 的语句执行。这一指令称作**相等则分支** (branch if equal)。

```asm
bne rs1, rs2, L1
```

该指令表示如果寄存器 `rs1` 中的值不等于寄存器 `rs2` 中的值，则转到标签为 `L1` 的语句执行。这一指令称作**不等则分支** (branch if not equal)。

类似的还有 `blt` 指令，如果寄存器 `rs1` 中的值小于寄存器 `rs2` 中的值则跳转；`bge` 指令，如果寄存器 `rs1` 中的值大于等于寄存器 `rs2` 中的值则跳转。

这些指令都属于**条件分支** (conditional branch) 指令。

> 变量 `f` 到 `j` 对应于寄存器 `x19` 到 `x23`，编译如下 C 语言代码：
>
> ```c
> if (i == j) {
>     f = g + h;
> }
> else {
>     f = g - h;
> }
> ```
>
> 得到的 RISC-V 代码为：
>
> ```asm
>     bne x22, x23, Else // go to Else if i != j
>     add x19, x20, x21 // f = g + h
>     beq x0, x0, Exit // go to Exit if 0 = 0 (unconditional branch)
> Else:
>     sub x19, x20, x21 // f = g - h
> Exit:
> ```

### 循环

有了标签和跳转指令，我们也容易得到循环的汇编代码。

> 变量 `i` 和 `k` 对应于寄存器 `x22` 到 `x24`，数组的基址保存在 `x25` 中，编译如下 C 语言代码：
>
> ```c
> while (save[i] == k) {
>     i += 1;
> }
> ```
>
> 得到的 RISC-V 代码为：
>
> ```asm
> Loop:
>     slli x10, x22, 3 // Temp reg x10 = i * 8
>     add x10, x10, x25 // x10 = address of save[i]
>     ld x9, 0(x10) // Temp reg x9 = save[i]
>     bne x9, x24, Exit // goto Exit if save[i] != k
>     addi x22, x22, 1 // i = i + 1
>     beq x0, x0, Loop // goto Loop
> Exit:
> ```

值得补充的一点是，一个没有分支（除结尾），同时没有分支目标或分支标签（除起始）的指令序列称作**基本块** (basic block)。在实际情况中，编译器通过识别出基本块来进行编译的优化，而高级处理器能够加速基本块的执行。

### case/switch 语句

大多数编程语言都包含 case 或 switch 语句。一个直观的实现 switch 的方法是将其转化为一系列 if-then-else 语句，但这里我们要介绍一种更有效的方法。

我们使用编码形成指令序列的地址表，这称作**分支地址表** (branch address table) 或**分支表** (branch table)。程序只需要索引到表中，然后跳转到合适的指令序列。当然，为了支持这一操作，RISC-V 中包含一类**间接跳转** (indirect jump) 指令，其使用方式将在后文指出。

## 计算机硬件对过程的支持

**过程** (procedure) 或函数是编程人员用于结构化编程的一种工具，两者均有助于提高程序的可理解性和代码的可重用性。

RISC-V 为过程调用分配寄存器时遵循以下约定：

- `x10`~`x17`：8 个参数寄存器，用于传递参数或返回值。
- `x1`：1 个返回地址寄存器，用于返回到起始点。
