---
comments: true
---

# 第三章 - 多维随机变量及其分布

## 二维离散型随机变量

### 二维离散型随机变量的联合分布

若二维随机变量 $(X, Y)$ 的可能取值为 $(x_{i}, y_{j}), i, j = 1, 2, \cdots$，则称

$$P \{ X = x_{i}, Y = y_{j} \} = p_{ij}, i, j = 1, 2, \cdots$$

为 $(X, Y)$ 的联合概率分布律，简称**联合分布律** (joint distribution law)。

二维离散型随机变量的联合分布律满足：

1. $p_{ij} \geq 0, i, j = 1, 2, \cdots$
2. $\sum_{i} \sum_{j} p_{ij} = 1$

### 二维离散型随机变量的边际分布

设二维离散型随机变量 $(X, Y)$ 的联合分布律为

$$P \{ X = x_{i}, Y = y_{j} \} = p_{ij}, i, j = 1, 2, \cdots$$

注意到 $\{ X = x_{i} \} = \bigcup_{j = 1}^{+\infty} \{ X = x_{i}, Y = y_{j} \}$，且 $\{ X = x_{i}, Y = y_{j} \}, i, j = 1, 2, \cdots$ 两两互不相容，所以

$$P \{ X = x_{i} \} = P \left( \bigcup_{j = 1}^{+\infty} \{ X = x_{i}, Y = y_{j} \} \right) = \sum_{j = 1}^{+\infty} p_{ij} = p_{i \cdot}, i = 1, 2, \cdots$$

同理有

$$P \{ Y = y_{j} \} = \sum_{i = 1}^{+\infty} p_{ij} = p_{\cdot j}, j = 1, 2, \cdots$$

显然有 $p_{i \cdot} \geq 0, p_{\cdot j} \geq 0, \sum_{i} p_{i \cdot} = 1, \sum_{j} p_{\cdot j} = 1$，即 $p_{i \cdot}, i = 1, 2, \cdots$ 与 $p_{\cdot j}, j = 1, 2, \cdots$ 满足概率分布律的性质，它们分别是随机变量 $X$ 与 $Y$ 的概率分布律，称作 $X$ 和 $Y$ 的**边际分布律** (marginal distribution law) 或边缘分布律。

### 二位离散型随机变量的条件分布

设二维离散型随机变量 $(X, Y)$ 的联合分布律为 $P \{ X = x_{i}, Y = y_{j} \} = p_{ij}, i, j = 1, 2, \cdots$，则当 $P \{ Y = y_{j} \} \neq 0$ 时，

$$P \{ X = x_{i} | Y = y_{j} \} = \frac{P \{ X = x_{i}, Y = y_{j} \} }{P \{ Y = y_{j} \} } = \frac{p_{ij}}{p_{\cdot j}}, i = 1, 2, \cdots$$

同理，当 $P \{ X = x_{i} \} \neq 0$ 时，

$$P \{ Y = y_{j} | X = x_{i} \} = \frac{P \{ X = x_{i}, Y = y_{j} \} }{P \{ X = x_{i} \} } = \frac{p_{ij}}{p_{i \cdot}}, j = 1, 2, \cdots$$

称上式为给定 $\{ Y = y_{j} \}$（或 $\{ X = x_{i} \}$）的条件下 $X$（或 $Y$）的**条件分布律** (conditional distribution law)。

同时，上式中显然有 $\frac{p_{ij}}{p_{\cdot j}} \geq 0$ 且 $\sum_{i = 1}^{+\infty} \frac{p_{ij}}{p_{\cdot j}} = 1$，$\frac{p_{ij}}{p_{i \cdot}} \geq 0$ 且 $\sum_{j = 1}^{+\infty} \frac{p_{ij}}{p_{i \cdot}} = 1$，即满足概率分布律的性质。

## 二维随机变量的分布函数

### 二维随机变量的联合分布函数

设二维随机变量 $(X, Y)$，对于任意的实数 $x, y$，称函数

$$F(x, y) = P \{ X \leq x, Y \leq y \}$$

作 $(X, Y)$ 的联合概率分布函数，简称**联合分布函数** (joint distribution function)。

与以为随机变量的分布函数相类似，$F(x, y)$ 具有以下性质：

