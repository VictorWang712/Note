---
comments: true
---

# 第五章 - 大数定律及中心极限定理

## 大数定律

### 依概率收敛

设 $\{ Y_{n}, n \geq 1 \}$ 为一随机变量序列，$c$ 为一常数。若对任意的 $\epsilon > 0$，都有

$$\lim_{n \to +\infty} P \{ |Y_{n} - c| \geq \epsilon \} = 0$$

成立，则称 $\{ Y_{n}, n \geq 1 \}$ **依概率收敛** (convergence in probability) 于 $c$，记作 $Y_{n} \stackrel{P}{\longrightarrow} c, n \to +\infty$。

一个等价表示是

$$\lim_{n \to +\infty} P \{ |Y_{n} - c| < \epsilon \} = 1$$

依概率收敛的一个重要性质是，设 $X_{n} \stackrel{P}{\longrightarrow} a, Y_{n} \stackrel{P}{\longrightarrow} b, n \to +\infty$，其中 $a, b$ 为两个常数。若二元函数 $g(x, y)$ 在点 $(a, b)$ 处连续，则有

$$g(X_{n}, Y_{n}) \stackrel{P}{\longrightarrow} g(a, b), n \to +\infty$$

### 两个重要不等式

#### 马尔可夫不等式

若随机变量 $Y$ 的 $k$ 阶（原点）矩存在，$k \geq 1$，则对任意的 $\epsilon > 0$，有

$$P \{ |Y| \geq \epsilon \} \leq \frac{E(|Y|^{k})}{\epsilon^{k}}$$

或等价表示为

$$P \{ |Y| < \epsilon \} \geq 1 - \frac{E(|Y|^{k})}{\epsilon^{k}}$$

这一定理被称作**马尔可夫不等式** (Markov inequality)。

???+ abstract "Proof"

    令

    $$Z = \begin{cases}
    \epsilon, & |Y| \geq \epsilon \\
    0, & |Y| < \epsilon
    \end{cases}$$

    则 $Z^{k} \leq |Y|^{k}$，故 $E(Z^{k}) \leq E(|Y|^{k})$。对任意的 $k \geq 1$，注意到 $E(Z^{k}) = \epsilon^{k} P \{ |Y| \geq \epsilon \}$，所以

    $$P \{ |Y| \geq \epsilon \} = \frac{E(Z^{k})}{\epsilon^{k}} \leq \frac{E(|Y|^{k})}{\epsilon^{k}}$$

特别地，当 $Y$ 为取非负值的随机变量且其 $k$ 阶矩存在时，则有

$$P \{ |Y| \geq \epsilon \} \leq \frac{E(Y^{k})}{\epsilon^{k}}$$

#### 切比雪夫不等式

设随机变量 $X$ 的数学期望和方差存在，分别记作 $\mu, \sigma^{2}$，则对任意的 $\epsilon > 0$，有

$$P \{ |X - \mu| \geq \epsilon \} \leq \frac{\sigma^{2}}{\epsilon^{2}}$$

或等价表示为

$$P \{ |X - \mu| < \epsilon \} \geq 1 - \frac{\sigma^{2}}{\epsilon^{2}}$$

这一定理被称作**切比雪夫不等式** (Chebyshev inequality)。

???+ abstract "Proof"

    在马尔可夫不等式中取 $Y = X - \mu, k = 2$ 即可。

### 两个大数定律

设 $\{ X_{i}, i \geq 1 \}$ 为一随机变量序列，若存在常数序列 $\{ c_{n}, n \geq 1 \}$，使得对任意的 $\epsilon > 0$，有

$$\lim_{n \to +\infty} P \left\{ \left| \frac{1}{n} \sum_{i = 1}^{n} X_{i} - c_{n} \right| \geq \epsilon \right\} = 0$$

或等价表示为

$$\lim_{n \to +\infty} P \left\{ \left| \frac{1}{n} \sum_{i = 1}^{n} X_{i} - c_{n} \right| < \epsilon \right\} = 1$$

成立，即当 $n \to +\infty$ 时，有 $\frac{1}{n} \sum_{i = 1}^{n} X_{i} - c_{n} \stackrel{P}{\longrightarrow} 0$，则称堆积变量序列 $\{ X_{i}, i \geq 1 \}$ 服从**弱大数定律** (weak law of large numbers)，简称服从大数定律。

特别地，当 $c_{n} = c, n = 1, 2, \cdots$ 时，可记作

