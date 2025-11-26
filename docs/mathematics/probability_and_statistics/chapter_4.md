---
comments: true
---

# 第四章 - 随机变量的数字特征

## 数学期望

### 数学期望的定义

设离散型随机变量 $X$ 的概率分布律为 $P \{ X = x_{i} \} = p_{i}, i = 1, 2, \cdots$，若级数 $\sum_{i = 1}^{+\infty} x_{i} p_{i}$ 绝对收敛，即 $\sum_{i = 1}^{+\infty} |x_{i}| p_{i} < +\infty$，则称级数 $\sum_{i = 1}^{+\infty} x_{i} p_{i}$ 为随机变量 $X$ 的**数学期望** (mathematical expectation) 或**均值** (mean)，简称期望，记作 $E(X)$，即

$$E(X) = \sum_{i = 1}^{+\infty} x_{i} p_{i}$$

若 $\sum_{i = 1}^{+\infty} |x_{i}| p_{i} = +\infty$，则称随机变量 $X$ 的数学期望不存在。

设连续型随机变量 $X$ 的密度函数为 $f(x)$。若 $\int_{-\infty}^{+\infty} |x| f_{x} \mathrm{d} x < +\infty$，则称积分 $\int_{-\infty}^{+\infty} x f(x) \mathrm{d} x$ 为 $X$ 的数学期望或均值，简称期望，记作 $E(X)$，即

$$E(X) = \int_{-\infty}^{+\infty} x f(x) \mathrm{d} x$$

若 $\int_{-\infty}^{+\infty} |x| f_{x} \mathrm{d} x = +\infty$，则称随机变量 $X$ 的数学期望不存在。

#### 泊松分布的数学期望

设随机变量 $X$ 服从泊松分布 $P(\lambda), \lambda > 0$，则

$$\begin{aligned}
E(X) & = \sum_{k = 0}^{+\infty} k \cdot \frac{\lambda^{k}}{k!} e^{-\lambda} \\
& = \lambda \sum_{k = 1}^{+\infty} \frac{\lambda^{k - 1}}{(k - 1)!} e^{-\lambda} \\
& = \lambda
\end{aligned}$$

#### 指数分布的数学期望

设随机变量 $X$ 服从指数分布 $E(\lambda), \lambda > 0$，则

$$\begin{aligned}
E(X) & = \int_{0}^{+\infty} x \lambda e^{-\lambda x} \mathrm{d} x \\
& = -\int_{0}^{+\infty} x \mathrm{d} e^{-\lambda x} \\
& = \left. -(x e^{-\lambda x}) \right|_{0}^{+\infty} + \int_{0}^{+\infty} e^{-\lambda x} \mathrm{d} x \\
& = \frac{1}{\lambda}
\end{aligned}$$

#### 标准正态分布的数学期望

设随机变量 $X$ 服从标准正态分布 $N(0, 1)$，则

$$\begin{aligned}
& \phi(x) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^{2}}{2}} \\
& E(X) = \int_{-\infty}^{+\infty} x \phi(x) \mathrm{d} x = 0
\end{aligned}$$

### 随机变量函数的数学期望

当 $X$ 为离散型随机变量时，若 $\sum_{i = 1}^{+\infty} |g(x_{i})| p_{i} < +\infty$，则 $g(X)$ 的数学期望 $E(g(X))$ 存在，且

$$E(g(X)) = \sum_{i = 1}^{+\infty} g(x_{i}) p_{i}$$

其中 $P \{ X = x_{i} \} = p_{i}, i = 1, 2, \cdots$ 为 $X$ 的概率分布律。

当 $X$ 为连续型随机变量时，若 $\int_{-\infty}^{+\infty} |g(x)| f(x) \mathrm{d} x < +\infty$，则 $g(X)$ 的数学期望 $E(g(X))$ 存在，且

$$E(g(X)) = \int_{-\infty}^{+\infty} g(x) f(x) \mathrm{d} x$$

