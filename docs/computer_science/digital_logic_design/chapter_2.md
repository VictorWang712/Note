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

通用门指的是可以独自实现所有布尔函数的门类型，即「功能完全的」。因此只需保证与、或、非三种逻辑运算都可以仅用该种通用门实现。理论证明，与非门和或非门都可以实现这一点。

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

- $\overline{X_{1} + X_{2} + \cdots + X_{n}} = \overline{X_{1}} \ \overline{X_{2}} \cdots \overline{X_{n}}$
- $\overline{X_{1} X_{2} \cdots X_{n}} = \overline{X_{1}} + \overline{X_{2}} + \cdots + \overline{X_{n}}$

### 对偶性

这些基本恒等式体现了布尔代数的**对偶性** (duality)。一个布尔表达式的**对偶式** (dual) 可以通过交换与和或运算，交换常量 $0$ 和常量 $1$ 来获得。在基本恒等式表中，每一行的两个式子即互为对偶式。特别的，第 9 式是**自对偶** (self-dual) 的，即其对偶式仍是自身。

???+ warning

    需要注意的是，有些式子的自对偶性并不是显然的，可能需要进行对偶操作后进一步化简才能得到和原式一样的形式。

    一个例子是：$F = A B + A C + B C$，进行对偶操作后得到的式子为 $F' = (A + B) (A + C) (B + C)$，此时要利用分配律化简：$(A + B) (A + C) (B + C) = (A + B C) (B + C) = A B + A C + B C$，才能直观地看出其自对偶性。

### 反函数

函数 $F$ 的反函数 $\overline{F}$，就是在真值表中将 $F$ 的值由 $1$ 变成 $0$，$0$ 变成 $1$。对表达式取反可以通过交换与和或运算，并将每一个变量和常量均取反的方法得到。其正确性是由德摩根定理保证的。

虽然上文给出了求反函数的一般方法，但该方法实际上非常繁琐，实际操作中常用多次德摩根定理进行化简。

> 例：求 $F_{1} = \overline{X} Y \overline{Z} + \overline{X} \ \overline{Y} Z, F_{2} = X (\overline{Y} \ \overline{Z} + Y Z)$ 的反函数。
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

### 表达式化简

当一个布尔等式用逻辑门实现时，每一个项都需要用一个门，项中的每一个变量都对应着门的一个输入。我们将项中的一个变量（或者变量的补）定义为一个**字符** (literal)。不难意识到，字符越少的表达式，其对应的电路就越简单，在实际实现中也就更加便捷与可靠。

## 标准形式

布尔函数的代数形式可以有多种，但有一些特殊的方法可以用来求布尔表达式的**标准形式** (standard form)。标准形式可以使简化布尔表达式的过程更加方便。

标准形式包括**乘积项** (product term) 与**求和项** (sum term)。乘积项是形如 $X \overline{Y} Z$ 这样，由若干变量的与运算组成的逻辑积；求和项是形如 $X + Y + \overline{Z}$ 这样，由若干变量的或运算组成的逻辑和。

### 最小项和最大项

一个真值表定义一个布尔函数。因此，一个自然的想法是通过遍历所有可能情况并进行运算，就能得到这个布尔函数的等价表达式。

第一个方法是：一个布尔函数可以用乘积项的逻辑和来表示，对应这些乘积项函数的值为逻辑 $1$。基于此，我们提出**最小项** (minterm) 这一概念，即所有变量都以原变量或反变量的形式出现，且仅出现一次的乘积项。

举例来说，三变量的最小项如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_11.png" width="70%" style="margin: 0 auto;">
</div>

那么，一个布尔函数可以由真值表中所有使函数取值为 $1$ 的最小项的逻辑和来表示，这样的表达式叫做**最小项之和** (sum of minterm, SOM)。

