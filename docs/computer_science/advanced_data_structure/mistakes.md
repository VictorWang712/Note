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

HW10 判断题 1-5

If a problem can be solved by dynamic programming, it must be solved in polynomial time.

??? abstract "答案解析"

    正确答案：F

    解析：一些动态规划问题，如背包问题的复杂度是伪多项式的，故不能保证。

---

HW11 判断题 1-3

Suppose ALG is an $\alpha$-approximation algorithm for an optimisation problem $\Pi$ whose approximation ratio is tight. Then for every $\epsilon > 0$ there is no $(\alpha - \epsilon)$-approximation algorithm for $\Pi$ unless $\text{P} = \text{NP}$.

??? abstract "答案解析"

    正确答案：F

    解析：一个算法的近似比是「紧的」，仅仅意味着该算法在最坏情况下的性能比确实达到了 $\alpha$，即存在问题的实例使得算法得到的解与最优解的比值恰好为 $\alpha$（或收敛于 $\alpha$）。但这只说明了该算法本身的分析是紧的，并不代表问题 $\Pi$ 在计算复杂性意义上具有近似下界。
    
    问题的近似下界需要单独证明，通常需要基于复杂性假设（如 $\text{P} = \text{NP}$）来证明不存在比某个比率更好的近似算法。而仅从某个算法的近似比是紧的这一事实，并不能推出其他算法无法取得更好的近似比。
    
    所以，原陈述的结论并不成立，除非问题 $\Pi$ 本身已被证明在 $\text{P} = \text{NP}$ 的条件下不存在比 $\alpha$ 更好的近似算法，但这一点并不能从算法 ALG 的近似比是紧的推导出来。

---

HW12 判断题 1-1

For the graph given in the following figure, if we start from deleting the black vertex, then local search can always find the minimum vertex cover.

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/advanced_data_structure/mistakes_1.png" width="70%" style="margin: 0 auto;">
</div>

??? abstract "答案解析"

    正确答案：T

    解析：在此例中，最优解中的顶点无法被删去，否则无法得到任何可行解。在这种情况下，我们确实可以保证得到最优解。
