---
comments: true
---

# 第七章 - 参数估计

## 点估计

设总体 $X$ 的分布函数为 $F(x; \theta)$，$\theta$ 是待估函数，$X_{1}, X_{2}, \cdots, X_{n}$ 是 $X$ 的一个样本。点估计问题就是要构造一个适当的统计量 $\hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$，用来估计参数 $\theta$，此时称 $\hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$ 为 $\theta$ 的**点估计量** (point estimator)。如果把其中的样本用用样本值 $x_{1}, x_{2}, \cdots, x_{n}$ 代替，就称 $\hat{\theta}(x_{1}, x_{2}, \cdots, x_{n})$ 为 $\theta$ 的一个估计值。

根据不同的统计思想，可以得到不同的点估计方法。下面将介绍两种常用的点估计方法。

### 矩法

**矩法** (moment method) 的主要理论依据为大数定律，即当样本容量 $n \to +\infty$ 时，样本矩依概率收敛于相应的总体矩，即

$$A_{k} \stackrel{P}{\longrightarrow} \mu_{k}, B_{k} \stackrel{P}{\longrightarrow} \nu_{k}$$

其中 $A_{k}, B_{k}$ 分别为样本的 $k$ 阶原点矩和 $k$ 阶中心矩，$\mu_{k}, \nu_{k}$ 分别为总体的 $k$ 阶原点矩和 $k$ 阶中心距。因此，我们可以用样本矩作为相应总体矩的估计，用样本矩的函数作为相应总体矩的同意函数的估计。

设 $\theta_{1}, \theta_{2}, \cdots, \theta_{m}$ 是总体 $X$ 的待估函数，并假定 $X$ 的前 $m, m \geq 1$ 阶矩存在，下面给出利用矩法来求参数估计量的基本步骤：

1. 求总体 $X$ 的前 $m$ 阶原点矩 $\mu_{1}, \mu_{2}, \cdots, \mu_{m}$，一般地，这些矩可以写成待估参数 $\theta_{1}, \theta_{2}, \cdots, \theta_{m}$ 的函数形式，记作

    $$\begin{cases}
    \mu_{1} = E(X) = g_{1}(\theta_{1}, \theta_{2}, \cdots, \theta_{m}) \\
    \mu_{2} = E(X^{2}) = g_{2}(\theta_{1}, \theta_{2}, \cdots, \theta_{m}) \\
    \cdots \\
    \mu_{m} = E(X^{m}) = g_{m}(\theta_{1}, \theta_{2}, \cdots, \theta_{m})
    \end{cases}$$

2. 由上述方程组，可解出各参数关于前 $m$ 阶原点矩 $\mu_{1}, \mu_{2}, \cdots, \mu_{m}$ 的函数表达式，即

    $$\theta_{k} = h_{k}(\mu_{1}, \mu_{2}, \cdots, \mu_{m}), k = 1, 2, \cdots, m$$

3. 根据矩法思想，用 $A_{i}$ 代替 $\mu_{i}, i = 1, 2, \cdots, m$，即可得各参数的估计量为

    $$\hat{\theta}_{k} = h_{k}(A_{1}, A_{2}, \cdots, A_{m}), k = 1, 2, \cdots, m$$

我们称上述求得的 $\hat{\theta}_{k}$ 为参数 $\theta_{k}, k = 1, 2, \cdots, m$ 的**矩估计量** (moment estimator)。

同理，我们也可以使用中心矩进行矩法的点估计。只需将上述过程中的 $\mu_{i}$ 替换为 $\nu_ {i}$，$A_{i}$ 替换为 $B_{i}$ 即可。

### 极大似然法

极大似然法是在参数分布族的场合下使用的一种应用非常广泛的参数估计方法。其基本思想是：设某事件 $A$ 发生的概率依赖于待估参数 $\theta$，如果观察到 $A$ 已经发生，那么就取使得事件 $A$ 发生的概率达到最大的 $\theta$ 的值作为 $\theta$ 的估计。

设 $X$ 为离散型总体，其概率分布律为 $P \{ X = x \} = p(x; \theta), \theta \in \Theta$ 是未知的待估参数，$\Theta$ 为参数可取值的范围，即参数空间。$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本，并设 $x_{1}, x_{2}, \xdots, x_{n}$ 是已经得到的样本值，则样本 $x_{1}, X_{2}, \cdots, X_{n}$ 取到样本值 $x_{1}, x_{2}, \xdots, x_{n}$ 的概率为

