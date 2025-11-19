---
comments: true
---

# 第六章 - 统计量与抽样分布

## 随机样本与统计量

### 总体与样本

数理统计中，我们把研究对象的全体称作**总体** (population)，而总体中的每个成员称作**个体** (individual)。总体中所包含的个体数量称作**总体容量** (size of population)，容量有限的总体称作**有限总体** (finite population)，容量无限的总体称作**无限总体** (infinite population)。

为了对总体进行研究，首先要收集数据。经典的数据收集方法一般有两种：

1. 通过抽样调查收集数据；
2. 通过试验收集数据。

总体的某个指标 $X$，对不同的个体来说有不同的取值，这些取值构成一个分布，因此 $X$ 可以看成一个随机变量。如果我们关心总体的两个或两个以上的指标，就可用随机向量 $(X_{1}, X_{2}, \cdots, X_{d})$ 来表示。

数理统计的主要任务是从总体中抽取一部分个体，根据这部分个体的数据对总体分布或其中的未知参数给出推断。被抽取的部分个体被称作总体的一个**样本** (sample)，被抽取的个体数量称作**样本容量** (size of sample)。

假设我们从总体 $X$ 中随机地抽取 $n$ 个个体，随着抽取个体的不同，指标 $X$ 的取值也不同，分别记作 $X_{1}, X_{2}, \cdots, X_{n}$，称其为**随机样本** (random sample)。

设总体 $X$ 是具有分布函数 $F(\cdot)$ 的随机变量，$X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的随机样本。若满足

1. （独立性）$X_{1}, X_{2}, \cdots, X_{n}$ 是相互独立的随机变量；
2. （代表性）每一 $X_{i}$ 与总体 $X$ 有相同的分布函数，

则称 $X_{1}, X_{2}, \cdots, X_{n}$ 为取自总体 $X$ 的**简单随机样本** (simple random sample) 或 **i.i.d. 样本** (independent identically distributed sample)，此时所采用的抽样方式称作**简单随机抽样** (simple random sampling)。

后文中提到的「样本」均指简单随机样本，「随机抽取」均指采用简单随机抽样。

对所抽取的样本进行观测，得出一组实数 $x_{1}, x_{2}, \cdots, x_{n}$，我们称 $x_{1}, x_{2}, \cdots, x_{n}$ 为样本 $X_{1}, X_{2}, \cdots, X_{n}$ 的一个**样本值** (sample value) 或**观测值** (observation)。

如果总体的分布函数为 $F(x)$，那么样本的联合分布函数为

$$F_{n} (x_{1}, x_{2}, \cdots, x_{n}) = \prod_{i = 1}^{n} F(x_{i})$$

如果总体具有连续型分布，其密度函数为 $f(x)$，那么样本的联合密度函数为

$$f_{n} (x_{1}, x_{2}, \cdots, x_{n}) = \prod_{i = 1}^{n} f(x_{i})$$

### 统计量

设 $X_{1}, X_{2}, \cdots, X_{n}$ 是来自总体 $X$ 的一个样本，$g(X_{1}, X_{2}, \cdots, X_{n})$ 是样本 $X_{1}, X_{2}, \cdots, X_{n}$ 的函数。若 $g$ 不含位置参数，则称 $g(X_{1}, X_{2}, \cdots, X_{n})$ 是一**统计量** (statistic)。

下面是几个常用的重要统计量：

- 样本均值

    $$\bar{X} = \frac{1}{n} \sum_{i = 1}^{n} X_{i}$$

- 样本方差

    $$S^{2} = \frac{1}{n - 1} \sum_{i = 1}^{n} (X_{i} - \bar{X})^{2} = \frac{1}{n - 1} \left( \sum_{i = 1}^{n} X_{i}^{2} - n \bar{X}^{2} \right)$$

- 样本标准差

    $$S = \sqrt{S^{2}} = \sqrt{\frac{1}{n - 1} \sum_{i = 1}^{n} (X_{i} - \bar{X})^{2}}$$

- 样本 $k$ 阶（原点）矩

    $$A_{k} = \frac{1}{n} \sum_{i = 1}^{n} X_{i}^{k}, k = 1, 2, \cdots$$

- 样本 $k$ 阶中心距

    $$B_{k} = \frac{1}{n}\sum_{i = 1}^{n} (X_{i} - \bar{X})^{k}, k = 2, 3, \cdots$$

一般地，用样本均值 $\bar{X}$ 作为总体均值 $\mu$ 的估计；用样本方差 $S^{2}$ 作为总体方差 $\sigma^{2}$ 的估计；用样本原点矩 $A_{k}$ 作为总体原点矩 $\mu_{k}$ 的估计；用样本中心矩 $B_{k}$ 作为总体中心距 $\nu_{k}$ 的估计。

