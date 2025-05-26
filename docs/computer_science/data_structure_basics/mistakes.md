---
comments: true
---

# 错题整理

第五周 选择题 2-5

Among the following binary trees, which one can possibly be the decision tree (the external nodes are excluded) for binary search?

=== "A"

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/mistakes_1.png" width="70%" style="margin: 0 auto;">
    </div>

=== "B"

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/mistakes_2.png" width="70%" style="margin: 0 auto;">
    </div>

=== "C"

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/mistakes_3.png" width="70%" style="margin: 0 auto;">
    </div>

=== "D"

    <div style="text-align: center; margin-top: 0px;">
    <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/mistakes_4.png" width="70%" style="margin: 0 auto;">
    </div>

正确答案：A

解析：在二分搜索中，每次求中间值时向下取整还是向上取整是唯一确定的。对应地，向下取整会导致剩下的小于中间值的值少于大于中间值的值，从而使得决策树上的中间值节点的左子树在大小上小于右子树；向上取整则反之。因此本题就是需要判断哪个树的每一个节点都满足左子树小于右子树，或反之。

---

期中考 选择题 2-8

Suppose that the level-order traversal sequence of a max-heap is { 82, 65, 17, 26, 8, 12, 3 }. Use the linear algorithm to adjust this max-heap into a min-heap, and then call DeleteMin. The preorder traversal sequence of the resulting tree is:

=== "A"

    8, 26, 82, 65, 12, 17

=== "B"

    8, 17, 12, 26, 65, 82

=== "C"

    26, 65, 17, 82, 12, 8

=== "D"

    8, 17, 26, 65, 12, 82

正确答案：D

解析：线性时间建堆指的是，对于任何一个完全二叉树，从最后一个非叶子节点开始向下调整。

---

期中考 程序填空题 5-2

```c
T->Left = BuildTree( );
```

正确答案：`in + 0, pre + 1, i`

解析：从中间访问数组应当用指针的加减法运算实现。

---

第十一周 判断题 1-1

For a graph, if each vertex has an even degree or only two vertexes have odd degree, we can find a cycle that visits every edge exactly once.

正确答案：F

解析：题目中要求的是「cycle」，即欧拉回路，故顶点只能是全偶度数。

---

第十一周 选择题 2-2

Graph G is an undirected completed graph of 20 nodes. Is there an Euler circuit in G? If not, in order to have an Euler circuit, what is the minimum number of edges which should be removed from G?

=== "A"

    Yes, Graph G has an Euler circuit.

=== "B"

    No, Graph G has no Euler circuit. 10 edges should be removed.

=== "C"

    No, Graph G has no Euler circuit. 20 edges should be removed.

=== "D"

    No, Graph G has no Euler circuit. 40 edges should be removed.

正确答案：B

解析：已知在 20 个顶点的完全图中，每个顶点的度数均为 19。于是只需要删去「1-11」「2-12」……「10-20」 这 20 条边，即可使每个顶点变为偶度数。

---

第十二周 选择题 2-1

To sort {8, 3, 9, 11, 2, 1, 4, 7, 5, 10, 6} by Shell Sort, if we obtain (4, 2, 1, 8, 3, 5, 10, 6, 9, 11, 7) after the first run, and (1, 2, 3, 5, 4, 6, 7, 8, 9, 11, 10) after the second run, then the increments of these two runs must be __ , respectively.

=== "A"

    3 and 1

=== "B"

    3 and 2

=== "C"

    5 and 2

=== "D"

    5 and 3

正确答案：B

解析：依次代入 increment 的值模拟即可。

---

第十三周 判断题 1-2

During the sorting, processing every element which is not yet at its final position is called a "run". To sort a list of integers using quick sort,  it may reduce the total number of recursions by processing the small partion first in each run.

正确答案：F

解析：无论先处理较小的区间还是较大的区间，递归调用的次数应该是相同的，处理顺序的不同并不会减少总的递归次数。

---

第十三周 选择题 2-1

During the sorting, processing every element which is not yet at its final position is called a "run".  Which of the following cannot be the result after the second run of quicksort?

=== "A"

    5, 2, 16, 12, 28, 60, 32, 72

=== "B"

    2, 16, 5, 28, 12, 60, 32, 72

=== "C"

    2, 12, 16, 5, 28, 32, 72, 60

=== "D"

    5, 2, 12, 28, 16, 32, 72, 60

正确答案：D

解析：在 D 选项的序列中，第一个 pivot 可以选择 12 或 32。但无论选择哪一个作为第一个 pivot 后，都无法选出第二个 pivot。

---

第十四周 选择题 2-1

The average search time of searching a hash table with $N$ elements is:

=== "A"

    $O(1)$

=== "B"

    $O(\log N)$

=== "C"

    $O(N)$

=== "D"

    cannot be determined

正确答案：D

解析：题目中没有给出散列表的构造方法和解决冲突的策略，因此是无法确定具体的时间复杂度的。