其中 $f(x)$ 为 $X$ 的密度函数。

当 $(X, Y)$ 为二维离散型随机变量时，若实函数 $h(x, y)$ 满足 $\sum_{i = 1}^{+\infty} \sum_{j = 1}^{+\infty} |h(x_{i}, y_{j})| P \{ X = x_{i}, Y = y_{j} \} < +\infty$，则 $h(X, Y)$ 的数学期望 $E(h(X, Y))$ 存在，且

$$E(h(X, Y)) = \sum_{i = 1}^{+\infty} \sum_{j = 1}^{+\infty} h(x_{i}, y_{j}) p_{ij}$$

其中 $P \{ X = x_{i}, Y = y_{j} \} = p_{ij}, i = 1, 2, \cdots, j = 1, 2, \cdots$ 为 $(X, Y)$ 的联合分布律。

当 $(X, Y)$ 为二维连续型随机变量时，若实函数 $h(x, y)$ 满足 $\int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} |h(x, y)| f(x, y) \mathrm{d} x \mathrm{d} y < +\infty$，则 $h(X, Y)$ 的数学期望 $E(h(X, Y))$ 存在，且

$$E(h(X, Y)) = \int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} h(x, y) f(x, y) \mathrm{d} x \mathrm{d} y$$

其中 $f(x, y)$ 为 $(X, Y)$ 的联合密度函数。

### 数学期望的性质

#### 数学期望的线性性

若 $n$ 个随机变量 $X_{1}, X_{2}, \cdots, X_{n}, n \geq 1$ 的数学期望都存在，则对任意 $n + 1$ 个实数 $c_{0}, c_{1}, c_{2}, \cdots, c_{n}$，$c_{0} + \sum_{i = 1}^{n} c_{i} X_{i}$ 的数学期望也存在，且

$$E \left( c_{0} + \sum_{i = 1}^{n} c_{i} X_{i} \right) = c_{0} + \sum_{i = 1}^{n} c_{i} E(X_{i})$$

#### 正态分布的数学期望

设随机变量 $X$ 服从正态分布 $N(\mu, \sigma^{2}), -\infty < \mu < +\infty, \sigma > 0$。由于 $Z = \frac{X - \mu}{\sigma} \sim N(0, 1)$，故 $X = \sigma Z + \mu$，则

$$E(X) = E(\sigma Z + \mu) = \sigma E(Z) + \mu = \mu$$

#### 二项分布的数学期望

设随机变量 $X$ 服从二项分布 $B(n, p), 0 < p < 1$，则

$$E(X) = np$$

#### 独立随机变量的期望乘法性质

$n$ 个相互独立的随机变量乘积的数学期望等于它们的数学期望的乘积。即若随机变量 $X_{1}, X_{2}, \cdots, X_{n}, n \geq 1$ 相互独立，且它们的数学期望都存在，则 $\prod_{i = 1}^{n} X_{i}$ 的数学期望也存在，且

$$E \left( \prod_{i = 1}^{n} X_{i} \right) = \prod_{i = 1}^{n} E(X_{i})$$

### 条件数学期望

条件分布函数的数学期望称作**条件数学期望** (conditional mathematical expectation)，简称为条件期望。

若 $(X, Y)$ 为二维离散型随机变量，在给定 $\{ X = x \}, f_{X} (x) > 0$ 的条件下，$Y$ 的条件分布律为 $P \{ Y = y_{j} | X = x \} = p_{j} (x), j = 1, 2, \cdots$，则在给定 $\{ X = x \}$ 的条件下，$Y$ 的条件期望为

$$E(Y | X = x) = \sum_{i = 1}^{+\infty} y_{j} p_{j} (x)$$

若 $(X, Y)$ 为二维连续型随机变量，在给定 $\{ X = x \}, f_{X} (x) > 0$ 的条件下，$Y$ 的条件密度函数为 $f_{Y | X} (y | x)$，则在给定 $\{ X = x \}$ 的条件下，$Y$ 的条件期望为