$$P \{ X_{1} = x_{1}, X_{2} = x_{2}, \cdots, X_{n} = x_{n} \} = \prod_{i = 1}^{n} P \{ X_{i} = x_{i} \} = \prod_{i = 1}^{n} p(x_{i}; \theta)$$

其为参数 $\theta$ 的函数。对于不同的 $\theta$，这一概率是不相同的。记

$$L(\theta) = L(\theta; x_{1}, x_{2}, \cdots, x_{n}) = \prod_{i = 1}^{n} p(x_{i}; \theta)$$

则称 $L(\theta)$ 为**似然函数** (likelihood function)。基于极大似然法的基本思想，我们应选取 $\theta$ 的估计值 $\hat{\theta}$，使得 $L(\theta)$ 取到最大。于是 $\hat{\theta}$ 需满足

$$L(\hat{\theta}) = L(\hat{\theta}; x_{1}, x_{2}, \cdots, x_{n}) = \max_{\theta \in \Theta} L(\theta; x_{1}, x_{2}, \cdots, x_{n})$$

由此获得的 $\hat{\theta} = \hat{\theta}(x_{1}, x_{2}, \cdots, x_{n})$ 称作参数 $\theta$ 的极大似然估计值，相应的统计量 $\hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$ 称作 $\theta$ 的**极大似然估计量** (maximum likelihood estimation, MLE)。

当 $X$ 为连续型总体时，设其密度函数为 $f(x; \theta), \theta \in \Theta$ 是未知的待估参数，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本，并设 $x_{1}, x_{2}, \cdots, x_{n}$ 是已经得到的样本值。此时，似然函数可定义为

$$L(\theta) = L(\theta; x_{1}, x_{2}, \cdots, x_{n}) = \prod_{i = 1}^{n} f(x_{i}; \theta)$$

其极大似然估计值 $\hat{\theta}$ 可用相同的方式确定，极大似然估计量为相应的统计量 $\hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$。

寻求极大似然估计用常用微分法，即求解

$$\left. \frac{\mathrm{d}L(\theta)}{\mathrm{d}\theta} \right|_{\theta = \hat{\theta}} = 0$$

通常称这一方程为**似然方程** (likelihood equation)。为计算方便，往往对似然函数求对数，记作

$$l(\theta) = \ln L(\theta)$$

称 $l(\theta)$ 为**对数似然函数** (log-likelihood function)，则似然方程等价于

$$\left. \frac{\mathrm{d}l(\theta)}{\mathrm{d}\theta} \right|_{\theta = \hat{\theta}} = 0$$

通常称这一方程为**对数似然方程** (log-likelihood equation)。

当然，根据极大值的充分条件，往往还需要验证似然函数或对数似然蛤属关于待估参数的二阶导数是否小于零。

当似然方程的解不存在时，我们往往根据似然函数关于待估函数的单调性来求其极大似然估计。

极大似然估计具有不变性，即设参数 $\theta$ 的极大似然估计为 $\hat{\theta}, \theta^{*} = g(\theta)$ 是 $\theta$ 的连续函数，则参数 $\theta^{*}$ 的极大似然估计为 $\hat{\theta^{*}} = g(\hat{\theta})$。

## 估计量的评价准则

从上一节的讨论可知，对总体的同意参数，采用不同的估计方法得到的估计量可能是不一样的，这就意味着需要一个选择「较好」的估计量的准则。本节将讨论四个估计量的评价准则。

### 无偏性准则

一个自然的评价标准是，要求估计量无系统偏差，即要求在大量重复抽样时，所有估计值的平均应与待估参数的真值相同，这就是无偏性准则。

设 $\theta \in \Theta$ 是总体 $X$ 的待估参数，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本。若估计量 $\hat{\theta} = \hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$ 的数学期望存在，且满足

$$E(\hat{\theta}) = \theta, \forall \theta \in \Theta$$

则称 $\hat{\theta}$ 是 $\theta$ 的**无偏估计量**或**无偏估计** (unbiased estimator)。

若 $E(\hat{\theta}) \neq \theta$，则称 $E(\hat{\theta}) - \theta$ 为估计量 $\hat{\theta}$ 的**偏差** (bias)。

若 $E(\hat{\theta}) \neq \theta$，但满足 $\lim_{n \to +\infty} E(\hat{\theta}) = \theta$，则称 $\hat{\theta}$ 是 $\theta$ 的**渐进无偏估计** (asymptotic unbiased estimator)。

### 有效性准则

在有些情况下，同一总体参数的无偏估计量是不唯一的。为比较两个无偏估计量的好坏，我们需进一步考察估计量取值的波动性，即估计量的方差。无偏估计量的方差越小，说明该估计量的取值越集中在参数真值的附近。

