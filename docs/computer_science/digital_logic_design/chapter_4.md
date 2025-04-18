---
comments: true
---

# 第四章 - 时序电路

## 时序电路的定义

### 时序电路

前述的数字电路仅包含组合逻辑电路，但在实际情况中，绝大多数的电路系统还包括存储元件，这样的电路系统称作**时序电路** (sequential circuit)。

时序电路最基本的框图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_1.png" width="70%" style="margin: 0 auto;">
</div>

可见，一个时序电路由组合电路和存储元件连接在一起组成。存储元件是用来存储二进制信息的电路，某一时刻存储在这些存储元件中的二进制信息称为该时刻时序电路的**状态** (state)。时序电路通过输入端从外界接受二进制信息，这些输入值和存储元件的当前状态一起决定了输出端的值，同时也决定了存储元件的下一个状态。

还可以发现，时序电路的输出不仅是其输入的函数，而且还是存储元件当前状态的函数，存储元件的下一个状态也是电路输入以及当前状态的函数。因此，时序电路可以由输入、内部状态和输出的时间序列完全确定。

时序电路主要分为两类，这一分类取决于我们观察输入信号的时间和内部状态改变的时间。**同步时序电路** (synchronous sequential circuit) 的行为可以根据在离散的时间点，其信号线上的相关信息来进行定义；**异步时序电路** (asynchronous sequential circuit) 的行为则依赖于某一时刻的输入信号以及输入信号在连续时间内变化的顺序。

### 存储器

在数字系统中存储信息有很多种方式，使用逻辑电路就是其中一种。计算机存储器最常用的一种实现方法如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_2.png" width="70%" style="margin: 0 auto;">
</div>

我们顺次讨论。首先图 a 中给出了一个缓冲器，其传播延迟为 $t_{G}$，即缓冲器输入端在 $t$ 时刻的信息值要在 $t + t_{G}$ 时刻才会在输出端显现，信息在 $t_{G}$ 时间内被有效存储。

我们将图 a 中缓冲器的输出端连接到其自己的输入端，如图 b 和图 c 所示，那么其暑促就会一直保持不变，这种情况我们称 $0$ 或 $1$ 被存储。

缓冲器的例子表=表明我们可以将具有延迟的逻辑连接成一个闭路圈来构造存储器。任何具有存储功能的环路必须像缓冲器一样，信号在环绕环路一圈后没有改变。在实际情况中，缓冲器通常用两个反相器实现，即如图 d。

然而，尽管这样的电路可以存储信息，却因为没有其他输入可用于改写，从而不能改变所存储的信息。如果用或非门或与非门替代反相器，就可以实现信息的改变。锁存器这一异步存储电路就是用这种方式实现的，我们将在后文讨论。

### 钟控时序电路

同步时序电路只在离散的时刻采集影响存储元件的信号，同步过程是通过**时钟发生器** (clock generator) 这种时序器件产生周期性的**时钟脉冲** (clock pulse) 序列来实现的。把时钟脉冲作为存储元件输入信号的同步时序电路称作**钟控时序电路** (clocker sequential circuit)。

在最简单的钟控时序电路中使用的存储元件称作触发器，有关其细节将在后文讨论。我们此处只需关注钟控时序电路的基本结构，如下图：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_3.png" width="70%" style="margin: 0 auto;">
</div>

可见触发器用于接受时钟脉冲并改变状态，从而影响组合电路在下一个状态的输入。钟控时序电路在实际中广泛应用，因为其操作的正确性依赖于时钟脉冲自身的稳定性，从而避免了电路延迟的影响。

## 锁存器

只要电路一直供电，输入信号不发生变化，存储元件可以无限期地保存二进制数据。**锁存器** (latch) 是一类异步存储电路，不同类型的锁存器或触发器之间的主要区别在于它们拥有的输入信号的个数以及输入信号影响其二进制状态的方式。

### SR 和 $\bar{\text{S}} \bar{\text{R}}$ 锁存器

SR 锁存器电路是由两个交叉耦合的或非门构成的，只需将前述的但环路存储元件中的反相器替换成或非门即可得到。其逻辑图和功能表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_4.png" width="70%" style="margin: 0 auto;">
</div>

据图，我们对 SR 锁存器进行分析。锁存器有两个输入端 $S$ 和 $R$，其中 $S$ 用于置位，$R$ 用于复位，还有两个有用的状态。当输出 $Q = 1$ 且 $\overline{Q} = 0$ 时，称锁存器处于**置位状态** (set state)；当输出 $Q = 0$ 且 $\overline{Q} = 1$ 时，称锁存器处于**复位状态** (reset state)。输出 $Q$ 和 $\overline{Q}$ 通常是互反的，因此当 $S = 1, R = 1$ 而导致 $Q = 0, \overline{Q} = 1$ 时，此状态为未定义状态。

在通常情况下，除非要改变状态，否则锁存器的两个输入信号都将保持为 $0$。若输入端 $S$ 变为 $1$，锁存器进入置位状态；若输入端 $R$ 变为 $1$，锁存器进入复位状态。需要注意的是，将任意一个输入端信号变为 $1$ 前，都需要先将两个信号返回到 $0$，否则电路可能会进入未定义状态，从而导致输出的下一个状态不确定或不可预知。当两个输入同时被置为 $0$ 时，锁存器可能处于置位状态，也可能处于复位状态，这取决于最近哪个输入为 $1$。

与 SR 锁存器相对的，$\bar{\text{S}} \bar{\text{R}}$ 锁存器电路是由两个交叉耦合的与非门构成的。其逻辑图和功能表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_5.png" width="70%" style="margin: 0 auto;">
</div>

其逻辑和状态与 SR 锁存器完全对应，故详细分析就不展开叙述了。

通过增加一个额外的输入控制信号，可以控制锁存器何时对输入敏感，其逻辑图和功能表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_6.png" width="70%" style="margin: 0 auto;">
</div>

### D 锁存器

上述所有类型的锁存器都会遇到同一个问题，即未定义状态的出现。由于时序电路每个状态之间的关联，一旦锁存器进入未定义状态，就会影响后续所有的状态，从而导致锁存器失效。因此我们还是需要继续改进锁存器，以彻底避免这种未定义状态的出现。

一种方法就是确保输入信号 $S$ 和 $R$ 永远不会同时取 $1$，D 锁存器就是按照这种方法，在 $\bar{\text{S}} \bar{\text{R}}$ 锁存器的基础上构造的。D 锁存器只有两个输入信号：数据信号 $D$ 和控制信号 $C$。$D$ 连接到输入端 $\overline{R}$，$\overline{D}$ 连接到输入端 $\overline{S}$。其逻辑图和功能表如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_7.png" width="70%" style="margin: 0 auto;">
</div>

可见，仅当 $C = 1$ 时，输出 $Q$ 才会随输入 $D$ 改变，而且总是和 $D$ 保持一致。这种设计就避免了未定义状态的出现。