$$E(Y | X = x) = \int_{-\infty}^{+\infty} y f_{Y | X} (y | x) \mathrm{d} y$$

$E(Y | X = x)$ 有时也简记为 $E(Y | x)$。

设 $(X, Y)$ 为二维随机变量，若 $E(Y)$ 存在，则

$$E(Y) = E[E(Y|X)]$$

这称作**全期望公式** (total expectation formula)。

当 $(X, Y)$ 为二维离散型随机变量时，即有

$$E(Y) = \sum_{i = 1}^{+\infty} E(Y | X = i) P \{ X = i \}$$

当 $(X, Y)$ 为二维连续型随机变量时，即有

$$E(Y) = \int_{-\infty}^{+\infty} E(Y | X = x) f_{X} (x) \mathrm{d} x$$

## 方差、变异系数

### 方差的定义

设随机变量 $X$ 的数学期望 $E(X)$ 存在，若 $E[(X - E(X))^{2}]$ 存在，则称

$$E[(X - E(X))^{2}]$$

为 $X$ 的**方差** (variance)，记作 $\text{Var}(X)$ 或 $D(X)$。

方差的平方根 $\sqrt{\text{Var}(X)}$ 称作随机变量 $X$ 的**标准差** (standard deviation) 或均方差，记作 $\sigma(X)$ 或 $SD(X)$。

若离散型随机变量 $X$ 的概率分布律为 $P \{ X = x_{i} \} = p_{i}, i = 1, 2, \cdots$，则 $X$ 的方差为

$$\text{Var}(X) = \sum_{i = 1}^{+\infty} (x_{i} - E(X))^{2} p_{i}$$

若连续型随机变量 $X$ 的密度函数为 $f(x)$，则 $X$ 的方差为

$$\text{Var}(X) = \int_{-\infty}^{+\infty} (x - E(X))^{2} f(x) \mathrm{d} x$$

若随机变量 $X$ 的方差存在，则

$$\text{Var}(X) = E(X^{2}) - (E(X))^{2}$$

#### 泊松分布的方差

设随机变量 $X$ 服从泊松分布 $P(\lambda), \lambda > 0$，则

$$\begin{aligned}
E(X^{2}) & = \sum_{k = 0}^{+\infty} k^{2} \cdot \frac{\lambda^{k}}{k!} e^{-\lambda} \\
& = \lambda^{2} + \lambda \\
\text{Var}(X) & = \lambda^{2} + \lambda - \lambda^{2} \\
& = \lambda
\end{aligned}$$

#### 指数分布的方差

设随机变量 $X$ 服从指数分布 $E(\lambda), \lambda > 0$，则

$$\begin{aligned}
E(X^{2}) & = \int_{-\infty}^{+\infty} x^{2} \lambda e^{-\lambda x} \mathrm{d} x \\
& = \frac{2}{\lambda^{2}} \\
\text{Var}(X) & = \frac{2}{\lambda^{2}} - \frac{1}{\lambda^{2}} \\
& = \frac{1}{\lambda^{2}}
\end{aligned}$$

#### 标准正态分布的方差

设随机变量 $X$ 服从标准正态分布 $N(0, 1)$，则

$$\begin{aligned}
E(X^{2}) & = \frac{1}{\sqrt{2 \pi}} \int_{-\infty}^{+\infty} x^{2} e^{-\frac{x^{2}}{2}} \mathrm{d} x \\
& = 1 \\
\text{Var}(X) & = 1 - 0 \\
& = 1
\end{aligned}$$

### 方差的性质

设随机变量 $X$ 的方差存在，$c$ 为某一常数，则