$$\frac{1}{n} \sum_{i = 1}^{n} X_{i} \stackrel{P}{\longrightarrow} c, n \to +\infty$$

#### 伯努利大数定律

设 $n_{A}$ 为 $n$ 重伯努利试验中事件 $A$ 发生的次数，$p, 0< p < 1$ 为事件 $A$ 在每次试验中发生的概率，即 $P(A) = p$，则对任意的 $\epsilon > 0$，有

$$\lim_{n \to +\infty} P \left\{ |\frac{n_{A}}{n} - p| \geq \epsilon \right\} = 0$$

即 $\frac{n_{A}}{n} \stackrel{P}{\longrightarrow} p, n \to +\infty$。这一定理被称作**伯努利大数定律** (Bernoulli law of large numbers)。

???+ abstract "Proof"

    引入随机变量

    $$X_{i} = \begin{cases}
    1, & \text{第 } i \text{ 次试验中事件 } A \text{ 发生} \\
    0, & \text{第 } i \text{ 次试验中事件 } A \text{ 不发生}
    \end{cases}, i = 1, 2, \cdots, n$$

    易见 $n_{A} = \sum_{i = 1}^{n} X_{i}$，且 $X_{1}, X_{2}, \cdots, X_{n}$ 相互独立，均服从参数为 $p$ 的 0-1 分布。从而

    $$E(X_{i}) = p, \text{Var}(X_{i}) = p (1 - p), i = 1, 2, \cdots, n$$

    故 $E \left( \frac{n_{A}}{n} \right) = p, \text{Var} \left( \frac{n_{A}}{n} \right) = \frac{p (1 - p)}{n}$。利用切比雪夫不等式，可得

    $$\begin{aligned}
    P \left\{ \left| \frac{n_{A}}{n} - p \right| \geq \epsilon \right\} & = P \left\{ \left| \frac{n_{A}}{n} - E \left( \frac{n_{A}}{n} \right) \right| \geq \epsilon \right\} \\
    & \leq \frac{\text{Var} \left( \frac{n_{A}}{n} \right)}{\epsilon^{2}} = \frac{p (1 - p)}{n \epsilon^{2}} \to 0, n \to +\infty
    \end{aligned}$$

    再结合 $P \left\{ \left| \frac{n_{A}}{n} - p \right| \geq \epsilon \right\} \geq 0$，即证。

#### 辛钦大数定律

设 $\{ X_{i}, i \geq 1 \}$ 为独立同分布的随机变量序列，且数学期望存在，记为 $\mu$，则对任意的 $\epsilon > 0$，有

$$\lim_{n \to +\infty} P \left\{ \left| \frac{1}{n} \sum_{i = 1}^{n} X_{i} - \mu \right| \geq \epsilon \right\} = 0$$

即 $\frac{1}{n} \sum_{i = 1}^{n} X_{i} \stackrel{P}{\longrightarrow} \mu, n \to +\infty$。这一定理被称作**辛钦大数定律** (Khinchin law of large numbers)。

辛钦大数定律不要求随机变量的方差存在。

注意到当 $\{ X_{i}, i \geq 1 \}$ 为独立同分布的随机变量序列时，若 $h(x)$ 为一连续函数，则 $\{ h(X_{i}), i \geq 1 \}$ 也是独立同分布的。因此辛钦大数定律可以得到以下推论：

