---
comments: true
---

# 错题整理

HW1 选择题 2-5

Consider the following buffer management problem. Initially the buffer size (the number of blocks) is one. Each block can accommodate exactly one item. As soon as a new item arrives, check if there is an available block. If yes, put the item into the block, induced a cost of one. Otherwise, the buffer size is doubled, and then the item is able to put into. Moreover, the old items have to be moved into the new buffer so it costs $k + 1$ to make this insertion, where k is the number of old items. Clearly, if there are $N$ items, the worst-case cost for one insertion can be $\Omega (N)$.  To show that the average cost is $O(1)$, let us turn to the amortized analysis. To simplify the problem, assume that the buffer is full after all the $N$ items are placed. Which of the following potential functions works?

=== "A"

    The number of items currently in the buffer

=== "B"

    The opposite number of items currently in the buffer

=== "C"

    The number of available blocks currently in the buffer

=== "D"

    The opposite number of available blocks in the buffer

??? abstract "答案解析"

    正确答案：D

    解析：在不需要扩容的插入操作中，剩余的空缓存数可以使势能减少。又每次操作我们需要「加上」操作的势能，因此势能函数应当为负值。

---

EX1 判断题 1-1

Amortized bounds are weaker than the corresponding worst-case bounds, because there is no guarantee for any single operation.

??? abstract "答案解析"

    正确答案：T

    解析：摊还复杂度虽然和最坏复杂度同阶，但是具体的操作时常数确实有可能更大。所以称其为「更弱」没有问题。

---

EX1 选择题 2-2

Among the following 6 statements about AVL trees and splay trees, how many of them are correct?

1. AVL tree is a kind of height balanced tree. In a legal AVL tree, each node's balance factor can only be $0$ or $1$.

2. Define a single-node tree's height to be $1$. For an AVL tree of height h, there are at most $2^{h} - 1$ nodes.

3. Since AVL tree is strictly balanced, if the balance factor of any node changes, this node must be rotated.

4. In a splay tree, if we only have to find a node without any more operation, it is acceptable that we don't push it to root and hence reduce the operation cost. Otherwise, we must push this node to the root position.

5. In a splay tree, for any non-root node $X$, its parent $P$ and grandparent $G$ (guranteed to exist), the correct operation to splay $X$ to $G$ is to rotate $X$ upward twice.

6. Splaying roughly halves the depth of most nodes on the access path.

=== "A"

    2

=== "B"

    3

=== "C"

    4

=== "D"

    5

??? abstract "答案解析"

    正确答案：A

    解析：正确的说法是 2 和 6。1、4、5 的错误明显，这里着重说一下 3。请注意如果一个节点的平衡因子发生改变，但仍然为 $-1, 0, 1$ 中的一个，那就不需要旋转操作维护平衡。

---

Q2 判断题 1-3

In the worst case the DELETE operation in a RED-BLACK tree of n nodes requires $\Omega(\log n)$ rotations.

??? abstract "答案解析"

    正确答案：F

    解析：红黑树的插入最多进行 2 次旋转，删除最多进行 3 次旋转。

---

HW3 判断题 1-2

When evaluating the performance of data retrieval, it is important to measure the relevancy of the answer set.

??? abstract "答案解析"

    正确答案：F

    解析：评估**数据检索** (data retrieval) 的性能时，我们只关注搜索的响应时间和使用的存储大小。评估**信息检索** (information retrieval) 的性能时，我们才关注检索结果的相关性。

---

Ex3 判断题 1-3

In a search engine, thresholding for query retrieves the top $k$ documents according to their weights.  

??? abstract "答案解析"

    正确答案：F

    解析：在搜索引擎中，「阈值过滤」与「取前 k 个文档」是两种不同的检索策略。阈值过滤是为每个文档分配一个评分，然后只返回分数超过某个固定阈值的所有文档。文档数量不固定，可多可少。

---

HW4 程序填空题 5-1

```c
if ( )
    swap(H1, H2);  //swap H1 and H2
```

??? abstract "答案解析"

    正确答案：`H1->Element > H2->Element`

    解析：左式堆合并时，取两个根节点中较小的作为新堆的根。因此题目中应当将较小的堆换为 `H1`。

---

Ex4 判断题 1-2

The number of light nodes along the right path of a skew heap is $O(\log N)$.

??? abstract "答案解析"

    正确答案：T

    解析：轻节点指的是该节点的字数大小不大于其父节点的字数大小的一半。于是我们考察从根沿右孩子一路向下的右路径：经过 $k$ 个轻节点后，子树大小至多为 $N \cdot 2^{-k}$。子树大小至少为 $1$，于是有

    $$N \cdot 2^{-k} \geq 1$$

    解得

    $$k \leq \lfloor \log N \rfloor$$

    即右路径上的轻节点个数为 $O(\log N)$。

---

Ex4 判断题 1-5