第二个方法是：一个布尔函数可以用求和项的逻辑积来表示，对应这些求和项函数的值为逻辑 $0$。基于此，我们提出**最大项** (maxterm) 这一概念，即所有变量都以原变量或反变量的形式出现，且仅出现一次的求和项。

举例来说，三变量的最大项如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_12.png" width="70%" style="margin: 0 auto;">
</div>

那么，一个布尔函数可以由真值表中所有使函数取值为 $0$ 的最大项的逻辑积来表示，这样的表达式叫做**最大项之积** (product of maxterm, POM)。

不难发现的一点是，有相同下标的最小项和最大项是互补的，即 $m_{j} = \overline{M_{j}}, M_{j} = \overline{m_{j}}$。

接下来，我们就用一个实例来展示，在已知布尔函数真值表的情况下，如何用最小项之和或者最大项之积来表示该函数。

> 考察一个三变量布尔函数，其完整真值表如下：
>
> |$X$|$Y$|$Z$|$F$|
> |:-:|:-:|:-:|:-:|
> |0|0|0|1|
> |0|0|1|0|
> |0|1|0|1|
> |0|1|1|0|
> |1|0|0|0|
> |1|0|1|1|
> |1|1|0|0|
> |1|1|1|1|
>
> 用最小项之和表示：$F = \overline{X} \ \overline{Y} \ \overline{Z} + \overline{X} Y \overline{Z} + X \overline{Y} Z + X Y Z = m_{0} + m_{2} + m_{5} + m_{7}$
>
> 这种表示形式可以进一步简化为用最小项的十进制下标来表示：$F(X, Y, Z) = \sum m(0, 2, 5, 7)$
>
> 用最大项之积表示：$F = (X + Y + \overline{Z}) (X + \overline{Y} + \overline{Z}) (\overline{X} + Y + Z) (\overline{X} + \overline{Y} + Z) = M_{1} M_{3} M_{4} M_{6}$
>
> 这种表示形式可以进一步简化为用最大项的十进制下标来表示：$F(X, Y, Z) = \prod M(1, 3, 4, 6)$
>
> 进一步地，我们不难发现反函数 $\overline{F} = \sum m(1, 3, 4, 6) = \prod M(0, 2, 5, 7)$

最小项之和与最大项之积两种表示形式，被称作布尔函数的**规范形式** (canonical form)。

???+ warning

    请务必注意「规范形式」和「标准形式」是两种表示方法。

### 积之和

一旦从真值表中得到了函数的最小项之和，下一步就是尝试着简化表达式，看是否可以减少乘积项的数目及乘积项中文字的数目。其结果是一个简化了的**积之和** (sum of product, SOP) 表达式，这是一种布尔函数表达式的标准形式，其中每个乘积项最多包含 $n$ 个文字。

不难意识到，所有积之和表达式都可以对应一个**两级实现** (two-level implementation) 的电路，这样的电路被称作**两级电路** (two-level circuit)。

> 举例来说，积之和表达式 $F = \overline{Y} + \overline{X} Y \overline{Z} + X Y$ 对应的两级电路是：
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_13.png" width="70%" style="margin: 0 auto;">
> </div>

### 和之积

另一种布尔函数表达式的标准形式是**和之积** (product of sum, POS)，即由若干求和项的逻辑乘组成。

???+ warning

    需要注意的是，与积之和中每个乘积项最多有 $n$ 个文字不同，和之积中每个求和项的文字数可以任意多。

不难发现，每个和之积也对应一个二级电路。

> 举例来说，和之积表达式 $F = X (\overline{Y} + Z) (X + Y + \overline{Z})$ 对应的两级电路是：
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_14.png" width="70%" style="margin: 0 auto;">
> </div>

## 两级电路的优化

用于实现布尔函数的逻辑电路的复杂度直接取决于实现该函数的代数表达式的形式，因此自然地，我们化简得到的表达式尽量简单，即进行优化。

但是在讨论具体如何优化前，我们需要先定义什么是「简单」的表达式，什么是「复杂」的表达式，即需要给出一个成本标准。

