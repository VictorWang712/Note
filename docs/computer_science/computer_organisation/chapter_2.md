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
>     bne x9, x24, Exit // go to Exit if save[i] != k
>     addi x22, x22, 1 // i = i + 1
>     beq x0, x0, Loop // go to Loop
> Exit:
> ```

值得补充的一点是，一个没有分支（除结尾），同时没有分支目标或分支标签（除起始）的指令序列称作**基本块** (basic block)。在实际情况中，编译器通过识别出基本块来进行编译的优化，而高级处理器能够加速基本块的执行。

### case/switch 语句

大多数编程语言都包含 case 或 switch 语句。一个直观的实现 switch 的方法是将其转化为一系列 if-then-else 语句，但这里我们要介绍一种更有效的方法。

我们使用编码形成指令序列的地址表，这称作**分支地址表** (branch address table) 或**分支表** (branch table)。程序只需要索引到表中，然后跳转到合适的指令序列。当然，为了支持这一操作，RISC-V 中包含一类**间接跳转** (indirect jump) 指令，其使用方式将在后文指出。

## 计算机硬件对过程的支持

**过程** (procedure) 或函数是编程人员用于结构化编程的一种工具，两者均有助于提高程序的可理解性和代码的可重用性。

在执行过程时，程序会遵循以下 6 个步骤：

1. 将参数放在过程可以访问到的位置
2. 将控制转交给过程
3. 获取过程所需的存储资源
4. 执行所需的任务
5. 将结果值放在调用程序可以访问到的位置
6. 将控制返回到初始点，因为过程可以从程序中的多个点调用

### 跳转-链接指令

RISC-V 为过程调用分配寄存器时遵循以下约定：

- `x10`~`x17`：8 个参数寄存器，用于传递参数或返回值。
- `x1`：1 个返回地址寄存器，用于返回到起始点。

为了完成跳转，RISC-V 汇编语言包含两个**跳转-链接指令** (jump-and-link instruction)。

第一个是 `jal`，用于跳转到某个地址的同时将下一条指令的地址保存到目标寄存器 `rd`，使用方法是：

```asm
jal reg, ProcedureAddress // jump to ProcedureAddress and write return address to register storing the return address
```

指令中的链接部分表示指向调用点的地址或链接，以允许该过程返回到合适的地址。存储在寄存器 `reg`，即**指令地址寄存器** (instruction address register) 中的这个「链接」称作**返回地址** (return address)。返回地址是必需的，因为同一过程可能在程序的不同部分被调用。

由于历史原因，指令地址寄存器也常称作**程序计数器** (program counter)。在 RISC-V 中，这一寄存器缩写为 PC，通常是 `x1`。

第二个是 `jalr`，用于支持过程的返回，使用方法是：

```asm
jalr reg, imm(base_reg) // jump back to saved address and write return address to register storing the return address
```

目标寄存器 `reg` 保存返回地址，通常使用 `x0` 作为目标寄存器，以丢弃返回地址。同时指令跳转回到存储在寄存器 `base_reg` 中的地址。

总的来说，调用程序，即**调用者** (caller) 将参数值放入 `x10`~`x17` 中，并使用 `jal x1, X` 跳转到过程 `X`，即**被调用者** (callee)。被调用者执行计算，将结果放在相同的参数寄存器中，并使用 `jalr x0, 0(x1)` 将控制返还给调用者。

> 变量 `f` 到 `k` 对应于寄存器 `x20` 到 `x25`，寄存器 `x5` 的值为 4，，编译如下 C 语言代码：
>
> ```c
> switch (k) {
>     case 0:
>         f = i + j;
>         break;
>     case 1:
>         f = g + h;
>         break;
>     case 2:
>         f = g - h;
>         break;
>     case 3:
>         f = i - j;
>         break;
> }
> ```
>
> 得到的 RISC-V 代码为：
>
> ```asm
>     blt x25, x0, Exit // test if k < 0
>     bge x25, x5, Exit // or k >= 4, go to Exit
>     slli x7, x25, 3 // Temp reg x7 = k * 8
>     add x7, x7, x6 // x7 = address of JumpTable[k]
>     ld x7, 0(x7) // Temp reg x7 gets JumpTable[k]
>     jalr x1, 0(x7) // jump based on register x7 (entrance)
> Exit:
> ```
>
> Jump address table: `x7 = x6 + k * 8`，对应 `L0` 到 `L3`。
>
> Memory 中存放 `L0` 到 `L3` 的具体指令：
> 
> ```asm
> L0:
>     add x20, x24, x25 // k = 0 so f gets i + j
>     jalr x0, 0(x1) // end of this case so go to Exit
> L1:
>     add x20, x21, x22 // k = 1 so f gets g + h
>     jalr x0, 0(x1) // end of this case so go to Exit
> L2:
>     sub x20, x24, x25 // k = 2 so f gets g - h
>     jalr x0, 0(x1) // end of this case so go to Exit
> L3:
>     sub x20, x21, x22 // k = 3 so f gets i - j
>     jalr x0, 0(x1) // end of this case so go to Exit
> ```

### 使用更多的寄存器

假设对于一个过程，编译器需要比 8 个参数寄存器更多的寄存器，且过程完成后调用者所需的所有寄存器都必须恢复到调用该过程之前所存储的值。此时我们就需要将寄存器换出到存储器中。

换出寄存器的理想数据结构是**栈** (stack)。栈需要一个指向栈中最新分配地址的指针，以指示下一个过程应该放置置换出寄存器的位置或寄存器旧值的存放位置。在 RISC-V 中，**栈指针** (stack pointer) 是寄存器 `x2`，也记作 `sp`。栈指针按照每个被保存或回复的寄存器按双字进行调整。

在看具体的例子前，我们也给出 RISC-V 对寄存器的一些约定。RISC-V 软件将 19 个寄存器分为两组：

- `x5`~`x7` 和 `x28`~`x31`：临时寄存器，在过程调用中不被被调用者（被调用的过程）保存。
- `x8`~`x9` 和 `x18`~`x27`：**保存寄存器** (saved register)，在过程调用中必须被保存。一旦使用，由被调用者保存并恢复。

> 变量 `g`、`h`、`i`、`j` 对应于寄存器 `x10` 到 `x13`，变量 `f` 对应于寄存器 `x20`，编译如下 C 语言代码：
>
> ```c
> long long int leaf_example (long long int g, long long int h, long long int i, long long int j) {
>     long long int f;
>     f = (g + h) - (i + j);
>     return f;
> }
> ```
>
> 得到的 RISC-V 代码为：
>
> ```asm
> leaf_example:
>     addi sp, sp, -24 // adjust stack to make room for 3 items
>     sd x5, 16(sp) // save register x5 for use afterwards
>     sd x6, 8(sp) // save register x6 for use afterwards
>     sd x20, 0(sp) // save register x20 for use afterwards
>
>     add x5, x10, x11 // register x5 contains g + h
>     add x6, x12, x13 // register x6 contains i + j
>     sub x20, x5, x6 // f = x5 - x6, which is (g + h) - (i + j)
>     addi x10, x20, 0 // returns f
>
>     ld x20, 0(sp) // restore register x20 for caller
>     ld x6, 8(sp) // restore register x6 for caller
>     ls x5, 16(sp) // restore register x5 for caller
>     addi sp, sp, 24 // adjust stack to delete 3 items
>
>     jalr x0, 0(x1)
> ```
>
> 可以看到，总的流程可以分为 4 步：
>
> 1. 将传入值压入栈中；
> 2. 执行过程并保存返回值；
> 3. 从栈中弹出数据来恢复旧值；
> 4. 跳转返回以结束过程。

### 嵌套过程

不调用其它过程的过程称作**叶子** (leaf) 过程。显然不是所有过程都是叶子过程，于是各过程间会存在嵌套关系。此时就存在潜在的寄存器冲突。

一种解决方法是将其它所有必须保存的寄存器压栈。具体来说：

- 调用者将所有调用后还需要的参数寄存器或临时寄存器压栈
- - 被调用者将返回地址寄存器和自身使用的保存寄存器压栈

调整栈指针 `sp` 以计算压栈寄存器的数量，返回时从存储器中恢复寄存器并重新调整栈指针。

> 变量 `n` 对应于寄存器 `x10`，编译如下 C 语言代码：
>
> ```c
> long long int fact (long long int n) {
>     if (n < 1) {
>         return 1;
>     }
>     else {
>         return n * fact(n - 1);
>     }
> }
> ```
>
> 得到的 RISC-V 代码为：
>
> ```asm
> fact:
>     addi sp, sp, -16 // adjust stack for 2 items
>     sd x1, 8(sp) // save the return address
>     sd x10, 0(sp) // save the argument n
> 
>     addi x5, x10, -1 // x5 = n - 1
>     bge x5, x0, L1 // if (n - 1) >= 0, go to L1
> 
>     addi x10, x0, 1 // n < 1: return 1
>     addi sp, sp, 16 // pop 2 items off stack
>     jalr x0, 0(x1) // return to caller
> 
> L1:
>     addi x10, x10, -1 // n >= 1: arguments gets (n - 1)
>     jal x1, fact // call fact with (n - 1)
>     addi x6, x10, 0 // return from jal: move result of > fact (n - 1) to x6
>     ld x10, 0(sp) // restore argument n
>     ld x1, 8(sp) // restore the return address
>     addi sp, sp, 16 // adjust stack pointer to pop 2 items
>     mul x10, x10, x6 // return n * fact (n - 1)
>     jalr x0, 0(x1) // return to the caller
> ```

下表总结了过程调用中保存的与不保存的对象。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_3.png" width="70%" style="margin: 0 auto;">
</div>

### 在栈中为新数据分配空间

最后一个复杂点在于，栈也用于存储过程的局部变量，但这些变量不适用于寄存器，例如局部数组或结构体。栈中包含过程所保存的寄存器和局部变量的段称作**过程帧** (procedure frame) 或**活动记录** (activation record)。

一些 RISC-V 编译器使用**帧指针** (frame pointer) `fp` 或寄存器 `x8` 来指向过程帧的第一个双字。下图展示了过程调用之前、期间和之后时栈的状态。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_4.png" width="70%" style="margin: 0 auto;">
</div>

### 在堆中为新数据分配空间

一般在操作系统中，栈从用户地址空间的高端开始并向下扩展。低端内存的第一部分是保留的，之后是 RISC-V 机器代码，通常称作**代码段** (text segment)。在此之上是**静态数据段** (static data segment)，用于存放常量和其它静态变量。下图即展示了这一分配结构：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_5.png" width="70%" style="margin: 0 auto;">
</div>

常用**堆** (heap) 来存放数组和链表等数据结构，其也放在内存中。

最后，我们总结一下 RISC-V 汇编语言的寄存器约定：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/computer_organisation/chapter_2_6.png" width="70%" style="margin: 0 auto;">
</div>

## 对大立即数的 RISC-V 编址和寻址

RISC-V 指令均保持 32 位长，但有时我们会使用较长的常量。这些大常量需要的特定更多处理方式。

### 大立即数

RISC-V 指令系统包括指令**取立即数高位** (load upper immediate)。
