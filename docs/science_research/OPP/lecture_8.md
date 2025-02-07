---
comments: true
---

# Lecture 8 - The Probabilistic Method

Speaker: Prof. Alexander Scott

It can be very difficult to construct mathematical objects without embedding some sort of regular structure.

*Random* or *typical* objects often have desirable properties that are difficult to construct explicitly.

## Example 1: Tournaments

A *tournament* is an orientation of a complete graph: every edge between $x$ and $y$ is assigned a direction (towards $x$ or towards $y$).

A tournament has *Property* $P_{k}$ if for every set of $k$ players, there is someone who beats all of them. For example, the cyclic tournament on three vertices has Property $P_{1}$. For large $k$, tournaments with Property $P_{k}$ are difficult to construct!

**Theorem**

If $n \geq k^{2} 2^{k + 1}$, then some tournament with $n$ vertices has Property $P_k$.

Idea:

- Consider a random tournament.
- Show that with positive probability it has Property $P_{k}$.
- Deduce that *some* tournament must have this property.

**Proof**

Let $T$ be a random tournament on $n$ vertices, where each edge between $x$ and $y$ is directed independently with equal probability towards $x$ or $y$. For each set $S$ of $k$ vertices, let $B_{S}$ be the event that no vertex beats every vertex in $S$ (we say that $S$ is then a *bad set*).

Then

$$P(B_{S}) = (1 - \frac{1}{2^{k}})^{n - k} \leq e^{-\frac{n - k}{2^{k}}}$$

Here we have used the inequality $1 + x \leq e^{x}$, which holds for all real numbers $x$ (and is extremely useful).

We deduce that the expected number of bad $k$-sets $B$ is at most

$$\binom{n}{k} e^{-\frac{n - k}{2^{k}}}$$

Suppose this expectation is strictly less than $1$. If *on average* we have less than $1$ bad set, then there must be some tournament where we have less than $1$ bad set (the *minimum* is at most the *average*).

Thus, it is sufficient to show that

$$\binom{n}{k} e^{-\frac{n - k}{2^{k}}} < 1$$

Recall that $n \geq k^{2} 2^{k + 1}$; then

$$\binom{n}{k} e^{-\frac{n - k}{2^{k}}} \leq \frac{n^{k}}{k!} e^{-\frac{n}{2^{k + 1}}}$$

It is straightforward to see that this is less than $1$. $\square$

Let's note:

- We did not directly show that $T$ exists: we showed that a random tournament had a strictly positive probability of having the required properties.
- We needed to perform some calculations!

We can consider *random structures*, even when our original problem does not mention randomness.All the tools of *Probability Theory* are now at our disposal!

## Example 2: Coding Theory

Coding Theory addresses the problem of transmitting information through a binary channel: in other words, we aim to send information as a sequence of $0$s and $1$s.

A *code* is a collection of binary strings, one for each type of information we aim to transmit (for example, one string for each letter of our alphabet).

Sometimes the channel is *noisy*, in which case we require our strings to be highly distinct (we need an *error-correcting code*). Even without noise, important questions arise. For example, how quickly can we transmit information through a channel?

A *prefix* of a binary string is an initial segment. For example, $010$ is a prefix of $0101$ but not of $1010$.

A set $F$ of binary strings is *prefix-free* if no string in $F$ is a prefix of another. A fundamental theorem, the *Kraft-McMillan Inequality*, applies to prefix-free codes:

**Theorem (*Kraft-McMillan Inequality*)**

Let $F$ be a prefix-free set of binary strings, and suppose that $F$ contains $N_{i}$ strings of length $i$ for each $i$. Then

$$\sum_{i \geq 0} \frac{N_{i}}{2^{i}} \leq 1$$

**Proof**

Consider a random (infinite) sequence $B = b_{1} b_{2} \dots$. For a string $C$ of length $k$,

$$P(C\ \text{is a prefix of}\ B) = 2^{-k}$$

Thus, the expected number of strings from $F$ that occur as a prefix of $B$ is

$$\sum_{C \in F} 2^{-|C|} = \sum_{i \geq 0} \frac{N_{i}}{2^{i}}$$