1. 当给定 $x = x_{0}$ 时，$F(x_{0}, y)$ 关于 $y$ 单调不减；当给定 $y = y_{0}$ 时，$F(x, y_{0})$ 关于 $x$ 单调不减。
2. $0 \leq F(x, y) \leq 1$，且 $F(x, -\infty) = F(-\infty, y) = F(-\infty, -\infty) = 0$，$F(+\infty, +\infty) = 1$。
3. $F(x, y) = F(x + 0, y), F(x, y) = F(x, y + 0)$，即 $F(x, y)$ 关于 $x$ 右连续，关于 $y$ 右连续。
4. 当实数 $x_{2} > x_{1}, y_{2} > y_{1}$ 时，$F(x_{2}, y_{2}) - F(x_{1}, y_{2}) - F(x_{2}, y_{1}) + F(x_{1}, y_{1}) = P \{ x_{1} < X \leq x_{2}, y_{1} < Y \leq y_{2} \} \geq 0$。

### 二维随机变量的边际分布函数

记二维随机变量 $(X, Y)$ 的联合分布函数为 $F(x, y)$，称函数

$$\begin{aligned}
F_{X} (x) = P \{ X \leq x \} = P \{ X \leq x, Y < +\infty \} = F(x, +\infty) \\
F_{Y} (y) = P \{ Y \leq y \} = P \{ Y \leq y, X < +\infty \} = F(+\infty, y)
\end{aligned}$$

为 $X, Y$ 的边际概率分布函数，简称**边际分布函数** (marginal distribution function)。即二位随机变量的边际分布函数是联合分布函数当另一个变量趋于 $+\infty$ 时的极限函数。

### 条件分布函数

设 $(X, Y)$ 为二维离散型随机变量，当 $P \{ X = x_{i} \} \neq 0$ 时，称函数

$$F_{Y | X} (y | x_{i}) = P \{ Y \leq y | X = x_{i} \}$$

为给定 $\{ X = x_{i} \}$ 的条件下 $Y$ 的条件概率分布函数，简称条件分布函数。

设 $(X, Y)$ 为二维连续型随机变量，对任意给定的实数 $x$，若 $P \{ x < X \leq x + \delta \} > 0$，其中 $\delta > 0$，对任意实数 $y$，称函数

$$F_{Y | X} (y | x) = \lim_{\delta \to 0^{+}} P \{ Y \leq y | x < X \leq x + \delta \}$$

为给定 $\{ X = x \}$ 的条件下 $Y$ 的条件分布函数。

一般地，设 $(X, Y)$ 为二维随机变量，对给定的实数 $x$，若极限

$$\lim_{\delta \to 0^{+}} P \{ Y \leq y | x - \delta < X \leq x + \delta \} = \lim_{\delta \to 0^{+}} P \{ Y \leq y, x - \delta < X \leq x + \delta \}$$

对任意实数 $y$ 均存在，则称函数

$$F_{Y | X} (y | x) = \lim_{\delta \to 0^{+}} P \{ Y \leq y | x - \delta < X \leq x + \delta \}$$

为给定 $\{ X = x \}$ 的条件下 $Y$ 的条件分布函数。

## 二维连续型随机变量

### 二维连续型随机变量的联合分布

设二维随机变量 $(X, Y)$ 的联合分布函数为 $F(x, y)$，若存在二元非负函数 $f(x, y)$，使对任意的实数 $x, y$ 有

$$F(x, y) = \int_{-\infty}^{x} \int_{-\infty}^{x} f(u, v) \mathrm{d} u \mathrm{d} v$$

则称 $(X, Y)$ 为**二维连续型随机变量** (bivariate continuous random variable)，称 $f(x, y)$ 为 $(X, Y)$ 的**联合概率密度函数** (joint probability density function)，简称联合密度函数。

$f(x, y)$ 具有以下性质：

1. $f(x, y) \geq 0$。
2. $\int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} f(x, y) \mathrm{d} x \mathrm{d} y = F(+\infty, +\infty) = 1$。
3. 在 $f(x, y)$ 的连续点处有 $\frac{\partial^{2} F(x, y)}{\partial x \partial y} = f(x, y)$。
4. $(X, Y)$ 落入 $xOy$ 平面任一区域 $D$ 的概率为 $P \{ (X, Y) \in D \} = \iint_{D} f(x, y) \mathrm{d} x \mathrm{d} y$。

从几何含义上说，$f(x, y)$ 使描述二维随机变量 $(X, Y)$ 落在点 $(x, y)$ 附近的概率大小的一个量。

### 二维连续型随机变量的边际分布

设 $(X, Y)$ 为二维连续型随机变量，$F(x, y), f(x, y)$ 分别为 $(X, Y)$ 的联合分布函数和联合密度函数，称单个随机变量 $X$（或 $Y$）的密度函数为 $X$（或 $Y$）的**边际概率密度函数** (marginal probability density function)，简称**边际密度函数**，常分别用 $f_{X} (x), f_{Y} (y)$ 表示。

