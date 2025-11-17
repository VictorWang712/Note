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

    解析：