设 $\hat{\theta}_{1} = \hat{\theta}_{1} (X_{1}, X_{2}, \cdots, X_{n})$ 与 $\hat{\theta}_{2} = \hat{\theta}_{2} (X_{1}, X_{2}, \cdots, X_{n})$ 都是参数 $\theta$ 的无偏估计，若 $\forall \theta \in \Theta, \text{Var}_{\theta}(\hat{\theta}_{1}) \leq \text{Var}_{\theta}(\hat{\theta}_{2})$，且至少有一个 $\theta \in \Theta$ 使不等号成立，则称 $\hat{\theta}_{1}$ 比 $\hat{\theta}_{2}$ 有效。

### 均方误差准则

设 $\hat{\theta} = \hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$ 是总体参数 $\theta$ 的估计量，称 $E[(\hat{\theta} - \theta)^{2}]$ 是估计量 $\hat{\theta}$ 的均方误差，记作 $\text{Mse}(\hat{\theta})$。

一个常用于计算 $\text{Mse}(\hat{\theta})$ 的公式为

$$\text{Mse}(\hat{\theta}) = \text{Var}(\hat{\theta}) + [\text{Bias}(\hat{\theta})]^{2}$$

???+ abstract "Proof"

    已知

    $$\text{Var}(\hat{\theta}) = E[(\hat{\theta} - E(\hat{\theta}))^{2}], \text{Bias}(\hat{\theta}) = E(\hat{\theta}) - \theta$$

    则

    $$\begin{aligned}
    \text{Mse}(\hat{\theta}) & = E[(\hat{\theta} - \theta)^{2}] \\
    & = E[(\hat{\theta} - E(\hat{\theta}) + E(\hat{\theta}) - \theta)^{2}] \\
    & = E[(\hat{\theta} - E(\hat{\theta}))^{2}] + 2E[(\hat{\theta} - E(\hat{\theta}))(E(\hat{\theta}) - \theta)] + E[(E(\hat{\theta}) - \theta)^{2}]
    \end{aligned}$$

    其中
    
    $$E[(\hat{\theta} - E(\hat{\theta}))(E(\hat{\theta}) - \theta)] = (E(\hat{\theta}) - \theta) \cdot E[\hat{\theta} - E(\hat{\theta})] = (E(\hat{\theta}) - \theta) \cdot 0 = 0$$
    
    且 $E(\hat{\theta}) - \theta$ 为常数。故

    $$\begin{aligned}
    \text{Mse}(\hat{\theta}) & = E[(\hat{\theta} - E(\hat{\theta}))^{2}] + 2E[(\hat{\theta} - E(\hat{\theta}))(E(\hat{\theta}) - \theta)] + E[(E(\hat{\theta}) - \theta)^{2}] \\
    & = \text{Var}(\hat{\theta}) + [\text{Bias}(\hat{\theta})]^{2}
    \end{aligned}$$

设 $\hat{\theta}_{1}$ 和 $\hat{\theta}_{2}$ 都是 $\theta$ 的估计量，若对于任意 $\theta \in \Theta, \text{Mse}(\hat{\theta}_{1}) \leq \text{Mse}(\hat{\theta}_{2})$，且至少存在某个 $\theta$ 使得不等号成立，则称在均方误差准则下，$\hat{\theta}_{1}$ 优于 $\hat{\theta}_{2}$。

有定义可知，若 $\hat{\theta}$ 是参数 $\theta$ 的无偏估计量，则 $\text{Mse}(\hat{\theta}) = \text{Var}(\hat{\theta})$。均方误差准则常用于有偏估计之间，或有偏估计与无偏估计之间的比较。若仅限于无偏估计之间的比较，则等价于有效性准则。

### 相合性准则

前面三个准则都是在样本容量 $n$ 固定的情况下讨论的。然而，由于估计量 $\hat{\theta}$ 依赖于样本容量 $n$，自然会想到，一个好的估计量，当样本容量 $n$ 越大时，应该越精确可靠。特别是当 $n \to +\infty$ 时，估计量的取值与参数真值应几乎完全一致，这就是股价零的相合性，或一致性。相合性的严格定义如下：

设 $\hat{\theta}_{n} = \hat{\theta}(X_{1}, X_{2}, \cdots, X_{n})$ 是总体参数 $\theta$ 的估计量，若对任意 $\epsilon > 0$，有

$$\lim_{n \to +\infty} P \{ |\hat{\theta}_{n} - \theta| < \epsilon \} = 1$$

