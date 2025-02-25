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

??? note+

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