### 成本标准

第一个标准是**文字成本** (literal cost)，即与表达式中文字的个数。

文字成本的优点在于计算方法简单，但缺点在于不能在所有情况下准确地反映电路的复杂度。

> 例如对于表达式 $G = A B C D + \overline{A} \overline{B} \overline{C} \overline{D} = (\overline{A} + B) (\overline{B} + C) (\overline{C} + D) (\overline{D} + A)$。
>
> 两个表达式的文字成本都是 $8$，但是前者仅有 $2$ 个函数项，后者则有 $8$ 个函数项，故前者的成本低。

为了反映这一差异，我们定义另一种成本标准，**门输入成本** (gate-input cost)，即表达式对应电路中所用门的输入端的个数。

对于和之积或者积之和的表达式，可以通过对表达式中的如下几部分计数以获得门输入成本：

- 全部文字数：来自电路外部的全部门输入个数
- 全部项数：电路内除反相器外的所有门输入个数
- 取反数：电路内的反相器个数

???+ warning

    请注意，最外层的运算结果是直接输出而不需要引脚的，因此不需要再 $+1$！

### 卡诺图

**卡诺图** (Karnaugh map)，或**K-图** (K-map) 是一种重要的用于两级电路优化的方式。

???+ note

    卡诺图不能用于直接用于三级或者更多极电路的优化。另外通过纸笔，卡诺图一般只适用于二变量、三变量和四变量的二级电路优化，原因将在介绍卡诺图结构时说明。

在接下来的讨论中，我们将先讨论如何用卡诺图进行积之和的化简。最后我们将利用形式上的对偶性再单独介绍如何将卡诺图应用到和之积的花间中。

#### 卡诺图的思想

卡诺图的出发点源于布尔代数中的这条定理：$A B + A \overline{B} = A$。现在我们将这条定理推广到更多变量上。

如果两个乘积项中只有一个变量不同，且该变量再一个乘积项中未取反，而在另一个乘积项中取反，则称这两项是**相邻** (adjacent) 的，即相邻项。

> 例如 $X Y \overline{Z}$ 和 $X \overline{Y} \overline{Z}$ 就是相邻项。

那么根据定理 $A B + A \overline{B} = A$，这对相邻项总是可以合并的。

另一个巧妙之处在于，这种性质和格雷码息息相关，格雷码的编码方式便满足了前后两项是相邻项的目的！

从以上分析出发，我们就可以开始介绍卡诺图的结构了。

#### 卡诺图的结构

卡诺图是一张二维表格，其被这样设计：

- 行变量和列变量位于卡诺图的左上方，每一行每一列都标有这些变量的一个二进制组合，这些组合以格雷码排列。
- 行变量和列变量的乘积即为一个最小项，根据该最小项的真值再表格对应处填上 $0$ 或 $1$。

> 我们对二变量、三变量和四变量的表达式分别举一个例子：
>
> $F(A, B) = \sum m(0, 1, 3)$
>
> |$F(A, B)$|$B = 0$|$B = 1$|
> |:-:|:-:|:-:|
> |$A = 0$|$1$|$1$|
> |$A = 1$|$0$|$1$|
>
> $G(A, B, C) = \sum m(1, 3, 4, 5, 6)$
>
> |$G(A, B, C)$|$BC = 00$|$BC = 01$|$BC = 11$|$BC = 10$|
> |:-:|:-:|:-:|:-:|:-:|
> |$A = 0$|$0$|$1$|$1$|$0$|
> |$A = 1$|$1$|$1$|$0$|$1$|
>
> $H(A, B, C, D) = \sum m(0, 1, 2, 4, 5, 6, 8, 9, 10, 12, 13)$
>
> |$H(A, B, C, D)$|$CD = 00$|$CD = 01$|$CD = 11$|$CD = 10$|
> |:-:|:-:|:-:|:-:|:-:|
> |$AB = 00$|$1$|$1$|$0$|$1$|
> |$AB = 01$|$1$|$1$|$0$|$1$|
> |$AB = 11$|$1$|$1$|$0$|$0$|
> |$AB = 10$|$1$|$1$|$0$|$1$|