即 $\hat{\theta}_{n}$ 依概率收敛于 $\theta$，则称 $\hat{\theta}_{n}$ 是 $\theta$ 的**相合统计量** (consistent estimator)，并记作 $\hat{\theta}_{n} \stackrel{P}{\longrightarrow} \theta, n \to +\infty$。

一般地，由矩法求得的参数估计量都满足相合性。对于极大似然估计，在总体分布满足一定的条件下，求得的估计量也是待估参数的相合估计量。

## 区间估计

人们常常根据点估计对总体参数作出判断，但点估计无法确定这种判断的有效性。为此，我们提出区间估计来解决这一问题。

### 置信区间的定义

设总体为 $X, \theta \in \Theta$ 为待估参数，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本，统计量 $\hat{\theta}_{L} = \hat{\theta}_{L}(X_{1}, X_{2}, \cdots, X_{n})$ 和 $\hat{\theta}_{U} = \hat{\theta}_{U}(X_{1}, X_{2}, \cdots, X_{n})$ 满足 $\hat{\theta}_{L} < \hat{\theta}_{U}$，且对给定的 $\alpha \in (0, 1)$ 和任意的 $\theta \in \Theta$，有

$$P \{ \hat{\theta}_{L} < \theta < \hat{\theta}_{U} \} \geq 1 - \alpha$$

则称随机区间 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 是参数 $\theta$ 的**置信水平** (confidence level) 为 $1 - \alpha$ 的**置信区间** (confidence interval)，$\hat{\theta}_{L}$ 和 $\hat{\theta}_{U}$ 分别称作 $\theta$ 的置信水平是 $1 - \alpha$ 的双侧**置信下限** (lower confidence limit) 和**置信上限** (upper confidence limit)。

称区间的平均长度 $E(\hat{\theta}_{U} - \hat{\theta}_{L})$ 为置信区间 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 的精确度，并称区间平均长度的一半 $\frac{E(\hat{\theta}_{U} - \hat{\theta}_{L})}{2}$ 为置信区间的**误差限** (error limit)。

奈曼原则指出，在保证置信水平达到一定的前提下，应当尽可能提高精确度。因此，当总体 $X$ 是连续型随机变量是，对于给定的置信水平 $1 - \alpha$，我们应选择使等号刚好成立时，即

$$P \{ \hat{\theta}_{L} < \theta < \hat{\theta}_{U} \} = 1 - \alpha$$

的随机区间 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 作为参数 $\theta$ 的置信区间；而当总体 $X$ 是离散型随机变量时，则应选择使 $P \{ \hat{\theta}_{L} < \theta < \hat{\theta}_{U} \}$ 尽可能接近 $1 - \alpha$ 的随机区间 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 作为参数 $\theta$ 的置信区间。

在实际应用中，通常取 $\alpha = 0.1$ 或 $0.05$。

在一些实际问题中，人们只关注未知参数的置信下限或置信上限。对这些问题，我们只需给出单侧的置信限形式。

对给定的 $\alpha \in (0, 1)$，如果统计量 $\hat{\theta}_{L}$ 和 $\hat{\theta}_{U}$ 满足

$$\begin{aligned}
P \{ \hat{\theta}_{L} < \theta \} \geq 1 - \alpha, \theta \in \Theta \\
P \{ \hat{\theta}_{U} > \theta \} \geq 1 - \alpha, \theta \in \Theta
\end{aligned}$$

则分别称 $\hat{\theta}_{L}$ 和 $\hat{\theta}_{U}$ 是参数 $\theta$ 的置信水平为 $1 - \alpha$ 的**单侧置信下限** (one-sided lower confidence limit) 和**单侧置信上限** (one-sided upper confidence limit)。

当总体 $X$ 是连续型随机变量时，应选择 $\hat{\theta}_{L}$ 和 $\hat{\theta}_{U}$ 使

$$\begin{aligned}
P \{ \hat{\theta}_{L} < \theta \} = 1 - \alpha, \theta \in \Theta \\
P \{ \hat{\theta}_{U} > \theta \} = 1 - \alpha, \theta \in \Theta
\end{aligned}$$

根据上述定义，容易得到单侧置信限和置信区间的关系。

设统计量 $\hat{\theta}_{L}$ 和 $\hat{\theta}_{U}$ 分别是参数 $\theta$ 的置信水平为 $1 - \alpha_{1}$ 和 $1 - \alpha_{2}$ 的单侧置信下限和单侧置信上限，且 $\hat{\theta}_{L} < \hat{\theta}_{U}$，则 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 是 $\theta$ 的置信水平为 $1 - \alpha_{1} - \alpha_{2}$ 的置信区间。

