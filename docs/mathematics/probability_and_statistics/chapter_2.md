---
comments: true
---

# 第二章 - 随机变量及其概率分布

## 随机变量

设随机试验的样本空间为 $S$，若 $X = X(e)$ 为定义在样本空间 $S$ 上的实值单值函数，$e \in S$，则称 $X = X(e) 为**随机变量** (random variable)。

下文中，我们约定用大写英文字母 $X, Y, Z, X_{1}, X_{2}, \cdots$ 表示随机变量，小写字母 $x, y, z, x_{1}, x_{2}$ 表示实数。

## 离散型随机变量

若岁间变量的所有可能取值为有限个或可列个，则称此随机变量为**离散型随机变量** (discrete random variable)。

离散型随机变量的统计规律通常用概率分布律来描述。设 $X$ 为离散型随机变量，若其可能取值为 $x_{1}, x_{2}, \cdots, x_{k}, \cdots$，则称

$$P\{ X = x_{k} \} = p_{k}, k = 1, 2, \cdots$$

为 $X$ 的**概率分布律** (probability distribution law) 或**概率分布列** (probability distribution sequence)，简称为 $X$ 的**分布律**或**分布列**。

概率分布律需满足以下两条性质：

1. $p_{k} \geq 0, k = 1, 2, \cdots$
2. $\sum_{k = 1}^{+\infty} p_{k} = 1$

下面介绍几个重要的离散型随机变量的概率分布。

### 0-1 分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = 0 \} = 1 - p, P\{ X = 1 \} = p, 0 < p < 1$$

则称 $X$ 服从参数为 $p$ 的 0-1 分布，也称作**两点分布** (two-point distribution)，记作 $X \sim B(1, p)$。

### 二项分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = k \} = C_{n}^{k} p^{k} (1 - p)^{n - k}, k = 0, 1, 2, \cdots, n, 0 < p < 1, n \geq 1$$

则称 $X$ 服从参数为 $(n, p)$ 的**二项分布** (binomial distribution)，记作 $X \sim B(n, p)$。

设在 $n$ 次独立重复试验中，每个试验都只有两个结果：$A, \overline{A}$，且 $P(A) = p, 0 < p < 1$ 为定值，则称这一系列的试验为 $n$ 重**伯努利** (Bernoulli) 试验。此时，若记 $X$ 为在 $n$ 次试验中 $A$ 发生的次数，则 $X \sim B(n, p)$。

### 泊松分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = k \} = \frac{e^{- \lambda} \lambda^{k}}{k!}, k = 0, 1, 2, \cdots, \lambda > 0$$

则称 $X$ 服从参数为 $\lambda$ 的**泊松分布** (Poisson distribution)，记作 $X \sim P(\lambda)$。

当 $n$ 充分大，$p$ 充分小时，参数为 $(n, p)$ 的二项分布也可用泊松分布近似描述，这是基于以下的数学推导:

???+ abstract "Proof"

    设 $X \sim B(n, p)$，记 $\lambda = np$，则

    $$\begin{aligned}
    C_{n}^{k} p^{k} (1 - p)^{n - k} & = \frac{n!}{k! (n - k)!} p^{k} (1 - p)^{n - k} \\
    & = \frac{n!}{k! (n - k)!} (\frac{\lambda}{n})^{k} (1 - \frac{\lambda}{n})^{n - k} \\
    & = \frac{n (n - 1) \cdots (n - k + 1)}{n^{k}} \cdot \frac{\lambda^{k}}{k!} \cdot \frac{(1 - \frac{\lambda}{n})^{n}}{(1 - \frac{\lambda}{n})^{k}}
    \end{aligned}$$

    当 $n$ 充分大时，

    $$(1 - \frac{\lambda}{n})^{n} \approx e^{-\lambda}, \frac{n (n - 1) \cdots (n - k + 1)}{n^{k}} \approx 1, (1 - \frac{\lambda}{n})^{k} \approx 1$$

    故有

    $$C_{n}^{k} p^{k} (1 - p)^{n - k} \approx \frac{e^{- \lambda} \lambda^{k}}{k!}$$

### 超几何分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = k \} = \frac{C_{a}^{k} C_{b}^{n - k}}{C_{N}^{n}}, k = l_{1}, l_{1} + 1, \cdots, l_{2}, l_{1} = \max \{ 0, n - b \}, l_{2} = \min \{ a, n \}$$

则称 $X$ 服从参数为 $(n, a, N)$ 的**超几何分布** (hypergeometric distribution)，记作 $X \sim H(n, a, N)$。

### 几何分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = k \} = p (1 - p)^{k - 1}, k = 1, 2, \cdots$$

则称 $X$ 服从参数为 $p$ 的**几何分布** (geometric distribution)。

### 帕斯卡分布