- $\text{Var}(c X) = c^{2} \text{Var}(X)$
- $\text{Var}(X + c) = \text{Var}(X)$
- $\text{Var} \leq E[(X - c)^{2}]$，当且仅当 $E(X) = c$ 时取等
- $\text{Var}(X) = 0$ 当且仅当 $P \{ X = c \} = 1$，其中 $c = E(X)$

设 $X_{1}, X_{2}, \cdots, X_{n}, n \geq 2$ 为两两不相关的随机变量，方差都存在，则 $X_{1} + X_{2} + \cdots + X_{n}$ 的方差也存在，且

$$\text{Var} \left( \sum_{i = 1}^{n} X_{i} \right) = \sum_{i = 1}^{n} \text{Var} (X_{i})$$

进一步地，对任意的有限实数 $c_{0}, c_{1}, \cdots, c_{n}$，$c_{0} + \sum_{i = 1}^{n} c_{i} X_{i}$ 的方差也存在，且

$$\text{Var} \left( c_{0} + \sum_{i = 1}^{n} c_{i} X_{i} \right) = \sum_{i = 1}^{n} c_{i}^{2} \text{Var} (X_{i})$$

#### 二项分布的方差

设随机变量 $X$ 服从二项分布 $B(n, p), 0 < p < 1$，则

$$\text{Var}(X) = n p (1 - p)$$

#### 正态分布的方差

设随机变量 $X$ 服从正态分布 $N(\mu, \sigma^{2}), -\infty < \mu < +\infty, \sigma > 0$。由于 $Z = \frac{X - \mu}{\sigma} \sim N(0, 1)$，故 $X = \sigma Z + \mu$，则

$$\text{Var}(X) = \text{Var}(\sigma Z + \mu) = \sigma^{2} \text{Var}(Z) = \sigma^{2}$$

### 标准化随机变量与变异系数

若随机变量 $X$ 的方差存在，则称

$$X^{*} = \frac{X - E(X)}{\sqrt{\text{Var}(X)}}$$

为 $X$ 的标准化随机变量，简称标准化变量。

显然，$E(X^{*}) = 0, \text{Var}(X^{*}) = 1$，而且此类变量是无量纲的。

进一步地，我们称

$$Cv = \frac{\sqrt{\text{Var}(X)}}{E(X)}$$

为**变异系数** (coefficient of variation)。其反应了随机变量 $X$ 在以它的中心位置为标准时，其值的离散程度。

## 协方差与相关系数

### 协方差

对于数学期望都存在的随机变量 $X$ 和 $Y$，当 $(X - E(X))(Y - E(Y))$ 的数学期望存在时，称

$$\text{Cov}(X, Y) = E[(X - E(X))(Y - E(Y))]$$

为 $X$ 与 $Y$ 的**协方差** (covariance)。

在实际应用中，我们常将其变形为

$$\text{Cov}(X, Y) = E(XY) - E(X) E(Y)$$

以方便计算。

设 $X_{1}, X_{2}, \cdots, X_{n}, n \geq 2$ 为方差存在的随机变量，则 $X_{1} + X_{2} + \cdots + X_{n}$ 的方差也存在，且

$$\text{Var} \left( \sum_{i = 1}^{n} X_{i} \right) = \sum_{i = 1}^{n} \text{Var} (X_{i}) + 2 \sum_{1 \leq i < j \leq n} \text{Cov} (X_{i}, X_{j})$$

若随机变量 $X$ 和 $Y$ 的协方差存在，则