### 枢轴量法

接下来我们介绍置信区间的一种求解方法，即枢轴量法。

设总体 $X$ 的密度函数为 $f(x; \theta)$，其中 $\theta$ 为待估参数，并设 $X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本。如果样本和参数 $\theta$ 的函数 $G(X_{1}, X_{2}, \cdots, X_{n}; \theta)$ 的分布完全已知，且形式上不依赖于其它位置参数，就称 $G(X_{1}, X_{2}, \cdots, X_{n}; \theta)$ 为**枢轴量** (pivot)。

我们可以根据下列三个步骤来寻求 $\theta$ 的置信区间：

1. 构造一个分布已知的枢轴量 $G(X_{1}, X_{2}, \cdots, X_{n}; \theta)$。
2. 当总体 $X$ 是连续型随机变量时，对给定的置信水平 $1 - \alpha$，根据枢轴量 $G(X_{1}, X_{2}, \cdots, X_{n}; \theta)$ 的分布，适当地选择两个常数 $a$ 和 $b$，使得

    $$P_{\theta} \{ a < G(X_{1}, X_{2}, \cdots, X_{n}; \theta) < b \} = 1 - \alpha$$

3. 假如参数 $\theta$ 可以从 $G(X_{1}, X_{2}, \cdots, X_{n}; \theta)$ 中分离出来，不等式 $a < G(X_{1}, X_{2}, \cdots, X_{n}; \theta) < b$ 可以等价地转化为 $\hat{\theta}_{L} < \theta < \hat{\theta}_{U}$，则对于连续型总体，有

    $$P \{ \hat{\theta}_{L} < \theta < \hat{\theta}_{U} \} = 1 - \alpha$$

此时即求得置信区间。

当总体 $X$ 是离散型随机变量时，则应选择使 $P_{\theta} \{ a < G(X_{1}, X_{2}, \cdots, X_{n}; \theta) < b \}$ 尽量接近 $1 - \alpha$ 的常数 $a, b$。

一般地，满足条件的 $a, b$ 不是唯一的，根据奈曼原则，我们应该选择使置信区间 $(\hat{\theta}_{L}, \hat{\theta}_{U})$ 的平均长度达到最短的 $a$ 和 $b$，但有时要做到这点并非易事。习惯上，我们取 $a$ 和 $b$ 满足

$$P_{\theta} \{ G(X_{1}, X_{2}, \cdots, X_{n}; \theta) \leq a \} = P_{\theta} \{ G(X_{1}, X_{2}, \cdots, X_{n}; \theta) \geq b \} = \frac{\alpha}{2}$$

## 正态总体参数的区间估计

### 单个正态总体情形

设总体 $X \sim N(\mu, \sigma^{2})$，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本。$\bar{X}$ 和 $s^{2}$ 分别是样本均值和样本方差，$1 - \alpha$ 是给定的置信水平。

#### $\sigma^{2}$ 已知时均值 $\mu$ 的区间估计

我们常取 $\mu$ 的点估计为样本均值 $\bar{X}$，则有 $\bar{X} \sim N(\mu, \frac{\sigma^{2}}{n})$，即 $\frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}} \sim N(0, 1)$。这个分布是已知的，因此可取枢轴量 $G(X_{1}, X_{2}, \cdots, X_{n}; \mu) = \frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}}$。

设常数 $a < b$，且满足

$$P \left\{ a < \frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}} < b \right\} = P \left\{ \bar{X} - b \frac{\sigma}{\sqrt{n}} < \mu < \bar{X} - a \frac{\sigma}{\sqrt{n}} \right\} = 1 - \alpha$$

此时，区间的平均长度为 $L = (b - a)\frac{\sigma}{\sqrt{n}}$。根据正态分布的对称性，知取 $a = -b = -z_{\frac{\alpha}{2}}$ 时，区间的长度 $L$ 最短。从而所对应的 $\mu$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} - \frac{\sigma}{\sqrt{n}} z_{\frac{\alpha}{2}}, \bar{X} + \frac{\sigma}{\sqrt{n}} z_{\frac{\alpha}{2}} \right)$$

常记作

$$\left( \bar{X} \pm \frac{\sigma}{\sqrt{n}} z_{\frac{\alpha}{2}} \right)$$

#### $\sigma^{2}$ 未知时均值 $\mu$ 的区间估计