设 $\{ X_{i}, i \geq 1 \}$ 为独立同分布的随机变量序列，若 $h(x)$ 为一连续函数，且记 $a = E(|h(X_{1}|) < +\infty$，则对任意的 $\epsilon > 0$，有

$$\lim_{n \to +\infty} P \left\{ \left| \frac{1}{n} \sum_{i = 1}^{n} h(X_{i}) - a \right| \geq \epsilon \right\} = 0$$

即 $\frac{1}{n} \sum_{i = 1}^{n} h(X_{i}) \stackrel{P}{\longrightarrow} a, n \to +\infty$。

## 中心极限定理

### 独立同分布情形

#### 林德伯格-莱维中心极限定理

设 $\{ X_{i}, i \geq 1 \}$ 为独立同分布的随机变量序列，且数学期望 $E(X_{i}) = \mu$ 和方差 $\text{Var}(X_{i}) = \sigma^{2}, \sigma > 0$ 均存在，则对任意的 $x \in \mathbb{R}$，有

$$\begin{aligned}
\lim_{n \to +\infty} P \left\{ \frac{\sum_{i = 1}^{n} - E \left( \sum_{i = 1}^{n} X_{i} \right)}{\sqrt{\text{Var} \left( \sum_{i = 1}^{n} X_{i} \right)}} \leq x \right\} & = \lim_{n \to +\infty} P \left\{ \frac{\sum_{i = 1}^{n} X_{i} - n \mu}{\sigma \sqrt{n}} \leq x \right\} \\
& = \frac{1}{\sqrt{2 \pi}} \int_{-\infty}^{x} e^{-\frac{t^{2}}{x}} \mathrm{d} t = \Phi(x)
\end{aligned}$$

这一定理被称作**林德伯格-莱维中心极限定理** (Lindeberg - Lévy central limit theorem)，也称作**独立同分布的中心极限定理** (central limit theorem for independent identically)。

该定理表明，数学期望为 $\mu$，方差为 $\sigma^{2}$ 的独立同分布的随机变量的部分和 $\sum_{i = 1}^{n} X_{i}$ 的标准化变量 $\frac{\sum_{i = 1}^{n} X_{i} - n \mu}{\sigma \sqrt{n}}$，在当 $n$ 充分大时，近似地服从标准正态分布 $N(0, 1)$，即

$$\frac{\sum_{i = 1}^{n} X_{i} - n \mu}{\sigma \sqrt{n}} \sim N(0, 1), \text{当 } n \text{ 充分大时}$$

#### 棣莫弗-拉普拉斯中心极限定理

将林德伯格-莱维中心极限定理应用到 $n$ 重伯努利试验中，可得如下推论。

设 $n_{A}$ 为在 $n$ 重伯努利试验中事件 $A$ 发生的次数，$p$ 为事件 $A$ 在每次试验中发生的概率，即 $P(A) = p, 0 < p < 1$，则对任意的 $x \in \mathbb{R}$，有

$$\lim_{n \to +\infty} P \left\{ \frac{n_{A} - np}{\sqrt{n p (1 - p)}} \leq x \right\} = \frac{1}{\sqrt{2 \pi}} \int_{-\infty}^{x} e^{-\frac{t^{2}}{x}} \mathrm{d} t = \Phi(x)$$

这一定理被称作**棣莫弗-拉普拉斯中心极限定理** (De Moivre - Laplace central limit theorem)。

???+ abstract "Proof"

    引入随机变量

    $$X_{i} = \begin{cases}
    1, & \text{第 } i \text{ 次试验中事件 } A \text{ 发生} \\
    0, & \text{第 } i \text{ 次试验中事件 } A \text{ 不发生}
    \end{cases}, i = 1, 2, \cdots, n$$

    易见 $n_{A} = \sum_{i = 1}^{n} X_{i}$，且 $X_{1}, X_{2}, \cdots, X_{n}$ 相互独立，均服从参数为 $p$ 的 0-1 分布。从而

    $$E(X_{i}) = p, \text{Var}(X_{i}) = p (1 - p), i = 1, 2, \cdots, n$$

    由林德伯格-莱维中心极限定理即证。

该定理表明，当 $n$ 充分大时，二项分布 $B(n, p)$ 可以用正态分布 $N(np, np(1 - p))$ 来逼近。

### 独立不同分布情形

设 $\{ X_{i}, i \geq 1 \}$ 为相互独立的随机变量序列，其数学期望 $E(X_{i}) = \mu_{i}$，方差 $\text{Var}(X_{i}) = \sigma^{2}, \sigma_{i} > 0, i = 1, 2, \cdots$，如果存在 $\epsilon > 0$，使得

$$\lim_{n \to +\infty} \frac{1}{B_{n}^{2 + \epsilon}} \sum_{i = 1}^{n} E |X_{i} - \mu_{i}|^{2 + \epsilon} = 0$$

其中 $B_{n}^{2} = \sum_{i = 1}^{n} \sigma_{i}^{2}$，那么对于任意的 $x \in \mathbb{R}$，有

$$\lim_{n \to +\infty} P \left\{ \frac{1}{B_{n}} \sum_{i = 1}^{n} (X_{i} - \mu_{i}) \leq x \right\} = \frac{1}{\sqrt{2 \pi}} \int_{-\infty}^{x} e^{-\frac{t^{2}}{x}} \mathrm{d} t = \Phi(x)$$

这一定理被称作**李雅普诺夫中心极限定理** (Lyapunov central limit theorem)。