With the same operations, the resulting skew heap is always more balanced than the leftist heap.

??? abstract "答案解析"

    正确答案：F

    解析：左式堆强制维护一个度量 NPL，保证任何堆的右路径长度在最坏情况为 $O(\log N)$，也就是有一个确定的平衡上界。斜堆（skew heap）不维护任何额外的平衡信息，只是在每次合并时交换左右子树以做自适应调整。它只有摊还的 $O(\log N)$ 的性能保证，但没有最坏情况的右路径长度界：在特定的、刻意设计的合并/插入序列下，斜堆可以变得非常不平衡，右链长度可达到 $O(N)$。

---

Ex4 判断题 1-7

If we merge two heaps represented by complete binary trees, the time complexity is $\Theta (N)$ provided that the size of each heap is $N$.

??? abstract "答案解析"

    正确答案：T

    解析：若两个堆都是完全二叉树且采用数组式二叉堆表示，那么将它们合并通常的做法是：把两个数组直接拼接得到大小为 $2N$ 的数组；对新数组执行一次线性建堆，复杂度即为 $O(2N) = O(N)$。要注意这里的堆是普通二叉堆而不是左式堆或斜堆。

---

Ex5 判断题 1-1

To implement a binomial queue, the subtrees of a binomial tree are linked in increasing sizes.

??? abstract "答案解析"

    正确答案：F

    解析：一般二项队列的子树是从大到小连接。

---

Ex7 判断题 1-3

Given two $n \times n$ martices $A$ and $B$, the time complexity of the simple matrix multiplication $C = A \cdot B$ is $O(n^{3})$. Now let's consider the following Divide and Conquer idea:

Divide each matrix into four $\frac{n}{2} \times \frac{n}{2}$ submatrics as follows:

$$\begin{bmatrix}
C_{1} & C_{2} \\
C_{3} & C_{4}
\end{bmatrix} =
\begin{bmatrix}
A_{1} & A_{2} \\
A_{3} & A_{4}
\end{bmatrix} \cdot
\begin{bmatrix}
B_{1} & B_{2} \\
B_{3} & B_{4}
\end{bmatrix}$$

We recursively calculate each block of $C$ as $C_{1} = A_{1} \cdot B_{1} + A_{2} \cdot B_{3}$ and so on.  This can reduce the time complexity of the simple calculation.

??? abstract "答案解析"

    正确答案：F

    解析：计算每个子乘积时需要 $8$ 次规模为 $\frac{n}{2}$ 的矩阵乘法，因此时间复杂度满足递推式：

    $$T(n) = 8 T(\frac{n}{2}) + O(n^{2})$$

    由主定理得其复杂度为 $O(n^{3})$，因此并没有降低复杂度。

---

Ex7 选择题 2-2

Consider two disjoint sorted arrays $A[1 \cdots m]$ and $B[1 \cdots n]$, we would like to compute the $k$-th smallest element in the union of the two arrays, where $k \leq \min \{m, n\}$. Please choose the smallest possible running time among the following options.

=== "A"

    $O(\log k)$

=== "B"

    $O(\log m)$

=== "C"

    $O(\log n)$

=== "D"

    $O(\log m + \log n)$

??? abstract "答案解析"

    正确答案：A

    解析：因为 $A$ 和 $B$ 都已排序且 $k \leq \min \{m, n\}$，故可以在「从 $A$ 中取多少个元素」上做二分搜索。设我们取 $i$ 个来自 $A$，则取 $k - i$ 个来自 $B$。此时有三种情况：

    - 如果 $A_{i} \leq B_{k - i + 1}$ 且 $A_{i + 1} \geq B_{k - i}$，则第 $k$ 小元素是 $\max \{A_{i}, B_{k - i}\}$。
    - 如果 $A_{i} > B_{k - i + 1}$ 则说明我们从 $A$ 取的太多，向左区间内做二分搜索。
    - 如果 $A_{i + 1} < B_{k - i}$ 则说明我们从 $A$ 取的太少，向右区间内做二分搜索。

    二分的总次数为 $O(\log k)$，且每次搜索只做常数次比较，故总的时间复杂度为 $O(\log k)$。

---

期中考 判断题 1-2

After merging two Leftist Heaps $H_{1}$ and $H_{2}$ of different NPLs, the NPL of the resulted Leftist Heap's root could not be $\max(\text{NPL}(H_{1}), \text{NPL}(H_{2})) + 1$.

??? abstract "答案解析"

    正确答案：F

    解析：当 $\text{NPL}(H_{1}) = \text{NPL}(H_{2}) = k$ 时，合并后的 NPL 即为 $k + 1$。

---

期中考 判断题 1-8

The recurrence $T(n) = 2 T(\frac{n}{2}) + \frac{n}{\log n}$ can't be solved by the Master Theorem.