此时，我们不能再取 $\frac{\bar{X} - \mu}{\frac{\sigma}{\sqrt{n}}}$ 为枢轴量，因为其中除含有待估参数 $\mu$ 外，还含有未知参数 $\sigma^{2}$。考虑将 $\sigma^{2}$ 的无偏估计量 $S^{2}$ 代入，有

$$\frac{\bar{X} - \mu}{\frac{S}{\sqrt{n}}} \sim t(n - 1)$$

这个分布是已知的，因此可取枢轴量

$$G(X_{1}, X_{2}, \cdots, X_{n}; \mu) = \frac{\bar{X} - \mu}{\frac{S}{\sqrt{n}}}$$

根据 $t$ 分布，我们有

$$P \left\{ \left| \frac{\bar{X} - \mu}{\frac{S}{\sqrt{n}}} \right| < t_{\frac{\alpha}{2}} (n - 1) \right\} = P \left\{ \bar{X} - \frac{S}{\sqrt{n}} t_{\frac{\alpha}{2}} (n - 1) < \mu < \bar{X} + \frac{S}{\sqrt{n}} t_{\frac{\alpha}{2}} (n - 1) \right\} = 1 - \alpha$$

于是所对应的 $\mu$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} \pm \frac{S}{\sqrt{n}} t_{\frac{\alpha}{2}} (n - 1) \right)$$

#### 成对数据情形

对于成对数据样本 $(X_{1}, Y_{1}), (X_{2}, Y_{2}), \cdots, (X_{n}, Y_{n})$，$X_{i}$ 和 $Y_{i}$ 一般不独立，且 $X_{1}, X_{2}, \cdots, X_{n}$ 不能看作是来自同一个正态总体的样本，$Y_{1}, Y_{2}, \cdots, Y_{n}$ 也不能看作是来自同一个正态总体的样本。

此时，我们一般考察差值 $D_{i} = X_{i} - Y_{i}, i = 1, 2, \cdots, n$。我们可以将 $D_{1}, D_{2}, \cdots, D_{n}$ 看作是来自同一个正态总体 $N(\mu_{D}, \sigma_{D}^{2})$ 的样本。所以，求有关成对数据的均值差 $\mu_{1} - \mu_{2}$ 的置信区间问题可以转化为求单个正态总体均值 $\mu_{D}$ 的置信区间问题。

根据前文，可得 $\mu_{D}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{D} \pm \frac{S_{D}}{\sqrt{n}} t_{\frac{\alpha}{2}} (n - 1) \right)$$

其中 $\bar{D} = \bar{X} - \bar{Y}, S_{D}^{2} = \frac{1}{n - 1} \sum_{i = 1}^{n} (D_{i} - \bar{D})^{2}$。

#### $\mu$ 未知时方差 $\sigma^{2}$ 的区间估计

$\sigma^{2}$ 的无偏估计量为样本方差 $S^{2}$，当 $\mu$ 已知时这是可以直接求得的，因此我们只关注 $\mu$ 未知时的情形。

由前文可知，有

$$\frac{(n - 1) S^{2}}{\sigma^{2}} \sim \chi^{2} (n - 1)$$

这个分布是已知的，因此可取枢轴量

$$G(X_{1}, X_{2}, \cdots, X_{n}; \mu) = \frac{(n - 1) S^{2}}{\sigma^{2}}$$

根据 $\chi^{2}$ 分布，我们有

$$P \left\{ \chi_{1 - \frac{\alpha}{2}}^{2} (n - 1) < \frac{(n - 1) S^{2}}{\sigma^{2}} < \chi_{\frac{\alpha}{2}}^{2} (n - 1) \right\} = P \left\{ \frac{(n - 1) S^{2}}{\chi_{\frac{\alpha}{2}}^{2} (n - 1)} < \sigma^{2} < \frac{(n - 1) S^{2}}{\chi_{1 - \frac{\alpha}{2}}^{2} (n - 1)} \right\} = 1 - \alpha$$

于是所对应的 $\sigma^{2}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \frac{(n - 1) S^{2}}{\chi_{\frac{\alpha}{2}}^{2} (n - 1)}, \frac{(n - 1) S^{2}}{\chi_{1 - \frac{\alpha}{2}}^{2} (n - 1)} \right)$$

这里需要说明的是，由于 $\chi^{2}$ 分布的密度函数是不对称的，故以上所求得的置信区间并不满足区间平均长度最短。但这一区间在实际应用中较为方便。

### 两个正态总体情形

