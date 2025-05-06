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

## 触发器

在**触发器** (flip-flop) 中，输入信号值的改变可以控制内部锁存器的状态，这种现象称作**触发** (trigger)。对于控制输入信号为时钟脉冲的 D 锁存器，在每次时钟脉冲为 $1$ 时出发。只要时钟脉冲保持有效，那么数据输入信号的任何改变都将改变锁存器的状。从这种意义上讲，锁存器是**透明** (transparent) 的，因为当控制输入端为 $1$ 是时，从输出端可以看到数据输入端的值。

这种性质导致锁存器存在一个缺陷。当时钟脉冲一直为 $1$ 时，如果锁存器的输入信号发生变化，锁存器将响应这一变化进入新的状态，而不是保持原来的状态。这与我们的希望是不符的。

于是，触发器电路的构造就是要消除这种透明性，使得输出信号只在某几个特定的时刻更新，从而使得锁存器的每个状态是可用且能被应用到分析下一个状态的。

现在最常用的触发器都是**主从式** (master-slave) 触发器，即采用两个锁存器构造的触发器。具体来说，第一个锁存器称作主锁存器，它在每次触发的第一个阶段根据输入信号改变它的值；第二个锁存器称作从锁存器，在每次触发的第二个阶段，主锁存器将输出传递到从锁存器中。

### 触发器的分类

- 按照电路构造：主从式触发器
- 按照响应时钟变化的方式：
    - **脉冲触发式** (pulse-triggered)：当时钟脉冲为 $1$ 时，输入信号控制触发器的状态；当时钟脉冲为 $0$ 时，触发器的状态发生改变
    - **边沿触发式** (edge-triggered)：当时钟脉冲发生正向跳变时，输入信号控制触发器的状态；当时钟脉冲发生反向跳变时，触发器的状态才发生改变
- 按照锁存器的类型：
    - SR 触发器：使用两个 SR 锁存器
    - D 触发器：使用两个 D 锁存器

???+ note

    两种响应时钟变化的方式的区别在于，脉冲触发式所依赖的信号是「连续」的，而边沿触发式所依赖的信号是「离散」的。后者有利于消除输入信号中毛刺信号的影响。

    边沿触发式下的正向跳变是不唯一的，可以被规定为由 $0$ 跳变到 $1$，也可以被规定为由 $1$ 跳变到 $0$。反向跳变只需要和正向跳变相反即可。

### 边沿触发式 D 触发器

由于边沿触发式 D 触发器是当前最广泛使用的触发器，因此我们重点讨论这一种。

根据前文我们知道，边沿触发式触发器可以在正边沿（即由 $0$ 跳变到 $1$）时被触发，也可以在负边沿（即由 $1$ 跳变到 $0$）时被触发。我们给出负边沿触发和正边沿触发的 D 触发器的电路图。请注意，图中的触发器都是主从式触发器。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_8.png" width="70%" style="margin: 0 auto;">
</div>

### 标准图形符号

认识不同类型的锁存器和触发器的标准图形符号是必要的。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_9.png" width="70%" style="margin: 0 auto;">
</div>

大部分符号的含义是显然的。需要说明的有以下几点：

- 在输入或输出端的小圆圈表示该输入是逻辑 $0$ 触发而非逻辑 $1$ 触发
- 对于脉冲触发式触发器，在其输出端前有一个直角符号，称作**延时输出指示器** (postponed output indicator)，表示输出信号在脉冲的结尾发生改变。
- 在输入端 $C$ 的箭头符号称作**动态指示** (dunamic indicator)，表示 $C$ 是一个**动态输入** (dynamic input)。

### 直接输入

以上讨论的对于触发器的操作都是同步操作，即与时钟输入 $C$ 有关的操作。但在实际情况中，很多时候我们需要对触发器进行独立于时钟输入的，即异步的置位和复位。实现触发器异步置位的输入称作**直接置位** (direct set) 或**预置** (preset)，实现触发器异步复位的输入称作**直接复位** (direct reset) 或者**清零** (clear)。

支持直接输入的 D 触发器的功能表和符号如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_10.png" width="70%" style="margin: 0 auto;">
</div>

我们常采用简化符号的形式，可以看到，直接输入 $S$ 和 $R$ 位于代表触发器的矩形框的上下，表明这两个输入与时钟输入 $C$ 无关。

## 时序电路分析



### 输入方程

时序电路的逻辑图由触发器和组合逻辑门构成。用于描述为触发器产生输入信号的布尔函数称作**触发器输入方程** (flip-flop input equation)。

> 举例来说，对于如下的时序电路：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_11.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 其输入方程即为：
>
> - $D_{A} = A X + B X$
> - $D_{B} = \overline{A} X$
> - $Y = (A + B) \overline{X}$

### 状态表

时序电路的输入、输出和触发器状态之间的功能关系可以用一个**状态表** (state table) 列举出来。一个状态表中包含**当前状态** (present state)、**输入** (input)、**下一状态** (next state) 和**输出** (output)。

由于下一状态和输出都由当前状态和输入确定，因此一个状态表需要列举当前状态和输入的所有二进制组合。

> 我们仍然以上一小节中的时序电路为例，可以得到状态表如下：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_12.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 再由状态表，利用卡诺图一类的方法，即可得到输入方程。

输出既依赖于当前状态，也依赖于输入的时序电路，称作 **Mealy 型电路** (Mealy model circuit)；输出只依赖于当前状态的时序电路，称作 **Moore 型电路** (Moore model circuit)。

### 状态图