总体方差的估计可以用 $S^{2}$ 也可以用 $B_{2}$。主要的区别是 $S^{2}$ 作为总体方差估计是无偏估计，但 $B_{2}$ 作为总体方差的估计是有偏的。

假设 $X_{1}, X_{2}, \cdots, X_{n}$ 是一个从总体 $X$ 中抽取的简单随机样本，$\mu_{k} = E(X^{k}), k = 1, 2, \cdots$ 存在，由辛钦大数定律可知

$$A_{k} = \frac{1}{n} \sum_{i = 1}^{n} X_{i}^{k} \stackrel{P}{\longrightarrow} \mu_{k}, n \to +\infty$$

进一步，如果 $g(X_{1}, X_{2}, \cdots, X_{n})$ 是一个连续函数，由依概率收敛的性质，有

$$g(X_{1}, X_{2}, \cdots, X_{n}) \stackrel{P}{\longrightarrow} g(\mu_{1}, \mu_{2}, \cdots, \mu_{k}), n \to +\infty$$

## $\chi^{2}$ 分布、$t$ 分布、$F$ 分布

统计量的分布称作**抽样分布** (sampling distribution)。在数理统计中，最重要的三个抽样分布是 $\chi^{2}$ 分布、$t$ 分布、$F$ 分布。

### $\chi^{2}$ 分布

设 $X_{1}, X_{2}, \cdots, X_{n}$ 为独立同分布的随机变量，且都服从标准正态分布 $N(0, 1)$。记

$$Y = X_{1}^{2} + X_{2}^{2} + \cdots + X_{n}^{2}$$

则称 $Y$ 服从自由度为 $n$ 的 $\chi^{2}$ 分布，记作 $Y \sim \chi^{2} (n)$。

$\chi^{2}$ 分布的密度函数为

$$f_{\chi^{2}} (x) = \begin{cases}
\frac{1}{2^{\frac{n}{2}} \Gamma(\frac{n}{2})} x^{\frac{n}{2} - 1} e^{-\frac{x}{2}}, & x > 0 \\
0, & \text{else}
\end{cases}$$

$\chi^{2}$ 分布的自由度 $n$ 决定了其密度函数的形状。

$\chi^{2}$ 分布具有如下性质：

- $\chi^{2}$ 分布可加性：设 $Y_{1} \sim \chi^{2} (m), Y_{2} \sim \chi^{2} (n), m, n \geq 1$，且两者相互独立，则 $Y_{1} + Y_{2} \sim \chi^{2} (m + n)$。
- $\chi^{2}$ 分布的数学分布和方差：设 $Y \sim \chi^{2} (n)$，则
  
   $$ E(Y) = n, \text{Var}(Y) = 2n $$

- $\chi^{2}$ 分布分位数：对于给定的正数 $\alpha, 0 < \alpha < 1$，称满足条件

    $$P \{ \chi^{2} > \chi_{\alpha}^{2}(n) \} = \int_{\chi_{\alpha}^{2}(n)}^{+\infty} f_{{\alpha}^{2}} (x) \mathrm{d} x = \alpha$$

    的 $\chi_{\alpha}^{2}(n)$ 为 $\chi^{2}(n)$ 分布的上 $\alpha$ 分位数。

当 $n$ 充分大时，$\chi^{2}$ 分布的上 $\alpha$ 分位数可以有如下的近似：

$$\chi_{\alpha}^{2}(n) \approx \frac{1}{2}(z_{\alpha} + \sqrt{2n - 1})^{2}$$

其中 $z_{\alpha}$ 是标准正态分布的上 $\alpha$ 分位数。

### $t$ 分布

设 $X \sim N(0, 1), Y \sim \chi^{2}(n)$，且 $X, Y$ 相互独立，则称随机变量

$$t = \frac{X}{\sqrt{\frac{Y}{n}}}$$

服从自由度为 $n$ 的 $t$ 分布或**学生氏** (student) 分布，记作 $t \sim t(n)$。

$t(n)$ 分布的密度函数为

$$f_{t}(n) = \frac{\Gamma(\frac{n + 1}{2})}{\sqrt{\pi n} \Gamma(\frac{n}{2})} \left( 1 + \frac{x^{2}}{n} \right)^{-\frac{n + 1}{2}}, -\infty < x < +\infty$$

当 $n \to +\infty$ 时，$f_{t}(x)$ 趋于 $\phi(x)$，即为标准正态密度函数。

$t$ 分布具有如下性质：

- $t$ 分布的密度函数 $f_{t}(x)$ 是偶函数，关于 $y$ 轴对称。
- 由 $t$ 分布的密度函数可以得到

    $$\lim_{n \to +\infty} f_{t}(x) = \frac{1}{\sqrt{2\pi}} e^{-\frac{x^{2}}{2}}$$

    即当 $n$ 足够大时，$t$ 分布近似于标准正态分布 $N(0, 1)$。