- $\text{Cov}(X, Y) = \text{Cov}(Y, X)$
- $\text{Cov}(X, X) = \text{Var}(X)$
- $\text{Cov}(aX, bY) = a b \text{Cov}(X, Y), a, b \in \mathbb{R}$
- 若 $\text{Cov}(X_{i}, Y), i = 1, 2$ 存在，则 $\text{Cov}(X_{1} + X_{2}, Y) = \text{Cov}(X_{1}, Y) + \text{Cov}(X_{2}, Y)$
- 若 $X$ 和 $Y$ 相互独立，则 $\text{Cov}(X, Y) = 0$，但反之不然
- 当 $\text{Var}(X) \cdot \text{Var}(Y) \neq 0$ 时，有 $(\text{Cov}(X, Y))^{2} \leq \text{Var}(X) \text{Var}(Y)$，当且仅当存在常数 $c_{1}, c_{2}$ 使得 $P \{ Y = c_{1} + c_{2} X \} = 1$，即 $X$ 和 $Y$ 之间有严格的线性关系时取等

### 相关系数

对于随机变量 $X$ 和 $Y$，当 $E(X^{2})$ 与 $E(X^{2})$ 今年存在且 $\text{Var}(X), \text{Var}(Y)$ 均为非零实数时，称

$$\rho_{XY} = \frac{\text{Cov}(X, Y)}{\sqrt{\text{Var}(X)} \sqrt{\text{Var}(Y)}}$$

为 $X$ 与 $Y$ 的**相关系数** (correlation coefficient)，有时也简记为 $\rho$。

根据标准化变量的定义，可知

$$\rho_{XY} = \text{Cov}(X^{*}, Y^{*})$$

其中 $X^{*} = \frac{X - E(X)}{\sqrt{\text{Var}(X)}}, Y^{*} = \frac{Y - E{Y}}{\sqrt{\text{Var}(Y)}}$

对于随机变量 $X$ 和 $Y$，当相关系数 $\rho_{XY}$ 存在时，有

- 若 $X$ 和 $Y$ 相互独立，则 $\rho_{XY} = 0$，但反之不然
- $|\rho_{XY}| \leq 1$，当且仅当存在常数 $c_{1}, c_{2}$ 使得 $P \{ Y = c_{1} + c_{2} X \} = 1$，即 $X$ 和 $Y$ 之间有严格的线性关系时取等

由上可知，相关系数和协方差反映的是变量间「线性」关系的密切程度，因此相关系数有时也称作「线性相关系数」。$|\rho_{XY}|$ 越接近 $1$，则 $X$ 与 $Y$ 之间线性关系的程度就越强；反之两者的线性关系就越弱。

当 $\rho_{XY} > 0$，即 $\text{Cov}(X, Y) > 0$ 时，称 $X$ 与 $Y$ 正相关；反之，当 $\rho_{XY} < 0$ 时，称 $X$ 与 $Y$ 负相关。

### 不相关的定义

当随机变量 $X$ 和 $Y$ 的相关系数

$$\rho_{XY} = 0$$

时，称 $X$ 和 $Y$ **不相关** (uncorrelated) 或零相关。

$X$ 和 $Y$ 不相关的等价定义还有

- $\text{Cov}(X, Y) = 0$
- $E(XY) = E(X) E(Y)$
- $\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y)$

需要说明的是，这里的「不相关」同样指的是「不线性相关」，表示两个随机变量之间不存在线性关系，但可以存在非线性的函数关系。

对于两个相互独立的随机变量，若其方差存在，则一定不相关；但是如果它们不相关，却未必相互独立。反之，若两随机变量相关，则它们一定不独立。

#### 二维正态变量的相关系数

设二维随机变量 $(X, Y)$ 服从二元正态分布 $N(\mu_{1}, \mu_{2}; \sigma_{1}^{2}, \sigma_{2}^{2}; \rho)$，则 $X$ 与 $Y$ 的相关系数

$$\rho_{XY} = \rho$$

当 $\rho = 0$，即 $X$ 与 $Y$ 不相关时，有

$$f(x, y) = f_{X} (x) f_{Y} (y)$$

即 $X$ 和 $Y$ 相互独立。因此对于二维正态变量，两变量不相关等价于两变量相互独立。

## 其他数字特征

### 矩

设 $X, Y$ 为随机变量，$k, l$ 为正整数，如果以下的数学期望都存在，就称