根据以上例子，我们可以理解为什么使用纸笔分析卡诺图只适用于变量较少的表达式。

进一步地，请回忆格雷码相邻关系的循环性，即最后一项和第一项也是相邻的。请把这一点推广到卡诺图中，这一点在接下来的化简过程中要被利用。

#### 应用卡诺图化简

在画出卡诺图后，我们就要开始利用卡诺图化简了。这一步的核心在于找**矩形** (rectangle)。当然这里的矩形并非一般几何意义上的矩形，而是有其他要求。

卡诺图中的矩形指的是满足以下几个条件的相邻方格的组合：

- 每个方格的值均为 $1$
- 这些方格组成了一个矩形
- 这个矩形的「面积」（即包含的方格数）是 $2$ 的幂次方

特别的，由于我们之前强调了格雷码的循环性，所以卡诺图中的矩形也可以是循环的，即第一行和最后一行、第一列和最后一列也被认为是相邻的。

于是我们要做的第一步，就是框出卡诺图中所有的矩形。

第二步是判断画出的所有矩形是否有多余的。通常情况下，如果一个矩形删去后，剩下的矩形仍然覆盖了所有的 $1$ 方格，那么这个矩形就是多余的，可以被删去。如果两个不同大小的矩形需要删去一个，那么应该保留较大的那个。

???+ note

    事实上，这一步经常会出现的情况是要从两个相同大小的矩形中删去一个。结果上说，无论删去哪一个都是可以的，但这就是导致卡诺图多解的原因。

最后一步就是从卡诺图中读出积之和表达式。如果一个矩形中，包含了某一变量的 $0$ 和 $1$ 两个取值，那么就意味着这一变量的取值并不重要，在化简项中就不用写出这一变量；但如果只包含了某一变量 $X$ 的 $0$，那么化简项中就应该有 $\overline{X}$；如果只包含了某一变量 $X$ 的 $1$，那么化简项中就应该有 $X$。

> 我们沿用前面三变量表达式的例子：$F(A, B, C) = \sum m(1, 3, 4, 5, 6)$。我们先画出这一卡诺图中所有的矩形：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/digital_logic_design/chapter_2_15.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 不难发现矩形 $(1, 3)$ 和矩形 $(6, 4)$ 都不能删去，但是矩形 $(1, 5)$ 和 $(4, 5)$ 二者是可以删去一个的。假设不妨保留矩形 $(1, 5)$，那么剩余的矩形就是 $(1, 3), (6, 4), (1, 5)$，对应的乘积项就分别是 $\overline{A} C, A \overline{C}, \overline{B} C$，所以最后化简结果即为 $F(A, B, C) = \overline{A} C + A \overline{C} + \overline{B} C$。

#### 形式化的化简步骤

如果我们引入「蕴含项」「主蕴含项」和「质主蕴含项」的概念，那么利用卡诺图化简的过程会更加形式化。

我们定义：

- 若函数对某个乘积项的每一个最小项都取值为 $1$，则这个乘积项是函数的一个**蕴含项** (inplicant)。这对应着卡诺图中值为 $1$ 的方格。
- 若从蕴含项 $P$ 中移去任何一个变量，所得的乘积项不再是函数的蕴含项，则称这样的 $P$ 为函数的**主蕴含项** (prime implicant)。这对应着卡诺图中的矩形。
- 若函数的某个最小项只包含在一个主蕴含项中，则这个主蕴含项是必需的，称其为**质主蕴含项** (essential)。这对应着卡诺图中无法删去的矩形。