由于

$$\begin{aligned}
F_{X} (x) & = P \{ X \leq x \} = P \{ X \leq x, Y \in (-\infty, +\infty) \} \\
& = \int_{-\infty}^{x} \left[ \int_{-\infty}^{+\infty} f(x, y) \mathrm{d} y \right] \mathrm{d} x
\end{aligned}$$

由连续型随机变量的定义置 $X$ 为连续型随机变量，且 $X$ 的边际密度函数为

$$f_{X} (x) = \int_{-\infty}^{+\infty} f(x, y) \mathrm{d} y$$

同理有

$$f_{Y} (y) = \int_{-\infty}^{+\infty} f(x, y) \mathrm{d} x$$

即边际密度函数为联合密度函数关于另一个变量在 $(-\infty, +\infty)$ 上的积分。

### 二维连续型随机变量的条件分布

设 $(X, Y)$ 为二维连续型随机变量，$f(x, y)$ 为 $(X, Y)$ 的联合密度函数，$f_{X} (x), f_{Y} (y)$ 为 $X, Y$ 的边际密度函数。则函数

$$f_{Y | X} (y | x) = \frac{f(x, y)}{f_{X} (x)}, -\infty < y < +\infty$$

为给定 $\{ X = x \} (f_{X} (x) \neq 0)$ 的条件下 $Y$ 的**条件概率密度函数** (conditional probability density function)，简称条件密度函数。

同理，给定 $\{ Y = y \} (f_{Y} (y) \neq 0)$ 的条件下 $X$ 的条件密度函数为

$$f_{X | Y} (x | y) = \frac{f(x, y)}{f_{Y} (y)}, -\infty < x < +\infty$$

### 二元均匀分布

设二维随机变量 $(X, Y)$ 在二维有界区域 $D$ 上取值，且具有联合密度函数

$$f(x, y) = \begin{cases}
\frac{1}{D \text{ 的面积}}, & (x, y) \in D \\
0, & \text{else}
\end{cases}$$

则称 $(X, Y)$ 服从 $D$ 上均匀分布。

### 二元正态分布

设二维随机变量 $(X, Y)$ 具有联合密度函数

$$f(x, y) = \frac{1}{2 \pi \sigma_{1} \sigma_{2} \sqrt{1 - \rho^{2}}} \exp \left\{ -\frac{1}{2(1 - \rho^{2})} \left[ \frac{(x - \mu_{1})^{2}}{\sigma_{1}^{2}} - 2 \rho \frac{(x - \mu_{1}) (y - \mu_{2})}{\sigma_{1} \sigma_{2}} + \frac{(y - \mu_{2})^{2}}{\sigma_{2}^{2}} \right] \right\}$$

其中 $-\infty < \mu_{1} < +\infty, -\infty < \mu_{2} < +\infty, \sigma_{1} > 0, \sigma_{2} > 0, |\rho| < 1$，则称 $(X, Y)$ 服从参数为 $(\mu_{1}, \mu_{2}; \sigma_{1}, \sigma_{2}; \rho)$ 的**二元正态分布** (bivariate normal distribution)，记作 $(X, Y) \sim N (\mu_{1}, \mu_{2}; \sigma_{1}^{2}, \sigma_{2}^{2}; \rho)$。

## 随机变量的独立性

对于两个随机变量 $X, Y$，若对任意两个实数集合 $D_{1}, D_{2}$，有

$$P \{ X \in D_{1}, Y \in D_{2} \} = P \{ X \in D_{1} \} \cdot P \{ Y \in D_{2} \}$$

则称随机变量 $X, Y$ 相互独立，简称 $X, Y$ 独立。

这一定义也等价于，对任意实数 $x, y$，有

$$P \{ X \leq x, Y \leq y \} = P \{ X \leq x \} \cdot P \{ Y \leq y \}$$

即 $F(x, y) = F_{X} (x) \cdot F_{Y} (y)$，则 $X, Y$ 相互独立。

当 $(X, Y)$ 为二维离散型随机变量时，$X, Y$ 相互独立等价于

$$p_{ij} = p_{i \cdot} \cdot p_{\cdot j}, i, j = 1, 2, \cdots$$

当 $(X, Y)$ 为二维连续型随机变量时，$X, Y$ 相互独立等价于

$$f(x, y) = f_{X} (x) \cdot f_{Y} (y)$$

据此，我们可以得到一个定理。二维连续型随机变量 $X, Y$ 相互独立的充要条件时 $X, Y$ 的联合密度函数 $f(x, y)$ 几乎处处可写成 $x$ 的函数 $m(x)$ 与 $y$ 的函数 $n(y)$ 的乘积，即