??? abstract "答案解析"

    正确答案：T

    解析：$\frac{n}{\log n}$ 既不属于 $n^{1 + \epsilon}$，也不属于 $n^{1 - \epsilon}$。

---

期中考 程序填空题 5-1

```c
for(int i = 1; i < numsSize; i++) {
    for( ) {
    }
}
```

??? abstract "答案解析"

    正确答案：`int j = 0; j < i; j++`

    解析：记得看循环变量在外部有没有定义。

---

Ex9 判断题 1-1

A binary tree that is not full cannot correspond to an optimal prefix code.

??? abstract "答案解析"

    正确答案：T

    解析：满二叉树指的是没有节点只有一个子节点的二叉树。

---

Ex9 判断题 1-3

The Huffman code is one kind of optimal prefix codes. For a given alphabet and its characters' frequencies，the Huffman codes may not be unique, but the Huffman code length of each character is unique.

??? abstract "答案解析"

    正确答案：T

    解析：在 Huffman 树中，同样权重的节点可能在不同层。

---

Ex9 选择题 2-2

In Activity Selection Problem, we are given a set of activities $S = \{ a_{1}, a_{2}, \cdots, a_{n} \}$ that wish to use a resource (e.g. a room). Each $a_{i}$ takes place during a time interval $[ s_{i}, f_{i} )$.

Let us consider the following problem: given the set of activities $S$, we must schedule them all using the minimum
number of rooms.

**Greedy1:**

Use the optimal algorithm for the Activity Selection Problem  to find the max number of activities that can be scheduled in one room. Delete and repeat on the rest, until no activities left.

**Greedy2:**

- Sort activities by start time. Open room $1$ for $a_{1}$.
- for $i = 2$ to $n$, if $a_{i}$ can fit in any open room, schedule it in that room; otherwise open a new room for $a_{i}$.

Which of the following statement is correct?

=== "A"

    None of the above two greedy algorithms are optimal.

=== "B"

    Greedy1 is an optimal algorithm and Greedy2 is not.

=== "C"

    Greedy2 is an optimal algorithm and Greedy1 is not.

=== "D"

    Both of the above two greedy algorithms are optimal.

??? abstract "答案解析"

    正确答案：C

    解析：第一个算法中，让单个房间的活动最多可能会导致剩下来的活动彼此冲突，不利于总房间数的最小化。

---

HW10 判断题 1-5

If a problem can be solved by dynamic programming, it must be solved in polynomial time.

??? abstract "答案解析"

    正确答案：F

    解析：一些动态规划问题，如背包问题的复杂度是伪多项式的，故不能保证。

---

Q10 判断题 1-5

Greedy algorithm works only if the local optimum is equal to the global optimum.

??? abstract "答案解析"

    正确答案：F

    解析：贪心算法虽然每一步选择最优解，但这种选择往往是有技巧的，并不是简单的「全局最优」。因此贪心算法的正确性不依赖于局部最优和全局最优的等价性。

---

Ex10 判断题 1-3

If $L_{1} \leq_{p} L_{2}$ and $L_{2} \in \text{NP}$, then $L_{1} \in \text{NP}$.

??? abstract "答案解析"

    正确答案：T

    解析：如果能在多项式时间内验证 $L_{2}$ 的解，并且在多项式时间内将 $L_{1}$ 规约为 $L_{2}$，那么就能在多项式时间内验证 $L_{1}$ 的解。

---

Ex10 选择题 2-5

Which one of the following statements is FALSE?

=== "A"

    SAT, Vertex Cover, Hamiltonian Cycle, Clique, Knapsack, Bin Packing, and Domination Set problems are all NP-completeness problems.

=== "B"

    If there is a polynomial time $(1 + \frac{1}{2n})$ -approximation algorithm for Vertex Cover with $n$ being the total number of vertices in the graph, then P=NP.

=== "C"

    If there is a polynomial time 3/2-approximation algorithm for K-Center, then P=NP.

=== "D"

    Given a weighted directed acyclic graph (DAG) $G$ and a source vertex $s$ in $G$, it is NP-hard to find the longest distances from $s$ to all other vertices in $G$.

??? abstract "答案解析"

    正确答案：D

    解析：B 选项：如果存在一个趋近于 $1$ 的近四比，那么就可以在多项式时间内恢复最优解。从而得到 $\text{P} = \text{NP}$；C 选项：这是一个结论，K 聚类问题的近似算法无法做到小于 $2$-近似，除非 $\text{P} = \text{NP}$；D 选项：在一般有向图中最长路径是 NP-hard 问题，但是 DAG 中最长路径是多项式可解的问题。

---

Ex10 选择题 2-6

Which one of the following statements is FALSE?

=== "A"

    A language $L_{1}$ is polynomial time transformable to $L_{2}$ if there exists a polynomial time function $f$ such that $w \in L_{1}$ if $f(w) \in L_{2}$.