- $t$ 分布分位数：对于给定的正数 $\alpha, 0 < \alpha < 1$，称满足条件

    $$P \{ t > t_{\alpha}(n) \} = \int_{t_{\alpha}(n)}^{+\infty} f_{t} (x) \mathrm{d} x = \alpha$$

    的 $t_{\alpha}(n)$ 为 $t(n)$ 分布的上 $\alpha$ 分位数。由 $t$ 分布密度函数的对称性可知 $t_{1 - \alpha}(n) = -t_{\alpha}(n)$。

### $F$ 分布

设 $U \sim \chi^{2}(n_{1}), V \sim \chi^{2}(n_{2})$，且 $U$ 与 $V$ 相互独立，则称随机变量

$$F = \frac{\frac{U}{n_{1}}}{\frac{V}{n_{2}}}$$

服从第一自由度为 $n_{1}$，第二自由度为 $n_{2}$ 的 $F$ 分布，记作 $F \sim F(n_{1}, n_{2})$。

$F(n_{1}, n_{2})$ 分布的密度函数为

$$f_{F}(x) = \frac{\Gamma(\frac{n_{1} + n_{2}}{2}) (\frac{n_{1}}{n_{2}})^{\frac{n_{1}}{2}} x^{\frac{n_{1}}{2} - 1}}{\Gamma(\frac{x_{1}}{2}) \Gamma(\frac{n_{2}}{2}) (1 + \frac{n_{1} x}{n_{2}})^{\frac{n_{1} + n_{2}}{2}}}, x > 0$$

$F$ 分布具有如下性质：

- 若 $F \sim F(n_{1}, n_{2})$，则 $\frac{1}{F} \sim F(n_{2}, n_{1})$。
- 若 $X \sim t(n)$，则 $X^{2} \sim F(1, n)$。
- $F$ 分布分位数：对于给定的正数 $\alpha, 0 < \alpha < 1$，称满足条件

    $$P \{ F > F_{\alpha}(n_{1}, n_{2}) \} = \int_{ F_{\alpha}(n_{1}, n_{2})}^{+\infty} f_{F} (x) \mathrm{d} x = \alpha$$

    的 $F_{\alpha}(n_{1}, n_{2})$ 为 $F(n)$ 分布的上 $\alpha$ 分位数。由 $F$ 分布密度函数可知 $F_{1 - \alpha}(n_{1}, n_{2}) = \frac{1}{F_{\alpha}(n_{2}, n_{1})}$。

## 正态总体下的抽样分布

设 $X_{1}, X_{2}, \cdots, X_{n}$ 为来自正态总体 $N(\mu, \sigma^{2})$ 的简单随机样本，$\bar{X}$ 是样本均值，$S^{2}$ 是样本方差，则有如下定理：

- $\bar{X} \sim N \left( \mu, \frac{\sigma^{2}}{n} \right)$
- $\frac{(n - 1) X^{2}}{\sigma^{2}} \sim \chi^{2} (n - 1)$
- $\bar{X}$ 与 $S^{2}$ 相互独立
- $\frac{\bar{X} - \mu}{\frac{S}{\sqrt{n}}} \sim t(n - 1)$

设 $X_{1}, X_{2}, \cdots, X_{n_{1}}$ 和 $Y_{1}, Y_{2}, \cdots, Y_{n_{2}}$ 分别为来自正态总体 $N(\mu_{1}, \sigma_{1}^{2})$ 和 $N(\mu_{2}, \sigma_{2}^{2})$ 的两个相互独立的简单随机样本。记 $\bar{X}, \bar{Y}$ 分别是两个样本的样本均值，$S_{1}^{2}, S_{2}^{2}$ 分别是两个样本的样本方差，则有

- $\frac{\frac{S_{1}^{2}}{\sigma_{1}^{2}}}{\frac{S_{2}^{2}}{\sigma_{2}^{2}}} \sim F(n_{1} - 1, n_{2} - 1)$
- 当 $\sigma_{1}^{2} = \sigma_{2}^{2} = \sigma^{2}$ 时

    $$\frac{(\bar{X} - \bar{Y}) - (\mu_{1} - \mu_{2})}{S_{w} \sqrt{\frac{1}{n_{1}} + \frac{1}{n_{2}}}} \sim t(n_{1} + n_{2} - 2)$$

    其中 $S_{w}^{2}$ 称作「合样本方差」，定义如下：

    $$S_{w}^{2} = \frac{(n_{1} - 1) S_{1}^{2} + (n_{2} - 1) S_{2}^{2}}{n_{1} + n_{2} - 2}, S_{w} = \sqrt{S_{w}^{2}}$$