On the other hand, we can never have more than one string from $F$ as prefixes simultaneously, so we deduce that

$$\sum_{i \geq 0} \frac{N_{i}}{2^{i}} \leq 1$$

(the *average* is at most the *maximum*). $\square$

## Example 3: Max Cut

In the first example, the *linearity of expectation* is straightforward: if $X = \sum X_{i}$, then

$$\mathrm{E}(X) = \sum \mathrm{E}(X_{i})$$

It also applies to variance if the random variables are independent.

In the *Max Cut* problem, we are given a graph $G$ and aim to divide its vertices into two classes $V_{1}, V_{2}$ so that as many edges as possible have ends in both classes.

The Max Cut problem is known to be a challenging algorithmic problem. (It is NP-hard; in fact, it is NP-hard even to find a good approximate solution!)

A theorem provides a simple bound for the Max Cut problem:

**Theorem**

For every graph $G$, there exists a partition $V(G) = V_{1} \cup V_{2}$ such that at least half the edges of $G$ have one end in each class.

**Proof**

Consider a random partition. For each edge $e = (x, y)$, we define a random variable $X_{e}$ by setting $X_{e} = 1$ if $e$ has one end in each set and $X_{e} = 0$ otherwise. Let

$$X = \sum_{e} X_{e}$$

We aim to show that there exists some partition in which $X \geq \frac{e(G)}{2}$.

Observe that

$$\mathrm{E}(X_{e}) = \frac{1}{2}$$

Thus, by linearity of expectation

$$\mathrm{E}(X) = \frac{e(G)}{2}$$

It follows that there exists *some* partition for which at least half the edges have one end in each class. $\square$

It is possible to *derandomise* this argument to obtain a very fast algorithm.

## Example 4: Independent Sets

In the *alteration method*, we generate a random structure and then modify it to achieve the desired properties.

For example: an *independent set* in a graph is a set of vertices, none of which are joined by edges.

**Theorem**

Let $G$ have $n$ vertices and average degree $d$. Then $G$ contains an independent set of size at least $\frac{n}{2d}$.

**Proof**

We generate a set in two steps. First, let $S$ be a random subset of $V(G)$ obtained by including each vertex independently with probability $p$. Then, let $T$ be obtained from $S$ by deleting one end from each edge.

The expected size of $S$ is

$$\mathrm{E}(S) = pn$$

The expected number of edges contained in $S$ is

$$\mathrm{E}(e(S)) = p^{2}e(G) = \frac{p^{2}nd}{2}$$

Thus, on average, the number of vertices remaining is

$$\mathrm{E}(T) \geq pn - \frac{p^{2}nd}{2}$$

Setting $p = \frac{1}{d}$ yields

$$\mathrm{E}(T) \geq \frac{n}{2d}$$

$\square$

## Broader Horizons: Random Graphs

A highly important and fascinating example is provided by *random graphs*. The theory of random graphs was initially developed in the 1960s, but it has since grown into a significant and influential area of research, with connections to numerous fields.

In the $G(n, p)$ model, we consider an $n$-vertex graph in which each edge is present independently with probability $p$. Thus, $G(n, 0)$ has no edges, $G(n, 1)$ is the complete graph, and $G(n, \frac{1}{2})$ has (on average) approximately half the edges.

Random graphs are used to model numerous real-world processes, from social networks to epidemics. A deep theory exists regarding the various changes that a typical random graph undergoes as $p$ increases from $0$ to $1$.

What can we say about the typical structure of a graph in $G(n, p)$, where $p = p(n)$ depends on $n$?

Let us consider triangles. How large must $p$ be for triangles to appear in $G(n, p)$? The expected number of triangles is given by

$$\binom{n}{3} p^{3} \sim \frac{n^{3}p^{3}}{6}$$