状态表中的信息也常用状态图的形式加以表示。与 Mealy 型和 Moore 型两种时序电路相对应，状态图的表示方式也有两种。具体来说：

- Mealy 型时序电路状态图
    - 将「输入/输出」标记在有向边上
    - 每个顶点内记录状态
- Moore 型时序电路状态图
    - 将「状态/输出」记录在顶点内
    - 有向边上标记不同输入对应的状态转移

这种描述显然是较为抽象的。我们结合以下两个实例来理解状态图的构造，先看一个 Mealy 型时序电路的例子：

> 第一个例子仍然沿用前文的时序电路，容易知道这是一个 Mealy 型时序电路。其对应的状态图如下：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_13.png" width="70%" style="margin: 0 auto;">
> </div>

再看一个 Moore 型时序电路的例子：

> 考察如下的时序电路，我们一并给出其逻辑图和状态表：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_14.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 容易得到其输入方程为 $D_{A} = A \oplus X \oplus Y$。同时由于输出即为当前状态，故这是一个 Moore 型时序电路。其对应的状态图如下：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_15.png" width="70%" style="margin: 0 auto;">
> </div>

无论是哪一种状态图，都可以帮助我们找到等价状态。如果两个状态对于任意的输入，都得到相同的下一状态和输出，那么我们就称这两个状态是**等价的** (equivalent)。多个等价状态可以合并，从而使得时序电路的分析和设计更加便捷。

???+ note

    事实上，如果两个状态式等价的，不一定要求两个状态在每个输入下的下一状态需要完全一致。只需要保证两者得到的效果是一致的即可（如分别转移到另外两个等价状态，或出现在同一循环上）。

## 触发器定时

定时参数与脉冲触发式和边沿触发式的触发器的操作有关。下图中给出了两种触发器（主从 SR 触发器和负边沿 D 触发器）的参数说明。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_16.png" width="70%" style="margin: 0 auto;">
</div>

使用触发器时，必须考虑触发器对输入的时钟 $C$ 的响应定时。

对于这两种触发器，都有一个称之为**建立时间** (setup time) 的最小时间 $t_{s}$，即让输出发生改变的时钟变化之前，输入 $S$ 和 $R$ 或 $D$ 必须维持一段时间不变。否则，主从触发器的主锁存器将发生错误的变化，而边沿触发器的主锁存器出于中间值，从锁存器复制这个中间值。

同样地，这两种触发器还有一个称之为**保持时间** (hold time) 的最小时间 $t_{h}$，即让输出发生改变的时钟变化之后，输入 $S$ 和 $R$ 或 $D$ 必须维持一段时间不变。否则，主锁存器可能会相应输入而发生变化，在其变化时从锁存器复制该值。

此外，还有一个最小的**时钟脉冲宽度** (clock pusl width) $t_{w}$，以保证主锁存器有足够的时间来正确地捕获输入值。

与反相器类似，触发器的**传播延迟时间** (propagation delay time) $t_{\text{PHL}}, t_{\text{PLH}}, t_{\text{pd}}$ 定义为时钟触发沿与输出稳定为一个新值之间的时间间隔。

## 时序电路定时

对于时序电路，我们还往往关注其**输入到输出的最大延迟** (maximum input-to0ouput delay) 和电路能正常工作的**最大时钟频率** (maximum clock frequency) $f_{\max}$。时钟频率是时钟周期 $t_{p}$ 的倒数，因此最大时钟频率对应于最小时钟周期。

为了确定时钟周期的最小值，我们需要考察两个时钟触发边沿之间的最长延迟，这一般由三部分组成：

- 触发器传播延迟 $t_{\text{pd, FF}}$
- 路径上一系列门产生的组合逻辑延迟 $t_{\text{pd, COMB}}$
- 触发器的建立时间 $t_{s}$

概括性地，边沿触发式和脉冲触发式触发器的延迟图如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_4_17.png" width="70%" style="margin: 0 auto;">
</div>

除了前面提到的三部分外，每条传播路径还有松弛时间 $t_{\text{stack}}$，即在时钟周期内，路径上传播信号所需时间之外的额外时间。于是我们可以得到如下等式：

$$t_{p} = t_{\text{stack}} + (t_{\text{pd, FF}} + t_{\text{pd, COMB}} + t_{s})$$

又为了宝成信号的变化值能够被接受触发器捕获，所有路径的 $t_{\text{stack}}$ 必须为非负值，于是又有：

$$t_{p} \geq \max (t_{\text{pd, FF}} + t_{\text{pd, COMB}} + t_{s}) = t_{p, \min}$$

> 我们用一个例子来展示对 $t_{p}$ 的典型分析方法。
>
> 假设电路中使用的触发器全部相同，$t_{\text{pd}} = 0.2 \mathrm{ns}, t_{s} = 0.1 \mathrm{ns}$，最大的 $t_{\text{pd, COMB}}$ 为 $1.3 \mathrm{ns}$，则根据前述关系有：
>
> $$t_{p} = t_{\text{stack}} + 0.2 + 1.3 + 0.1 = t_{\text{stack}} + 1.6 \mathrm{ns}$$
>
> 为保证 $t_{\text{stack}} \geq 0$，可知 $t_{p} \geq t_{p, \min} = 1.6 \mathrm{ns}$，于是最大频率 $f_{\max} = \frac{1}{1.6 \mathrm{ns}} = 625 \mathrm{MHz}$。

## 同步和亚稳态

在处理异步输入信号时，往往会出现**亚稳态** (metastable)，这通常是介于 0 和 1 之间的一个值。而触发器对这种值的相应往往是不可预测的，于是亚稳态的出现会导致时序电路失效。
