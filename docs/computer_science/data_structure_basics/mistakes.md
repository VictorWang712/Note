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
