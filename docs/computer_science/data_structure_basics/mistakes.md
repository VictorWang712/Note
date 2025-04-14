---
comments: true
---

# 错题整理

第五周 单选题 2-5

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

期中考 单选题 2-8

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

期中考 单选题 2-13

If an undirected graph G = (V, E) contains 12 vertices. Then to guarantee that G is connected in any cases, there has to be at least __ edges.

=== "A"

    12

=== "B"

    67

=== "C"

    11

=== "D"

    66

正确答案：C

解析：「in any cases」指的是对于所有连通图中找边最少的一种，而非在确定边数的情况下找确定能连通的。