若随机变量 $X$ 的概率分布律为

$$P\{ X = k \} = C_{k - 1}^{r - 1} p^{r} (1 - p)^{k - r}, k = r, r + 1, r + 2, \cdots$$

则称 $X$ 服从参数为 $(r, p)$ 的**帕斯卡分布** (Pascal distribution)，也称作**负二项分布** (negative binomial distribution)，记作 $X \sim NB(r, p)$。

## 随机变量的概率分布函数

对于非离散型的随机变量，我们无法用概率分布律描述其概率分布规律，因此我们引入概率分布函数的概念。

设 $X$ 为一随机变量，$x$ 为任意实数，函数

$$F(x) = P\{ X \leq x \}$$

称作随机变量 $X$ 的**概率分布函数** (probability distribution function)，简称**分布函数**。

容易发现，分布函数具有以下性质：

1. $F(x)$ 单调不减。
2. $0 \leq F(x) \leq 1$，且有 $\lim_{a \to -\infty} F(a) = 0, \lim_{b \to +\infty} F(b) = 1$，简记为 $F(-\infty) = 0, F(+\infty) = 1$。
3. $F(x + 0) = F(x)$，即 $F(x)$ 是右连续函数。

换言之，满足以上三条性质的函数就可以作为某随机变量的分布函数。

## 连续型随机变量

对于随机变量 $X$，其分布函数为 $F(x)$，若存在一个非负的实值函数 $f(x), -\infty < x < +\infty$，使得对于任意实数 $x$ 有

$$F(x) = \int_{-\infty}^{x} f(t) \mathrm{d} t$$

则称 $X$ 为**连续性随机变量** (continuous random variable)，$f(x)$ 为 $X$ 的**概率密度函数** (probability density function)，简称为**密度函数**。

容易知道，满足此定义的 $F(x)$ 是连续函数，同时 $f(x)$ 具有以下性质：

1. $f(x) \geq 0$
2. $\int_{-\infty}^{+\infty} f(x) \mathrm{d} x = 1$
3. $\forall x_{1}, x_{2} \in \mathbb{R}, x_{1} < x_{2}, P\{ x_{1} < X \leq x_{2} \} = F(x_{2}) - F(x_{1}) = \int_{x_{1}}^{x_{2}} f(t) \mathrm{d} t$
4. 在 $f(x)$ 的连续点 $x$ 处，$F'(x) = f(x)$

下面介绍几个重要的连续型随机变量的概率分布。

### 均匀分布

若随机变量 $X$ 具有密度函数

$$f(x) = \begin{cases}
\frac{1}{b - a}, x \in (a, b) \\
0, \text{else}
\end{cases}$$

则称 $X$ 服从区间 $(a, b)$ 上的**均匀分布** (uniform distribution)，记作 $X \sim U(a, b)$。其对应的分布函数为

$$F(x) = \begin{cases}
0, x < a \\
\frac{x - a}{b - a}, a \leq x < b \\
1, x \geq b
\end{cases}$$

### 正态分布

若随机变量 $X$ 具有密度函数

$$f(x) = \frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{(x - \mu)^{2}}{2 \sigma^{2}}}, -\infty < x < +\infty, -\infty < \mu < +\infty, \sigma > 0$$

则称 $X$ 服从参数为 $(\mu, \sigma)$ 的**正态分布** (normal distribution)，$X$ 为正态变量，记作 $X \sim N(\mu, \sigma^{2})$。其对应的分布函数为

$$F(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{(t - \mu)^{2}}{2 \sigma^{2}}} \mathrm{d} t$$

有关正态分布满足 $\int_{-\infty}^{+\infty} f(x) \mathrm{d} x = 1$ 的证明是富有技巧性的，展示如下:

???+ abstract "Proof"

    记 $I = \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{(x - \mu)^{2}}{2 \sigma^{2}}} \mathrm{d} x$，作积分变量代换，令 $\frac{x - \mu}{\sigma} = t$，则

    $$I = \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^2}{2}} \mathrm{d} t$$

    于是有

    $$\begin{aligned}
    I^{2} & = \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^2}{2}} \mathrm{d} x \cdot \int_{-\infty}^{+\infty} \frac{1}{\sqrt{2 \pi}} e^{-\frac{y^2}{2}} \mathrm{d} y \\
    & = \int_{-\infty}^{+\infty} \int_{-\infty}^{+\infty} \frac{1}{2 \pi} e^{-\frac{x^{2} + y^{2}}{2}} \mathrm{d} x \mathrm{d} y
    \end{aligned}$$

    将积分变量变换成极坐标形式，得

    $$I^{2} = \int_{0}^{2 \theta} \mathrm{d} \theta \int_{0}^{+\infty} r \cdot \frac{1}{2 \pi} e^{-\frac{r^{2}}{2}} \mathrm{d} r = 1$$

    即得

    $$I = 1$$