=== "B"

    $L_{1} \leq_{p} L_{2}$ and $L_{2} \leq_{p} L_{3}$ then $L_{1} \leq_{p} L_{3}$.

=== "C"

    If $L_{1} \in \text{P}$ then $L_{1} \in \text{NP} \cap \text{co-NP}$.

=== "D"

    If language $L_{1}$ has a polynomial reduction to language $L_{2}$, then the complement of $L_{1}$ has a polynomial reduction to the complement of $L_{2}$.

??? abstract "答案解析"

    正确答案：A

    解析：A 选项：正确的多项式时间规约定义是 $w \in L_{1}$ 当且仅当 $f(w) \in L_{2}$；C 选项：$\text{P}$ 在补运算下是封闭的；D 选项：$L_{1} \leq_{p} L_2$ 当且仅当 $\bar{L_{1}} \leq_{p} \bar{L_2}$。

---

HW11 判断题 1-3

Suppose ALG is an $\alpha$-approximation algorithm for an optimisation problem $\Pi$ whose approximation ratio is tight. Then for every $\epsilon > 0$ there is no $(\alpha - \epsilon)$-approximation algorithm for $\Pi$ unless $\text{P} = \text{NP}$.

??? abstract "答案解析"

    正确答案：F

    解析：一个算法的近似比是「紧的」，仅仅意味着该算法在最坏情况下的性能比确实达到了 $\alpha$，即存在问题的实例使得算法得到的解与最优解的比值恰好为 $\alpha$（或收敛于 $\alpha$）。但这只说明了该算法本身的分析是紧的，并不代表问题 $\Pi$ 在计算复杂性意义上具有近似下界。
    
    问题的近似下界需要单独证明，通常需要基于复杂性假设（如 $\text{P} = \text{NP}$）来证明不存在比某个比率更好的近似算法。而仅从某个算法的近似比是紧的这一事实，并不能推出其他算法无法取得更好的近似比。
    
    所以，原陈述的结论并不成立，除非问题 $\Pi$ 本身已被证明在 $\text{P} = \text{NP}$ 的条件下不存在比 $\alpha$ 更好的近似算法，但这一点并不能从算法 ALG 的近似比是紧的推导出来。

---

Q11 判断题 1-6

Given that problem A is NP-complete. If problem B is in NP and can be polynomially reduced to problem A, then problem B is NP-complete.

??? abstract "答案解析"

    正确答案：F

    解析：当一个 NPC 问题可以规约到另一个问题时，被规约的问题才是 NPC 问题。将一个问题归约到 NPC 问题上不能证明任何原问题的复杂度。

---

Ex11 判断题 1-2

An $(1 + \epsilon)$-approximation scheme of time complexity $(n + \frac{1}{\epsilon})^{3}$ is a PTAS but not an FPTAS.

??? abstract "答案解析"

    正确答案：F

    解析：PTAS 要求对任何确定的 $\epsilon > 0$，复杂度对 $n$ 是多项式时间；FPTAS 要求复杂度对 $n$ 和 $\frac{1}{\epsilon}$ 都是多项式时间。

---

Ex11 判断题 1-3

In the bin packing problem, we are asked to pack a list of items $L$ to the minimum number of bins of capacity $1$.  For the instance $L$, let $FF(L)$ denote the number of bins used by the algorithm First Fit. The instance $L'$ is derived from $L$ by deleting one item from $L$. Then $FF(L')$ is at most of $FF(L)$.

??? abstract "答案解析"

    正确答案：F

    解析：有反例：$\text{Bin Size} = 1, L = \{ 0.55, 0.7, 0.55, 0.1, 0.45, 0.15, 0.3, 0.2 \}, L' = L - \{ 0.1 \} = \{ 0.55, 0.7, 0.55, 0.45, 0.15, 0.3, 0.2 \}$。

---

Ex11 判断题 1-4

For an approximation algorithm for a minimization problem, given that the algorithm does not guarantee to find the optimal solution, the best approximation ratio possible to achieve is a constant $\alpha > 1$.

??? abstract "答案解析"

    正确答案：F

    解析：尽管近似算法不保证找到最优解，但是其复杂度可以无限趋近于 $1$，而不会卡在某个常数上。

---

Ex11 选择题 2-2

Assume $\text{P} \neq \text{NP}$, please identify the false statement.

=== "A"

    There cannot exist a $\rho$-approximation algorithm for bin packing problem for any $\rho < \frac{3}{2}$.

=== "B"

    In the minimum-degree spanning problem, we are given a graph G=(V, E) and wish to find a spanning tree T of G so as to minimize the maximum degree of nodes in T. Then it is NP-complete to decide whether or not a given graph has minimum-degree spanning tree of maximum degree two.

=== "C"

    In the minimum-degree spanning problem, we are given a graph G=(V, E) and wish to find a spanning tree T of G so as to minimize the maximum degree of nodes in T. Then there exists an algorithm with approximation ratio less than 3/2.