Thus, if $p \ll \frac{1}{n}$, then the expected number of triangles tends to $0$. It follows (for example, by *Markov's Inequality*) that the probability that $G$ contains a triangle tends to $0$.

On the other hand, if $p \gg \frac{1}{n}$, then the expected number of triangles tends to infinity. Does this imply that the probability of obtaining a triangle tends to $1$?

To address this, we need to consider the *variance*.

Idea:

- Consider a random graph $G(n, p)$, and let $X$ denote the number of triangles
- Calculate the mean and variance of $X$
- Use *Chebyshev's Inequality* to show that it is highly unlikely that $X = 0$

For each triple of vertices $A = \{x, y, z\}$, we define a random variable $X_{A}$ as follows:

$$X_{A} =\left\{ \begin{aligned}
    1,\ & \text{if}\ xyz\ \text{is a triangle in}\ G \\
    0,\ & \text{otherwise}
\end{aligned}
\right.$$

We know that $\mathrm{E}(X) \sim \frac{n^{3}p^{3}}{6}$. Let us calculate its variance $\sigma^{2}$. We have

$$\sigma^{2} = \mathrm{E}[(X - \mathrm{E}(X))^{2}] = \sum_{A, B} \text{cov}(A, B)$$

where the sum is taken over all pairs of $A$ and $B$.

If $A$ and $B$ are disjoint, then $X_{A}$ and $X_{B}$ are independent. Thus, $\text{cov}(A, B) = 0$. In fact, if $|A \cup B| = 1$, then they remain independent.

Thus

$$\sigma^{2} = \sum_{|A \cup B| = 2} \text{cov}(A, B) + \sum_{|A \cup B| = 3} \text{cov}(A, B)$$

If $|A \cup B| = 2, then$

$$\text{cov}(A, B) = \mathrm{E}(X_{A} X_{B}) - \mathrm{E}(X_{A}) \mathrm{E}(X_{B}) = p^{4} - p^{6} \leq p^{4}$$

and if $|A \cup B| = 3$, then $A = B$,

$$\text{cov}(A, B) = p^{3} - p^{6} \leq p^{3}$$

Thus

$$\sigma^{2} \leq \binom{n}{3} p^{3} + \binom{n}{2} (n - 2)(n - 3) p^{4} \leq 2 n^{4} p^{4}$$

We now apply *Chebyshev's Inequality*:

$$P(|X - \mu| \geq t) \leq \frac{\sigma^{2}}{t^{2}} \leq \frac{2 n^{4} p^{4}}{t^{2}}$$

By setting $t$ to different values, one can determine how large $p$ must be for the expected number of triangles to meet certain conditions.

We have demonstrated:

- If $np \rightarrow 0$, then $P(G \ \text{contains a triangle}) \rightarrow 0$
- If $np \rightarrow \infty$, then $P(G \ \text{contains a triangle}) \rightarrow 1$

We say that $p(n) = \frac{1}{n}$ is a *threshold function* for the presence of triangles in $G$.

We observe the same pattern for other graphs: there exists a threshold $p_{H}$ such that if $p \ll p_{H}$, then it is highly unlikely that $G(n, p)$ contains a copy of $H$; but if $p \gg p_{H}$, then $G(n, p)$ will almost certainly contain copies. This is an example of a *phase transition*.

For many graphs $H$, the threshold for $G$ to contain a copy of $H$ occurs around the point where the expected number of copies of $H$ becomes large.

Finally, let us briefly discuss martingale methods. A *martingale* is (informally) a sequence of random variables $X_{0}, X_{1}, \dots$ where $\mathrm{E}(X_{i + 1} | X_{i}) = X_{i}$: at each step, the expected value remains unchanged. (This can be likened to making a sequence of fair bets in a casino.)

Martingales are highly useful in analysing various types of random graph processes. For example, let $\chi(G)$ denote the chromatic number of $G$. Estimating the average value of $\chi(G)$ for a random graph is challenging, but it is known to be approximately

$$\chi(G) \sim \frac{n}{2}\log_{2}n$$

The key idea is as follows:

- Reveal the graph one vertex at a time: let $X_{i}$ denote the *expected* chromatic number of $G$ given the information provided by the first $i$ vertices.
- The sequence $(X_{i})_{i = 0}^{n}$ forms a martingale!
- Now apply a martingale inequality (for example, the *Hoeffding Inequality*, a relative of the *Chernoff Inequality* for binomial random variables) to show that $X$ is likely to be close to its mean.

The result follows elegantly!