$$\mu_{k} = E(X^{k})$$

为 $X$ 的 $k$ 阶（原点）**矩** (moment)。

称

$$\nu_{k} = E[(X - E(X))^{k}]$$

为 $X$ 的 $k$ 阶中心矩。

称

$$E(X^{k} Y^{l})$$

为 $X$ 和 $Y$ 的 $k + l$ 阶混合（原点）矩。

称

$$E[(X - E(X))^{k} (Y - E(Y))^{l}]$$

为 $X + Y$ 的 $k + l$ 阶混合中心矩。

由以上定义可知，随机变量的数学期望即为其一阶原点矩，随机变量的一阶中心矩恒为 $0$，方差即为二阶中心矩，协方差 $\text{Cov}(X, Y)$ 就是 $X$ 与 $Y$ 的二阶混合中心矩。

### 分位数

设连续型随机变量 $X$ 的分布函数和密度函数分别为 $F(x)$ 与 $f(x)$，对任意的 $0 < \alpha < 1$，称满足条件

$$P \{ X > x_{\alpha} \} = 1 - F(x_{\alpha}) = \int_{x_{\alpha}}^{+\infty} f(x) \mathrm{d} x = \alpha$$

的实数 $x_{\alpha}$ 为随机变量 $X$ 的上 $\alpha$ **分位数** (quantile)。

特别地，当 $\alpha = \frac{1}{2}$ 时，$x_{\frac{1}{2}}$ 称作 $X$ 的**中位数** (median)。

## 多维随机变量的数字特征

### 多维随机变量的数学期望与协方差矩阵