=== "D"

    In the knapsack problem, for any given real number ϵ>0, there exists an algorithm with approximation ratio less than 1+ϵ.

??? abstract "答案解析"

    正确答案：C

    解析：B 选项：最大度不大于 $2$ 的生成树等价于 Hamiltonian 路径，这是一个 NPC 问题；C 选项：在 $\text{P} \neq \text{NP}$ 的前提下，最小度生成树的近似算法存在近似比下界 $\frac{3}{2}$；D 选项：Knapsack 存在任意 $1 + \epsilon$ 的近似算法，这与 $\text{P}$ 是否等于 $\text{NP}$ 无关。

---

HW12 判断题 1-1

For the graph given in the following figure, if we start from deleting the black vertex, then local search can always find the minimum vertex cover.

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/advanced_data_structure/mistakes_1.png" width="70%" style="margin: 0 auto;">
</div>

??? abstract "答案解析"

    正确答案：T

    解析：在此例中，最优解中的顶点无法被删去，否则无法得到任何可行解。在这种情况下，我们确实可以保证得到最优解。

---

Ex12 判断题 1-1

For an optimization problem, given a neighborhood, if its local optimum is also a global optimum, one can reach an optimal solution with just one step of local improvements.

??? abstract "答案解析"

    正确答案：F

    解析：仅通过一次改进，只能得到一个更优的邻居解，而不能保证得到了局部最优解。

---

Ex12 判断题 1-4

Without any assumptions on the distances, if $\text{P} \neq \text{NP}$, there is no $\rho$-approximation for TSP (Travelling Salesman Problem) for any $\rho \geq 1$.

??? abstract "答案解析"

    正确答案：T

    解析：在 $\text{P} \neq \text{NP}$ 和没有三角不等式的前提下，旅行商问题不存在任何常数因子的近似算法。

---

Ex12 选择题 2-1

Consider the minimum-degree spanning tree problem: given a connected undirected graph $G(V, E)$, find a spanning tree $T$ that minimizes the maximum degree over all vertices among all spanning trees of $G$. This problem can be shown to be NP-hard via a reduction from the Hamiltonian path problem. On the other hand, we can design an approximation algorithm using local search. Let $d(u)$ denote the degree of vertex $u$ in tree $T$. Consider the following algorithm:

1. Find an arbitrary spanning tree $T$ of $G$.
2. If there exists an edge $e \in E(G)\setminus E(T)$ with endpoints $u, v$, such that on the path between $u$ and $v$ in $T$ there is some other vertex $w$ satisfying $\max\{d(u), d(v)\} + 1 < d(w)$, then replace an edge $e'$ incident to $w$ in $T$ with $e$, i.e., set $T := T \cup \{e\} \setminus \{e'\}$.
3. Repeat step (2) until no such edge exists.

It can be shown that this algorithm terminates with a solution whose maximum vertex degree is $OPT + O(\log |V|)$. To prove that the algorithm terminates in a finite number of steps, a useful technique is to define a non-negative potential function $\phi(T)$ and show that $\phi(T)$ strictly decreases in each iteration. Which of the following potential functions satisfies this requirement?

=== "A"

    $\phi(T) = \sum_{v \in V} d(v)$

=== "B"

    $\phi(T) = \sum_{(u,v) \in E(T)} \max\{d(u), d(v)\}$

=== "C"

    $\phi(T) = \sum_{u \in V} \sum_{v \in V, v \ne u} \sum_{w \in V, w \ne u,v} \max\{d(u), d(v), d(w)\}$

=== "D"

    $\phi(T) = \sum_{v \in V} 3^{d(v)}$

??? abstract "答案解析"

    正确答案：D

    解析：A 选项：$\sum_{v \in V} d(v) = 2(|V| - 1)$ 为定值，同时也说明了 D 选项为什么正确，因为和一定，每个点的度数变得更平均了，指数平均就会降低；B 选项，一步操作后可能会出现 $\max \{d(u) + 1, d(v) + 1\}$ 从而导致该函数增大；C 选项：整体的三元组的最大值可能不变。

---

Ex12 选择题 2-2

**Load balancing problem:**

We have $n$ jobs $j = 1, 2, \ldots, n$ each with processing time $p_j$ being an integer number.  
Our task is to find a schedule assigning $n$ jobs to 10 identical machines so as to minimize the makespan (the maximum completion time over all the machines).  
We adopt the following local search to solve the above load balancing problem.

**LocalSearch:**

Start with an arbitrary schedule.  
Repeat the following until no job can be re-assigned:

- Let $l$ be a job that finishes last.
- If there exists a machine $i$ such that assigning job $l$ to $i$ allows $l$ to finish earlier, then re-assign $l$ to be the last job on machine $i$.
- If such a machine is not unique, always select the one with the minimum completion time.

We claim the following four statements:

1. The algorithm LocalSearch finishes within polynomial time.
2. The Load-balancing problem is NP-hard.
3. Let OPT be the makespan of an optimal algorithm. Then the algorithm LocalSearch finds a schedule with the makespan at most of 1.8 OPT.
4. This algorithm finishes within $O(n^2)$.

How many statements are correct?

=== "A"

    0

=== "B"

    1

=== "C"

    2

=== "D"

    3

=== "E"

    4

??? abstract "答案解析"

    正确答案：D

    解析：只有第三条陈述是错的，该问题的局部搜索能保证的近似比是 $2 - \frac{1}{m}$，其中 $m$ 为机器数。

---

Ex12 选择题 2-4

Consider the metric Facility Location problem. A company wants to distribute its product to various cities. There is a set $I$ of potential locations where a storage facility can be opened and a fixed “facility cost” $f_i$ associated with opening a storage facility at location $i \in I$. (Sometimes we will say “facility $i$” to mean “facility at location $i$”). There also is a set $J$ of cities to which the product needs to be sent, and a “routing cost” $c(i,j)$ associated with transporting the goods from a facility at location $i$ to city $j$. The goal is to pick a subset $S$ of $I$ so that the total cost of opening the facilities and transporting the goods is minimized. In short, we want to minimize $C(S) = C_f(S) + C_r(S)$, where $C_f(S) = \sum_{i \in S} f_i$ and $C_r(S) = \sum_{j \in J} \min_{i \in S} c(i,j)$. Consider the following local search algorithm:

1. Picking any subset $S$ of the set $I$ of facilities. This gives us a feasible solution right away.
2. We then search for the local neighborhood of the current feasible solution to see if there is a solution with a smaller objective value; if we find one we update our feasible solution to that one.
3. We repeat step 2 until we do not find a local neighbor that yields a reduction in the objective value.

There are two types of “local steps” that we take in searching for a neighbor: i) remove/add a facility from/to the current feasible solution, or ii) swap a facility in our current solution with one that is not.

Which of the following statement is true?

=== "A"

    This algorithm is 2-approximation.

=== "B"

    Let $S$ be a local optimum that the above algorithm terminates with, and $S^*$ be a global optimum. Then $C_r(S) \geq C(S^*)$.

=== "C"

    Let $S$ be a local optimum that the above algorithm terminates with, and $S^*$ be a global optimum. Then $C_r(S) \leq C(S^*)$.

=== "D"

    None of the other options are correct.

