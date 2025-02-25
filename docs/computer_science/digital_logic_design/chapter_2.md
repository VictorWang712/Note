---
comments: true
---

# 第二章 - 组合逻辑电路

## 二值逻辑和逻辑门

### 二值逻辑

**二值逻辑** (binary logic) 是二值变量以及对这些变量所施加的数学逻辑运算，逻辑变量取两个不同的离散值。

与二值变量相关联的基本逻辑运算有三种：

- **与** (and) 运算
- **或** (or) 运算
- **非** (and) 运算

其记号与**真值表** (truth table) 如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_1.png" width="70%" style="margin: 0 auto;">
</div>

### 逻辑门

**逻辑门** (logic gate) 是一些处理一个或多个输入信号，产生一个输出信号的电子电路。每个信号的取值为低电平或高电平。

常见的用于分析逻辑电路的图表是**定时图** (timing diagramme)，其横轴代表时间，纵轴代表高低电平之间的变化。

???+ note

    非门通常称为**反相器** (inverter)，其原因可以在定时图中其相应看出，输出信号是对输入信号 $X$ 的取反。

逻辑门的一个重要特性是**门延时** (gate delay)，即输入信号变化引起输出信号相应变化所需要的时间。通常我们用 $t_{G}$ 表示延时大小。

???+ note

    事实上，每种门电路的延时大小都不一样。这与输入端的个数、制作工艺和设计方法有关。进一步地，根据实现逻辑门所使用的技术，门延迟的长短可能与哪一个输入信号发生变化有关。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_2.png" width="70%" style="margin: 0 auto;">
</div>

尽管使用与门、或门、非门三种基础门可以实现所有可能的逻辑电路，但在实际情况中，为了简化电路，我们使用的逻辑门不止基础门。常用的逻辑门如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_3.png" width="70%" style="margin: 0 auto;">
</div>

以上这些逻辑门我们可以分为三类：

- 基础门：与门、或门、非门
- **通用门** (universal gate)：与非门、或非门
- 其它门：异或门、同或门

通用门指的是可以独自实现所有布尔函数的门类型，即“功能完全的”。因此只需保证与、或、非三种逻辑运算都可以仅用该种通用门实现。理论证明，与非门和或非门都可以实现这一点。

???+ note

    有关与非门是通用门的证明：

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_4.png" width="70%" style="margin: 0 auto;">
    </div>

### 逻辑电路的描述方法

- 真值表
- 布尔方程
- 逻辑图
- 定时图

这四种描述方法都可以用于描述相同功能的逻辑电路。

但是对于一个确定的逻辑电路，其对应的真值表和定时图是确定的，但布尔方程可逻辑图并非确定的。这就意味着为了实现相同的功能，我们的逻辑电路设计是存在一定的灵活性的。

## 布尔代数

**布尔代数** (Boolean algebra) 是一种用来处理二进制变量和逻辑运算的代数方法。变量用大写字母来表示，三种基本的逻辑运算分别是与、或、非。

**布尔表达式** (Boolean exxpression) 是一个由二进制变量、常量 $0$ 和 $1$、逻辑运算符号和括号等组成的代数运算式。

**布尔函数** (Boolean function) 可以描述为一个布尔等式，其中依次包括一个代表函数的二进制变量、一个等号以及一个布尔表达式。

### 基本恒等式

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_5.png" width="70%" style="margin: 0 auto;">
</div>

值得注意的是，**德摩根定理** (De Morgan's laws) 可以扩展到更多变量。其一般形式如下：

- $\overline{X_{1} + X_{2} + \cdots + X_{n}} = \overline{X_{1}} \overline{X_{2}} \cdots \overline{X_{n}}$
- $\overline{X_{1} X_{2} \cdots X_{n}} = \overline{X_{1}} + \overline{X_{2}} + \cdots + \overline{X_{n}}$

### 对偶性

这些基本恒等式体现了布尔代数的**对偶性** (duality)。一个布尔表达式的**对偶式** (dual) 可以通过交换与和或运算，交换常量 $0$ 和常量 $1$ 来获得。在基本恒等式表中，每一行的两个式子即互为对偶式。特别的，第 9 式是**自对偶** (self-dual) 的，即其对偶式仍是自身。

???+ warning

    需要注意的是，有些式子的自对偶性并不是显然的，可能需要进行对偶操作后进一步化简才能得到和原式一样的形式。

    一个例子是：$F = A B + A C + B C$，进行对偶操作后得到的式子为 $F' = (A + B) (A + C) (B + C)$，此时要利用分配律化简：$(A + B) (A + C) (B + C) = (A + B C) (B + C) = A B + A C + B C$，才能直观地看出其自对偶性。

### 反函数

函数 $F$ 的反函数 $\overline{F}$，就是在真值表中将 $F$ 的值由 $1$ 变成 $0$，$0$ 变成 $1$。对表达式取反可以通过交换与和或运算，并将每一个变量和常量均取反的方法得到。其正确性是由德摩根定理保证的。

虽然上文给出了求反函数的一般方法，但该方法实际上非常繁琐，实际操作中常用多次德摩根定理进行化简。

> 例：求 $F_{1} = \overline{X} Y \overline{Z} + \overline{X} \overline{Y} Z, F_{2} = X (\overline{Y} \overline{Z} + Y Z)$ 的反函数。
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_6.png" width="70%" style="margin: 0 auto;">
> </div>

更进一步地，求反函数还有一个更加便捷的方法：求出函数的对偶式并将每一个变量取反。

> 同样求前述的 $F_{1}, F_{2}$ 的反函数：
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_7.png" width="70%" style="margin: 0 auto;">
> </div>

### 常用恒等式

从上述基本的运算定理出发，我们可以得到若干常用恒等式：

- $X + XY = X$
- $X Y + X \overline{Y} = X$
- $X + \overline{X} Y = X + Y$

其证明如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_8.png" width="70%" style="margin: 0 auto;">
</div>

利用对偶性，我们不难得到另外三个恒等式：

- $X (X + Y) = X$
- $(X + Y) (X + \overline{Y}) = X$
- $X (\overline{X} + Y) = XY$

我们同样给出其证明：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_9.png" width="70%" style="margin: 0 auto;">
</div>

基于以上恒等式，一个更重要的定理是**一致律定理** (consensus theorem)：

$$X Y + \overline{X} Z + Y Z = X Y + \overline{X} Z$$

其证明也非常重要：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_10.png" width="70%" style="margin: 0 auto;">
</div>

可以注意到，其中最关键的第一步，在于利用 $(X + \overline{X}) = 1$ 引入了 $(X + \overline{X})$，从而实现了裂项。

一致律的对偶式如下：

$$(X + Y) (\overline{X} + Z) (Y + Z) = (X + Y) (\overline{X} + Z)$$