记 $n$ 维随机变量 $\boldsymbol{X} = (X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$，若其每一分量的数学期望都存在，则称

$$E(\boldsymbol{X}) = (E(X_{1}), E(X_{2}), \cdots, E(X_{n}))^{\mathrm{T}}$$

为 $n$ 维随机变量 $\boldsymbol{X}$ 的数学期望。

显然，$n$ 为随机变量的数学期望就是各分量数学期望组成的向量。

记 $n$ 维随机变量 $\boldsymbol{X} = (X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$，若其每一分量的方差都存在，则称

$$\begin{aligned}
\text{Cov}(\boldsymbol{X}) & = E[(\boldsymbol{X} - E(\boldsymbol{X}))(\boldsymbol{X} - E(\boldsymbol{X}))^{\mathrm{T}}] \\
& = (\text{Cov}(X_{i}, X_{j}))_{n \times n} \\
& = \begin{pmatrix}
\text{Var}(X_{1}) & \text{Cov}(X_{1}, X_{2}) & \cdots & \text{Cov}(X_{1}, X_{n}) \\
\text{Cov}(X_{2}, X_{1}) & \text{Var}(X_{2}) & \cdots & \text{Cov}(X_{2}, X_{n}) \\
\vdots & \vdots & \ddots & \vdots \\
\text{Cov}(X_{n}, X_{1}) & \text{Cov}(X_{n}, X_{2}) & \cdots & \text{Var}(X_{n}) \\
\end{pmatrix}
\end{aligned}$$

为 $n$ 维随机变量 $\boldsymbol{X}$ 的**协方差矩阵** (covariance matrix)，简称协方差阵。

一个重要性质是，$n$ 维随机变量 $\boldsymbol{X}$ 的协方差矩阵 $\text{Cov}(\boldsymbol{X})$ 是一个对称的非负定矩阵。

### 多维正态变量

$n$ 维随机变量 $\boldsymbol{X} = (X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$，其每一分量的方差都存在。记 $\boldsymbol{X}$ 的协方差矩阵为 $\boldsymbol{B} = \text{Cov}(\boldsymbol{X})$，数学期望为 $\boldsymbol{a} = E(\boldsymbol{X}) = (E(X_{1}), E(X_{2}), \cdots, E(X_{n}))^{\mathrm{T}}$，则由密度函数

$$f(x) = f(x_{1}, x_{2}, \cdots, x_{n}) = \frac{1}{(2 \pi)^{\frac{n}{2}} |\boldsymbol{B}|^{\frac{1}{2}}} \exp \left[ -\frac{1}{2} (\boldsymbol{x} - \boldsymbol{a})^{\mathrm{T}} \boldsymbol{B}^{-1} (\boldsymbol{x} - \boldsymbol{a}) \right]$$

定义的分布为 $n$ 元正态分布，常记为 $\boldsymbol{X} \sim N(\boldsymbol{a}, \boldsymbol{B})$。

特别地，当 $n = 2$，有 $(X, Y) \sim N (\mu_{1}, \mu_{2}; \sigma_{1}^{2}, \sigma_{2}^{2}; \rho)$ 时，其协方差矩阵为

$$\boldsymbol{B} = \begin{pmatrix}
\sigma_{1}^{2} & \sigma_{1} \sigma_{2} \rho \\
\sigma_{1} \sigma_{2} \rho & \sigma_{2}^{2}
\end{pmatrix}$$

$n$ 元正态分布有如下一些性质：

- $n$ 维正态变量 $(X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$ 中的任意 $k$ 维子向量 $(X_{i_{1}}, X_{i_{2}}, \cdots, X_{i_{k}})^{\mathrm{T}}, 1 \leq k \leq n$ 也服从 $k$ 元正态分布。特别地，$n$ 维正态变量中的每个分量都是服从一元正态分布的。反之，若 $X_{i}, i = 1, 2, \cdots, n$ 都是正态变量，且相互独立，则 $(X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$ 服从 $n$ 元正态分布。
- $\boldsymbol{X} = (X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$ 服从 $n$ 元正态分布的充要条件是其各个分量的任意线性组合均服从一元正态分布。形式化的说，即对任意 $n$ 维实向量 $\boldsymbol{l} = (l_{1}, l_{2}, \cdots, l_{n})^{\mathrm{T}}$，有 $\boldsymbol{X} \sim N(\boldsymbol{a}, \boldsymbol{B}) \Leftrightarrow \boldsymbol{l}^{\mathrm{T}} \boldsymbol{X} = \sum_{i = 1}^{n} l_{i} X_{i} \sim N(\boldsymbol{l}^{\mathrm{T}} \boldsymbol{a}, \boldsymbol{l}^{\mathrm{T}} \boldsymbol{B} \boldsymbol{l})$，其中 $l_{1}, l_{2}, \cdots, l_{n}$ 不全为 $0$。
- 若 $(X_{1}, X_{2}, \cdots, X_{n})^{\mathrm{T}}$ 服从 $n$ 元正态分布，设 $Y_{1}, Y_{2}, \cdots, Y_{k}$ 都是 $X_{1}, X_{2}, \cdots, X_{n}$ 的线性函数，则 $\boldsymbol{Y} = (Y_{1}, Y_{2}, \cdots, Y_{k})^{\mathrm{T}}$ 也服从 $k$ 元正态分布。形式化地说，即若 $\boldsymbol{X} \sim N(\boldsymbol{a}, \boldsymbol{B})$，$\boldsymbol{C} = (c_{ij})_{k \times n}$ 为 $k \times n$ 实数矩阵，则 $\boldsymbol{Y} = \boldsymbol{C} \boldsymbol{X} \sim N(\boldsymbol{C} \boldsymbol{a}, \boldsymbol{C} \boldsymbol{B} \boldsymbol{C}^{\mathrm{T}})$。这一性质常称作「正态变量的线性变换不变性」。
- 服从 $n$ 元正态分布的随机变量 $X$ 中的分量 $X_{1}, X_{2}, \cdots, X_{n}$ 相互独立的充要条件是其两两不相关，也等价于 $\text{Cov}(\boldsymbol{X})$ 为对角矩阵。