???+ note

    对于任意一个函数，一定存在主蕴含项，但不一定存在质主蕴含项。例如**周期布尔函数** (cyclic Boolean function)：

    |$F(X, Y, Z, W)$|$ZW = 00$|$ZW = 01$|$ZW = 11$|$ZW = 10$|
    |:-:|:-:|:-:|:-:|:-:|
    |$XY = 00$|$1$|$0$|$0$|$1$|
    |$XY = 01$|$1$|$1$|$0$|$0$|
    |$XY = 11$|$0$|$1$|$1$|$0$|
    |$XY = 10$|$0$|$0$|$1$|$1$|
    
有了这些定义，利用卡诺图化简函数的一般步骤可以形式化地表述为：

- 确定所有的主蕴含项
- 对全部质主蕴含项进行逻辑和
- 再加上其他一些主蕴含项来覆盖剩余的不被质主蕴含项所包含的最小项

???+ note

    在纸笔做题中，我们可以在第一步中从大到小地框定矩形，从而便于后两步的进行。

#### 和之积化简

前述讨论已经给出了利用卡诺图化简得到积之和形式的表达式的系统方法。现在我们在此基础上，讨论利用卡诺图化简得到和之积形式的表达式的方法。

如果我们将化简过程中框选值为 $1$ 的矩形改为框选值为 $0$ 的矩形，那我们就可以得到 $\overline{F}$ 的积之和形式。然后我们只需运用德摩根定理，即取其对偶式并将每个变量取反，就可以得到 $F$ 的和之积的形式。

#### 无关最小项

在前述方法中，我们都基于这样一个隐含的假设，即每个最小项的取值要么是 $1$、要么是 $0$，总之是确定的。但在更多实际情况下，一些函数取值对某些变量的取值组合是不确定的。具体来说有以下两种情况：

- 某些输入组合根本不会出现（例如 BCD 码中没有用到的 6 种组合）
- 某些输入组合会出现，但是我们不考察这些输入组合下的输出结果

对于这两种情况下的输入取值组合，函数输出结果均不确定。这种对于某些输入组合来说输出结果不确定的函数称为**不完全确定函数** (incompletely specified function)，这些函数中没有指定输出的最小项称为**无关最小项** (don't-care condition)。

在应用卡诺图时，我们常将无关最小项对应的方格标记为 $\times$。而在后续的化简过程中，我们可以视需要将其任意的指定为 $0$ 或者 $1$，当然这一指定需要遵循以下两个规则：

- 在一次完整的化简过程中，一旦 $\times$ 的值被指定，就不能再改变
- 应该以产生尽可能多、尽可能大的矩形为目标指定 $\times$ 的值。

???+ note

    从函数原本的作用来看，无关最小项的值是不确定的。但是对于每一个特定的化简，无关最小项的值都是被确定为 $0$ 或 $1$ 的。

#### 卡诺图的意义

介绍完那么长篇幅有关卡诺图的知识，很多读者会产生这样一个疑惑：为了解决一个规范形式表达式化简的问题，卡诺图这一结构似乎有点过于复杂了。事实上也确实如此，在纸笔的做题过程中，卡诺图的便携程度并不比通过对规范形式瞪眼并不断使用 $A B + A \overline{B} = A$ 方便。而且从准确性的角度上来说，在表达式上看漏形如 $A B + A \overline{B} = A$ 的项和在卡诺图中看漏能化简的矩形的可能性也是差不多的。

但敏锐的读者可能会发现，笔者一直强调「纸笔」这个关键词，这也就意味着卡诺图在程序实现上有独特优势。

通过思考我们可以发现，假设我们确定规范形式中的一项，试图找出能和它合并的其他若干项，在表达式中就需要遍历剩下的所有项；但在卡诺图上就只用查看它的相邻项。进一步来说，可以利用类似 BFS 这样的算法来找到卡诺图上所有的矩形，从而进一步化简。这在大规模数据下的时间成本节省是显著的。