设有两个正态总体 $X \sim N(\mu_{1}, \sigma_{1}^{2}), Y \sim N(\mu_{2}, \sigma_{2}^{2})$，$X_{1}, X_{2}, \cdots, X_{n_{1}}, n_{1} \geq 2$ 为来自总体 $X$ 的样本，$Y_{1}, Y_{2}, \cdots, Y_{n_{2}}, n_{2} \geq 2$ 为来自总体 $Y$ 的样本。两样本相互独立，$\bar{X}, \bar{Y}$ 分别为两样本均值，$S_{1}^{2}, S_{2}^{2}$ 分别为两样本方差。

#### $\sigma_{1}$ 和 $\sigma_{2}$ 已知时均值差 $\mu_{1} - \mu_{2}$ 的区间估计

取 $\mu_{1} - \mu_{2}$ 的无偏估计 $\bar{X} - \bar{Y}$，则由正态分布的性质有

$$\bar{X} - \bar{Y} \sim N \left( \mu_{1} - \mu_{2}, \frac{\sigma_{1}^{2}}{n_{1}} + \frac{\sigma_{2}^{2}}{n_{2}} \right)$$

利用单个总体均值区间估计的结论，可得 $\mu_{1} - \mu_{2}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} - \bar{Y} \pm \sqrt{\frac{\sigma_{1}^{2}}{n_{1}} + \frac{\sigma_{2}^{2}}{n_{2}}} z_{\frac{\alpha}{2}} \right)$$

#### $\sigma_{1}$ 和 $\sigma_{2}$ 相等且未知时均值差 $\mu_{1} - \mu_{2}$ 的区间估计

当俩总体的方差相同，即 $\sigma_{1}^{2} = \sigma_{2}^{2} = \sigma^{2}$，但未知时，我们可以取 $\sigma^{2}$ 的无偏估计量

$$S_{w}^{2} = \frac{(n_{1} - 1) S_{1}^{2} + (n_{2} - 1) S_{2}^{2}}{n_{1} + n_{2} - 2}$$

此时有

$$\frac{(\bar{X} - \bar{Y}) - (\mu_{1} - \mu_{2})}{S_{w} \sqrt{\frac{1}{n_{1}} + \frac{1}{n_{2}}}} \sim t(n_{1} + n_{2} - 2)$$

利用单个总体均值区间估计的结论，可得 $\mu_{1} - \mu_{2}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} - \bar{Y} \pm S_{w} \sqrt{\frac{1}{n_{1}} + \frac{1}{n_{2}}} t_{\frac{\alpha}{2}} (n_{1} + n_{2} - 2) \right)$$

#### $\sigma_{1}$ 和 $\sigma_{2}$ 未知时均值差 $\mu_{1} - \mu_{2}$ 的区间估计

当样本容量 $n_{1}$ 和 $n_{2}$ 充分大时，可以证明

$$\frac{(\bar{X} - \bar{Y}) - (\mu_{1} - \mu_{2})}{\sqrt{\frac{S_{1}^{2}}{n_{1}} + \frac{S_{2}^{2}}{n_{2}}}}$$

渐进服从标准正态分布 $N(0, 1)$，于是可得 $\mu_{1} - \mu_{2}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} - \bar{Y} \pm \sqrt{\frac{S_{1}^{2}}{n_{1}} + \frac{S_{2}^{2}}{n_{2}}} z_{\frac{\alpha}{2}} \right)$$

对于有限小样本，可以证明

$$\frac{(\bar{X} - \bar{Y}) - (\mu_{1} - \mu_{2})}{\sqrt{\frac{S_{1}^{2}}{n_{1}} + \frac{S_{2}^{2}}{n_{2}}}}$$

近似服从自由度为 $k$ 的 $t$ 分布，其中

$$k = \left\lfloor \frac{\left( \frac{S_{1}^{2}}{n_{1}} + \frac{S_{2}^{2}}{n_{2}} \right)^{2}}{\frac{(S_{1}^{2})^{2}}{n_{1}^{2} (n_{1} - 1)} + \frac{(S_{2})^{2}}{n_{2}^{2} (n_{2} - 1)}} \right\rfloor$$

在实际应用中，也常用 $\min \{ n_{1} - 1, n_{2} - 1 \}$ 近似代替上述自由度 $k$。此时 $\mu_{1} - \mu_{2}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\left( \bar{X} - \bar{Y} \pm S_{w} \sqrt{\frac{1}{n_{1}} + \frac{1}{n_{2}}} t_{\frac{\alpha}{2}} (k) \right)$$

#### 方差比 $\frac{\sigma_{1}^{2}}{\sigma_{2}^{2}}$ 的区间估计

取 $\frac{\sigma_{1}^{2}}{\sigma_{2}^{2}}$ 的点估计  $\frac{S_{1}^{2}}{S_{2}^{2}}$，有