??? abstract "答案解析"

    正确答案：C

    解析：[文献](https://dl.acm.org/doi/10.1145/380752.380755)题，记住性质即可。A 选项：该算法是 $3 + \epsilon$ 的；B、C 选项都是论文中的结论。

---

HW13 判断题 1-1

Let $a = (a_{1}, a_{2}, \cdots, a_{i}, \cdots, a_{j}, \cdots, a_{n})$ denote the list of elements we want to sort. In the quicksort algorithm, if the pivot is selected uniformly at random. Then any two elements get compared at most once and the probability of $a_{i}$ and $a_{j}$ being compared is $\frac{2}{j - i + 1}$ for $j > i$, given that $a_{i}$ or $a_{j}$ is selected as the pivot.

??? abstract "答案解析"

    正确答案：F

    解析：对于**已经排序好的最终序列**，其中的 $a_{i}$ 和 $a_{j}$ 被比较的概率确实是 $\frac{2}{j - i + 1}$。因为其只会在完成对 $a_{i}$ 到 $a_{j}$ 这 $j - i + 1$ 个数的排序中被比较，而恰好选到 $a_{i}$ 或 $a_{j}$ 作 pivot 的可能情况只有两种。

    而题目中的 $a_{i}$ 和 $a_{j}$ 是原始**未排序序列**中的数，不具有任何有序性，所以上述讨论是无意义的，自然也不能导出对应的概率结论。

---

Ex13 判断题 1-2

A randomized Quicksort algorithm has an $O(N \log N)$ expected running time, only if all the input permutations are equally likely.

??? abstract "答案解析"

    正确答案：F

    解析：随机化快速排序的期望复杂度保证来自于选取 pivot 时的等概率，和输入序列无关。

---

Ex13 判断题 1-4

A Las Vegas algorithm is a randomized algorithm that always gives the correct result, however the runtime of a Las Vegas algorithm differs depending on the input.

A Monte Carlo algorithm is a randomized algorithm whose output may be incorrect with a certain (typically small) probability. The running time for the algorithm is fixed however.

Then if a Monte Carlo algorithm runs in $O(n^2)$ time, with the probability 50\% of producing a correct solution, then there must be a Las Vegas algorithm that can get a solution in $O(n^2)$ time in expectation.

??? abstract "答案解析"

    正确答案：F

    解析：尽管我们确实可以通过综合蒙特卡洛算法和拉斯维加斯算法使得在相对有限的时间内得到相对正确的结果，但是题目中没有给出「验证」答案的复杂度，有可能在这一步产生比较巨大的时间开销。

---

Ex13 选择题 2-1

In the maximum satisfiability problem (MAX SAT), the input consists of $n$ Boolean variables $x_1, \ldots, x_n$, $m$ clauses $C_1, \ldots, C_m$ (each of which consists of a disjunction (that is an “or”) of some number of the variables and their negations, e.g. $x_3 \lor \bar{x}_5 \lor x_{11}$, where $\bar{x}_i$ is the negation of $x_i$), and a nonnegative weight $w_j$ for each clause $C_j$. The objective of the problem is to find an assignment of the true/false to the $x_i$ that maximizes the weight of the satisfied clauses.

A variable or a negated variable is a literal. The number of literals in a clause is called its length. Denote $l_j$ to be the length of a clause $C_j$. Clauses of length 1 are called unit clauses.

**Randomized algorithm RA**: Setting each $x_i$ to true with probability $p$ independently.

Which of the following statement is false?

=== "A"

    Let $p = 1/2$, the randomized algorithm RA is a 2-approximation algorithm.

=== "B"

    If $l_j \geq 3$ for each clause $C_j$. Let $p = 1/2$, the randomized algorithm RA is a 9/8-approximation algorithm.

=== "C"

    If MAX SAT instances do not have unit clauses $\bar{x}_i$, we can obtain a randomized $\frac{2}{\sqrt{5}-1} \approx 1.618$-approximation algorithm for MAX SAT.

=== "D"

    One could obtain a better bound on optimal solution than $\sum_{j=1}^m w_j$ for MAX SAT.

??? abstract "答案解析"

    正确答案：B

    解析：A、B 选项：对于长度为 $l$ 的子句，该子句不被满足的概率为 $p^{l}$，故被满足的概率为 $1 - p^{l}$，对应的总近似比就是 $\frac{1}{1 - p^{l}}$；C 选项是结论，当不存在负的单位子句 $\bar{x}_{i}$ 时，纯随机算法的近似比即为 $\frac{2}{\sqrt{5}-1}$；D 选项中的 $\sum_{j=1}^m w_j$ 时一个平凡上界，对应所有子句都被满足的情况，可以通过子句间的互斥、冲突等关系得到更紧的上界。

---

Ex13 选择题 2-3

We have $m$ balls and $m$ boxes. Each ball is assigned to one of the $m$ boxes independently and uniformly at random (i.e., equally likely to each box). Suppose that $m$ is sufficiently large, and $e$ is the natural number, which of the following is FALSE?

=== "A"

    The expected number of balls in a box is $1$.

=== "B"

    The expected number of empty boxes is $\frac{m}{e}$.

=== "C"

    Suppose that one box can only contain one ball, and it will reject other balls if it already contains one. Then, the expected number of rejected balls is $\frac{m}{e}$.

=== "D"

    Suppose a box can accommodate two balls, and will reject any additional balls. The expected number of boxes containing exactly two balls is $\frac{m}{e}$.

??? abstract "答案解析"

    正确答案：D

    解析：B、C 选项：一个固定箱子为空的概率为 $\lim_{m \to +\infty} (1 - \frac{1}{m})^{m} = \frac{m}{e}$；D 选项：当 $m$ 很大时，单个箱子中的球数近似服从参数为 $1$ 的泊松分布，于是 $P \{X = 2\} = \frac{1^{2}}{2!} e^{-1} = \frac{1}{2e}$。

---

Ex13 选择题 2-4

To find the $k$th smallest number in a set $S$, randomized quick selection algorithm works in the following way:

1. If $|S| = 1$, then $k = 1$ and return the only element in $S$.
2. Randomly select a central splitter $p \in S$, which is a pivot that divides the set so that each side contains at least $|S|/4$ elements.
3. Partition $S - \{p\}$ into $S_1$ and $S_2$, as was done with quicksort.
4. If $k \leq |S_1|$, recursively find the $k$th smallest number in $S_1$. If $k = |S_1| + 1$, return the pivot as the answer. Otherwise, recursively find the $(k - |S_1| - 1)$st smallest number in $S_2$.

If $|S| = n$, then the best upper bound of the expected time complexity of this algorithm is:

=== "A"

    $O(n)$

=== "B"

    $O(n^2)$

=== "C"

    $O(n \log n)$

=== "D"

    $O((\frac{3}{4})^n)$

??? abstract "答案解析"

    正确答案：A

    解析：做分治分析。划分操作，即额外操作的复杂度为 $O(n)$，根据题目条件，划分完一边的规模至少有 $\frac{n}{4}$，也就是说较大的一遍的规模不超过 $\frac{3n}{4}$，于是可得递推式 $T(n) \leq T(\frac{3n}{4}) + O(n)$。应用主定理求解即可。

---

HW14 判断题 1-4

In order to solve the maximum finding problem by a parallel algorithm with $T(n) = O(1)$, we need work load $W(n) = \Omega(n^{2})$ in return.

??? abstract "答案解析"

    正确答案：F

    解析：在 CRCW PRAM 模型中，存在 $T(n) = O(1), W(n) = O(n)$ 的算法。

---

Q14 判断题 1-1

Consider the online hiring problem, in which we have total $k$ candidates. First of all, we interview $n$ candidates but reject them all. Then we hire the first candidate who is better than all of the previous candidates you have interviewed. It is true that the probability of the $m$th candidate is the best is $\frac{n}{k(m-1)}$, where $m > n$.

??? abstract "答案解析"

    正确答案：T

    解析：录取到第 $m$ 个人且为最优包含独立的两部分事件，首先第 $m$ 个人是最优的概率为 $\frac{1}{k}$，其次前 $m - 1$ 个人中最优的人出现在前 $n$ 个的概率为 $\frac{n}{m - 1}$，因为我们只会录取第一个超过这个 pivot 的人，两部分相乘即得。

---

Q14 选择题 2-1

Given a 3-SAT formula with $k$ clauses, in which each clause has three variables, the MAX-3SAT problem is to find a truth assignment that satisfies as many clauses as possible. A simple randomized algorithm is to flip a coin, and to set each variable true with probability $1/2$, independently for each variable. Which of the following statements is FALSE?

=== "A"

    If we repeatedly generate random truth assignments until one of them satisfies $\geq \frac{7k}{8}$ clauses, then this algorithm is a $\frac{8}{7}$-approximation algorithm.

=== "B"

    The expected number of clauses satisfied by this random assignment is $\frac{7k}{8}$.

=== "C"

    For every instance of 3-SAT, there is a truth assignment that satisfies at least a $\frac{7}{8}$ fraction of all clauses.

=== "D"

    The probability that a random assignment satisfies at least $\frac{7k}{8}$ clauses is at most $\frac{1}{8k}$.

??? abstract "答案解析"

    正确答案：D

    解析：C 选项：由于随机赋值得到正确子句的数量期望为 $\frac{7k}{8}$，所以至少有一种赋值使得正确子句的数量大于 $\frac{7k}{8}$；D 选项：和 C 同理，如果概率那么小的话，期望不可能那么大。

---

Ex14 选择题 2-3

When measure the performance of parallel algorithm, we often use work load ($W(n)$) and worst-case running time ($T(n)$). How many evaluation metrics are asymptotically equivalent to $W(n)$ and $T(n)$?

- $P(n) = W(n)/T(n)$ processors and $T(n)$ time (on a PRAM)
- $W(n)/p$ time using any number of $p \geq W(n)/T(n)$ processors (on a PRAM)
- $W(n)/p + T(n)$ time using any number of $p$ processors (on a PRAM)

=== "A"

    0

=== "B"

    1

=== "C"

    2

=== "D"

    3

??? abstract "答案解析"

    正确答案：C

    解析：3 个等价的指标分别是：

    - $P(n) = \frac{W(n)}{T(n)}$
    - **当 $p \leq \frac{W(n)}{T(n)}$ 时**，$\frac{W(n)}{p}$
    - $\forall p, \frac{W(n)}{p} + T(n)$

---

Q15 判断题 1-3

If we translate a serial algorithm into a reasonably efficient parallel algorithm, the work load and the worst-case running time are usually reduced.

??? abstract "答案解析"

    正确答案：F

    解析：最坏运行时间确实通常减少，因为允许在同一时间多个处理器同时操作；但总工作量一般不会减少，甚至还会略微增加，因为还额外产生了将并行结果合并的操作。

---

Ex15 判断题 1-1

Suppose that the replacement selection is applied to generate longer runs for N numbers with a priority queue of size M, the possible maximum length of the longest run is N.

??? abstract "答案解析"

    正确答案：T

    解析：替换选择下，最长 run 的期望长度是 $2M$，但是实际长度没有限制。当数据从小到大排列进入堆时，即可产生长度为 $N$ 的 run。

---

Ex15 判断题 1-2

In general, for a 3-way merge we need 6 input buffers and 2 output buffers for decreasing the number of passes.

??? abstract "答案解析"

    正确答案：F

    解析：采用 $2k$ 个输入缓冲区和 $2$ 个输出缓冲区的目的是减少输入输出的等待时间，和减少趟数没有关系。

---

Ex15 判断题 1-3

Given 1000 runs and 8 tapes. If simple k-way merge is used, the minimum number of passes required is 5 (runs generation pass is not counted).

??? abstract "答案解析"

    正确答案：T

    解析：趟数的公式为 $1 + \lceil \log_{k} \frac{N}{M} \rceil$，在本题中，$N = 1000$，$k = 8 - 1 = 7$，因为要分 1 条磁带作为输出磁带，因为是「simple」的 k 路合并，所以 $M = 1$。