正态变量 $X$ 的密度函数 $f(x)$ 具有以下性质：

1. $f(x)$ 关于 $x = \mu$ 对称。
2. $\max_{-\infty < x < +\infty} f(x) = f(\mu) = \frac{1}{\sqrt{2 \pi} \sigma}$
3. $\lim_{|x - \mu| \to +\infty} f(x) = 0$

通常地，我们称参数 $\mu$ 为位置参数，参数 $\sigma$ 为尺度参数。特别地，当 $\mu = 0, \sigma = 1$ 时，此时称 $Z \sim N(0, 1)$ 中的 $Z$ 服从**标准正态分布** (standard normal distribution)，密度函数为 $\phi(x) = \frac{1}{\sqrt{2 \pi}} e^{-\frac{x^{2}}{2}}, -\infty < x < +\infty$，分布函数为 $\Phi(x) = \int_{-\infty}^{x} \frac{1}{\sqrt{2 \pi}} e^{-\frac{t^{2}}{2}} \mathrm{d} t$。

标准正态分布的一个良好且重要的性质是：$\Phi(x) + \Phi(-x) = 1$。

通过变量代换，容易得到当 $X \sim N(\mu, \sigma^{2})$ 时，有 $P\{ a < X < b \} = \Phi(\frac{b - \mu}{\sigma}) - \Phi(\frac{a - \mu}{\sigma})$。因此所有正态函数的概率计算都可以转化为标准正态分布函数的计算。

### 指数分布

若随机变量 $X$ 具有密度函数

$$f(x) = \begin{cases}
\lambda e^{-\lambda x}, x > 0 \\
0, x \leq 0
\end{cases}, \lambda > 0$$

则称 $X$ 服从参数为 $\lambda$ 的**指数分布** (exponential distribution)，记作 $X \sim E(\lambda)$。其对应的分布函数为

$$F(x) = \begin{cases}
1 - e^{-\lambda x}, x > 0 \\
0, x \leq 0
\end{cases}, \lambda > 0$$

指数分布的一个重要性质是：

$$P\{ X > t_{0} + t \} = P\{ X > t_{0} \} \cdot P\{ X > t \}$$

这被称作指数分布的「无记忆性」。

### $\Gamma$ 分布

若随机变量 $X$ 具有密度函数

$$f(x) = \begin{cases}
\frac{\lambda e^{-\lambda x} (\lambda x)^{\alpha - 1}}{\Gamma(\alpha)}, x > 0 \\
0, x \leq 0
\end{cases}, \alpha > 0, \lambda > 0$$

则称 $X$ 服从参数为 $(\alpha, \lambda)$ 的**$\Gamma$ 分布** (Gamma distribution)，记作 $X \sim \Gamma (\alpha, \lambda)$。

其中，$\Gamma (\alpha) = \int_{0}^{+\infty} e^{-x} x^{\alpha - 1} \mathrm{d} x$，且有 $\Gamma(\alpha) = (\alpha - 1) \Gamma (\alpha - 1)$。特别地，当 $n$ 为正整数时，有 $\Gamma (n) = (n - 1)!$。

### 二参数威布尔分布

若随机变量 $X$ 具有密度函数

$$f(x) = \begin{cases}
\frac{\gamma}{\alpha} (\frac{x}{\alpha})^{\gamma - 1} e^{-(\frac{x}{\alpha})^{\gamma}}, x > 0 \\
0, x \leq 0
\end{cases}, \alpha > 0, \lambda > 0$$

则称 $X$ 服从参数为 $(\alpha, \lambda)$ 的**二参数威布尔分布** (Weibull distribution)。

### $\beta$ 分布

若随机变量 $X$ 具有密度函数

$$f(x) = \begin{cases}
\frac{\Gamma (a + b)}{\Gamma (a) \Gamma (b)} x^{\alpha - 1} (1 - x)^{b - 1}, 0 < x < 1 \\
0, \text{else}
\end{cases}, a > 0, b > 0$$

则称 $X$ 服从参数为 $(a, b)$ 的**$\beta$ 分布** (Bamma distribution)，记作 $X \sim \beta (\alpha, \lambda)$。

## 随机变量函数的分布

设 $X$ 为一连续型随机变量，其密度函数为 $f_{X} (x)$，随机变量 $Y = g(X)$。若函数 $y = g(x)$ 为一处处可导的严格单调函数，记 $y = g(x)$ 的反函数为 $x = h(y)$，则 $Y$ 的密度函数为

$$f_{Y} (y) = \begin{cases}
f_{X} (h(y)) \cdot |h'(y)|, y \in D \\
0, y \notin D
\end{cases}$$