$$\frac{\frac{S_{1}^{2}}{\sigma_{1}^{2}}}{\frac{S_{2}^{2}}{\sigma_{2}^{2}}} \sim F(n_{1} - 1, n_{2} - 1)$$

利用枢轴量法，可求得 $\frac{\sigma_{1}^{2}}{\sigma_{2}^{2}}$ 的置信水平为 $1 - \alpha$ 的置信区间为

$$\frac{\frac{S_{1}^{2}}{S_{2}^{2}}}{F_{\frac{\alpha}{2}} (n_{1} - 1, n_{2} - 1)}, \frac{\frac{S_{1}^{2}}{S_{2}^{2}}}{F_{1 - \frac{\alpha}{2}} (n_{1} - 1, n_{2} - 1)}$$

这里需要说明的是，由于 $F$ 分布的密度函数是不对称的，故以上所求得的置信区间并不满足区间平均长度最短。但这一区间在实际应用中较为方便。

### 总结

最后，我们将这一节的内容整理为下表：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/mathematics/probability_and_statistics/chapter_7_1.png" width="70%" style="margin: 0 auto;">
</div>

## 非正态总体参数的区间估计

当数据不服从正态分布时，求参数区间估计的一种有效方法就是所谓的大样本方法，即要求样本容量比较大，再利用中心极限定理进行分析。

### 0-1 分布参数的区间估计

设总体 $X$ 服从 0-1 分布 $B(1, p)$，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本，当 $n$ 充分大时，由中心极限定理知

$$\frac{\sum_{i = 1}^{n} X_{i} - np}{\sqrt{np(1 - p)}} = \frac{n \bar{X} - np}{\sqrt{np(1 - p)}}$$

近似服从标准正态分布 $N(0, 1)$。于是有

$$P \left\{ -z_{\frac{\alpha}{2}} < \frac{n \bar{X} - np}{\sqrt{np(1 - p)}} < z_{\frac{\alpha}{2}} \right\} \approx 1 - \alpha$$

等价于

$$P\{(n + z_{\frac{\alpha}{2}}^{2}) p^{2} - (2n \bar{X} + z_{\frac{\alpha}{2}}^{2}) p + n \bar{X}^{2} < 0\} \approx 1 - \alpha$$

求解方程可得参数 $p$ 的置信水平为 $1 - \alpha$ 的近似置信区间为

$$\left( \frac{1}{2a} (- b - \sqrt{b^{2} - 4ac}), \frac{1}{2a} (- b + \sqrt{b^{2} - 4ac}) \right) = (\hat{p}_{L}, \hat{p}_{U})$$

其中 $a = n + z_{\frac{\alpha}{2}}^{2}, b = -(2n \bar{X} + z_{\frac{\alpha}{2}}^{2}), c = n \bar{X}^{2}$。或取 $p(1 - p)$ 的估计量为 $\bar{X}(1 - \bar{X})$，得 $p$ 的置信水平为 $1 - \alpha$ 的近似置信区间为

$$\left( \bar{X} \pm z_{\frac{\alpha}{2}} \sqrt{\frac{\bar{X}(1 - \bar{X})}{n}} \right)$$

### 其它分布均值 $\mu$ 的区间估计

设总体 $X$ 的均值为 $\mu$，方差为 $\sigma^{2}$，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的样本。根据中心极限定理，当样本容量 $n$ 充分大时，

$$\frac{\sum_{i = 1}^{n} X_{i} - n \mu}{\sqrt{n} \sigma}$$

近似服从标准正态分布 $N(0, 1)$。故 $\mu$ 的置信水平为 $1 - \alpha$ 的近似置信区间为

$$\left( \bar{X} \pm \frac{\sigma}{\sqrt{n}} z_{\frac{\alpha}{2}} \right)$$

如果方差 $\sigma^{2}$ 未知，可以用估计量 $S^{2}$ 代替 $\sigma^{2}$，由此得到相应的近似置信区间为

$$\left( \bar{X} \pm \frac{S}{\sqrt{n}} z_{\frac{\alpha}{2}} \right)$$

对于有限小样本，可以证明

$$\frac{\bar{X} - \mu}{\frac{S}{\sqrt{n}}}$$

近似服从自由度为 $n - 1$ 的 $t$ 分布，即 $t(n - 1)$。故均值 $\mu$ 的置信水平为 $1 - \alpha$ 的近似置信区间为

$$\left( \bar{X} \pm \frac{S}{\sqrt{n}} t_{\frac{\alpha}{2}} (n - 1) \right)$$