$$f(x, y) = m(x) \cdot n(y), -\infty < x < +\infty, -\infty < y < +\infty$$

## 多元随机变量函数的分布

### $Z = X + Y$ 的分布

若 $(X, Y)$ 为二维离散型随机变量，设 $P \{ X = x_{i}, Y = y_{j} \} = p_{ij}, i, j = 1, 2, \cdots$，又设 $Z$ 的可能取值为 $z_{1}, z_{2}, \cdots, z_{k}, \cdots$，则

$$\begin{aligned}
P \{ Z = z_{k} \} & = P \{X + Y = z_{k} \} \\
& = \sum_{i = 1}^{+\infty} P \{ X = x_{i}, Y = z_{k} - x_{i} \}, k = 1, 2, \cdots \\
& = \sum_{j = 1}^{+\infty} P \{ X = z_{k} - y_{j}, Y = y_{j} \}, k = 1, 2, \cdots
\end{aligned}$$

特别地，当 $X$ 与 $Y$ 相互独立时，上式也可写作

$$\begin{aligned}
P \{ Z = z_{k} \} & = P \{ X = x_{i} \} \cdot P \{ Y = z_{k} - x_{i} \}, k = 1, 2, \cdots \\
& = P \{ X = z_{k} - y_{j} \} \cdot P \{ Y = y_{j} \}, k = 1, 2, \cdots
\end{aligned}$$

若 $(X, Y)$ 为二维连续型随机变量，设 $(X, Y)$ 的联合密度函数为 $f(x, y)$，则 $Z$ 的分布函数为

$$\begin{aligned}
F_{Z} (z) & = P \{ Z \leq z \} = P \{ X + Y \leq z \} = \iint_{x + y \leq z} f(x, y) \mathrm{d} x \mathrm{d} y \\
& = \int_{-\infty}^{+\infty} \mathrm{d} x \int_{-\infty}^{z - x} f(x, y) \mathrm{d} y \\
& = \int_{-\infty}^{+\infty} \mathrm{d} y \int_{-\infty}^{z - y} f(x, y) \mathrm{d} x
\end{aligned}$$

从而有

$$\begin{aligned}
f_{Z} (z) & = \int_{-\infty}^{+\infty} f(x, z - x) \mathrm{d} x \\
& = \int_{-\infty}^{+\infty} f(z - y, y) \mathrm{d} y
\end{aligned}$$

特别地，当 $X$ 与 $Y$ 相互独立时，上式也可写作

$$\begin{aligned}
f_{Z} (z) & = \int_{-\infty}^{+\infty} f_{X} (x) \cdot f_{Y} (z - x) \mathrm{d} x \\
& = \int_{-\infty}^{+\infty} f_{X} (z - y) \cdot f_{Y} (y) \mathrm{d} y
\end{aligned}$$

根据以上定义，可以推出两个重要分布的性质：

- $n$ 个相互独立的服从泊松分布的随机变量之和仍服从泊松分布，其参数为 $n$ 个分布的参数之和。
- $n$ 个相互独立的正态变量的线性组合仍为正态变量。

### $M = \max \{ X, Y \}, N = \min \{ X, Y \}$ 的分布

记 $X, Y$ 的联合分布函数为 $F(x, y)$，且记 $F_{X} (t), F_{Y} (t)$ 分别为 $X, Y$ 的边际分布函数。

由 $M$ 的定义可知

$$F_{M} (t) = P \{ \max \{ X, Y \} \leq t \} = P \{ X \leq t, Y \leq t \} = F(t, t)$$

特别地，当 $X$ 与 $Y$ 相互独立时，上式也可写作

$$F_{M} (t) = F_{X} (t) \cdot F_{Y} (t)$$

由 $N$ 的定义可知

$$\begin{aligned}
F_{N} (t) & = P \{ \min \{ X, Y \} \leq t \} = P \{ (X \leq t) \cup (Y \leq t) \} = F_{X} (t) + F_{Y} (t) - F(t, t) \\
& = 1 - P \{ \min \{ X, Y \} > t \} = 1 - P \{ X > t, Y > t \}
\end{aligned}$$

特别地，当 $X$ 与 $Y$ 相互独立时，上式也可写作

$$\begin{aligned}
F_{N} (t) & = F_{X} (t) + F_{Y} (t) - F_{X} (t) \cdot F_{Y} (t) \\
& = 1 - [1 - F_{X} (t)] \cdot [1 - F_{Y} (t)]
\end{aligned}$$
