---
comments: true
---

# 第三章 - 树

## 预备知识

### 树的定义

**树** (tree) 是最基本的数据结构之一。

一种自然的定义树的方式是通过递归的定义方式：一棵树是由称作**根节点** (root) 的节点 $r$ 和若干个（可以为 0 个）非空的子树 $T_{1}, T_{2}, \cdots, T_{k}$ 组成，这些子树中每一棵的根节点都被来自根节点 $r$ 的一条有向**边** (edge) 连接。

从递归定义中我们发现，一棵树是 $N$ 个节点和 $N - 1$ 条边的集合。

每一棵子树的根节点称作根节点 $r$ 的**子节点** (child)，而 $r$ 是每一棵子树的根节点的**父节点** (parent)。没有子节点的节点称作**叶节点** (leaf)，具有相同父节点的节点称作**兄弟节点** (sibling)。类似地，可以定义**祖父节点** (grandparent)、**孙节点** (grandchild)。

节点的**度数** (degree) 指的是该节点的子节点的数量；树的度数指的是树上每个节点的度数的最大值。

从节点 $n_{1}$ 到 $n_{k}$ 的**路径** (path) 定义为节点 $n_{1}, n_{2}, \cdots, n_{k}$ 的一个序列，其中对于 $1 \leq i < k$，节点 $n_{i}$ 是 $n_{i + 1}$ 的父节点。这个路径的**长度** (length) 为该路径上边的条数，即 $k - 1$。从每一个节点都有到它自己有一条长为 $0$ 的路径。

???+ note

    从此定义不难得到，在一棵树中，从根节点到每个节点恰好存在一条路径。

对任意节点 $n_{i}$，$n_{i}$ 的**深度** (depth) 为从根节点到 $n_{i}$ 的唯一路径的长。因此，根节点的深度为 $0$。$n_{i}$ 的**高** (height) 是从 $n_{i}$ 到一个叶节点的最长路径的长。因此，所有叶节点的高都是 $0$。一棵树的高等于其根节点的高，一棵树的深度等于它最深的叶节点的深度，一棵树的高总是与一棵树的深度相等。

如果存在从 $n_{1}$ 到 $n_{2}$ 的一条路径，那么 $n_{1}$ 是 $n_{2}$ 的**祖先节点** (ancestor)，$n_{2}$ 是 $n_{1}$ 的**后裔节点** (decendant)。如果 $n_{1} \neq n_{2}$，那么 $n_{1}$ 是 $n_{2}$ 的**真祖先节点** (proper ancestor)，$n_{2}$ 是 $n_{1}$ 的**真后裔节点** (proper decendant)

### 树的实现

实现树的一个简单方法是：将每个节点的子节点放在父节点的链表中。具体地，我们可以通过如下代码声明树的节点：

```c
typedef struct TreeNode *PtrToNode

struct TreeNode {
    ElementType Element;
    PtrToNode FirstChild, NextSibling;
}
```

> 我们给出一棵按此方法声明的树的具体例子，图中向下的箭头是指向 `FirstChild`（第一子节点）的指针，从左到右的箭头是指向 `NextSibling`（下一兄弟节点）的指针。
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_1.png" width="70%" style="margin: 0 auto;">
> </div>

### 树的遍历

得益于树的子结构的自相似性，不难想到对树的遍历总是依赖递归进行的。只是在递归中的细节顺序的不同产生了不同的遍历方式。

一种遍历的策略称作**先序遍历** (preorder traversal)。在先序遍历中，对某一节点的操作先于对其子节点的操作。

另一种遍历的策略称作**后序遍历** (postorder traversal)。在后序遍历中，对某一节点的操作后于对其子节点的操作。

## 二叉树

### 二叉树的定义

如果一棵树中每个节点的子节点不多于两个，那么我们称这棵树为 **二叉树** (binary tree)。

二叉树最重要的性质是，二叉树的平均深度比 $N$ 要小很多，这一平均值为 $O(\sqrt{N})$。对于特殊类型的二叉树，如**二叉查找树** (binary search tree)，其深度的平均值是 $O(\log N)$。

尽管从定义上出发，二叉树中每个节点的两个子节点是等价的。但是为了后续二叉树的实现和二叉树上算法的遍历性，我们还是将两个子节点分为**左子节点** (left child) 和**右子节点** (right child)。

### 二叉树的实现

因为在二叉树中，每个节点最多有两个子节点，因此我们可以用指针直接指向它们。具体地，我们可以通过如下代码声明二叉树的节点：

```c
typedef struct TreeNode *PtrToNode
typedef struct PtrToNode Tree

struct TreeNode {
    ElementType Element;
    Tree Left, Right;
}
```

### 表达式树

二叉树的一个常见应用即为**表达式树** (expression tree)，尽管这只适用于每种运算都是不高于二元运算的前提下。

表达式树的叶节点是**操作数** (operand)，它可以是常数或变量；其它的节点为**操作符** (operator)。

> 举例来说，表达式 `(a+(b*c))+(((d*e)+f)*g)` 对应的表达式树如下：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_2.png" width="70%" style="margin: 0 auto;">
> </div>

#### 由表达式构造表达式树

在[第二章对栈的讨论](https://victorwang712.github.io/Note/computer_science/data_structure_basics/chapter_2/#_14)中，我们知道表达式存在前缀表达式、中缀表达式和后缀表达式三种，且我们总是可以将表达式转换为后缀表达式。那么出于便捷实现算法的目的，我们常用的是由后缀表达式构造表达式树。

这一算法如下：

$$
\begin{array}{ll}
1 &  \textbf{Input. } \text{The expression } s \text{ under postfix notation.} \\
2 &  \textbf{Output. } \text{The corresponding expression tree for } s. \\
3 &  \textbf{Method. } \\
4 &  \text{make an empty stack} \\
5 &  \textbf{for} \text{ each } s_{i} \text{ in the expression } s \\
6 &  \qquad \textbf{if } s_{i} \text{ is an operand} \\
7 &  \qquad\qquad \text{create a single-node tree with the value } s_{i} \\
8 &  \qquad\qquad \text{push a pointer to the single-node tree into the stack} \\
9 &  \qquad \textbf{else if } s_{i} \text{ is an operator} \\
10 &  \qquad\qquad \textbf{let } a_{i} \text{ be the top of the stack} \\
11 &  \qquad\qquad \text{pop } a_{i} \text{ from the stack} \\
12 &  \qquad\qquad \textbf{let } a_{j} \text{ be the top of the stack} \\
13 &  \qquad\qquad \text{pop } a_{j} \text{ from the stack} \\
14 &  \qquad \text{create a single-node tree with the value } s_{i} \\
15 &  \qquad \textbf{let } \text{the left child pointer of } s_{i} \text{ to } a_{j} \\
16 &  \qquad \textbf{let } \text{the right child pointer of } s_{i} \text{ to } a_{i} \\
17 &  \qquad \text{push a pointer to the node } s_{i} \text{ into the stack} \\
\end{array}
$$

#### 由表达式树生成表达式

根据对表达式树不同的遍历方式，我们就可以得到不同类型的表达式。

最常见的遍历策略是，先对左子树递归生成一个带括号的左表达式，然后输出在根节点处的运算符，最后对右子树递归生成一个带括号的右表达式。这种遍历策略称作**中序遍历** (inorder traversal)，对于生成的表达式即为中缀表达式。

另外两种遍历策略即为前述的先序遍历和后序遍历，在表达式树上它们的具体操作如下：

先序遍历指的是先输出根节点，再递归左子树，最后递归右子树。对应生成的表达式即为前缀表达式。

后序遍历指的是先递归左子树，再递归右子树，最后输出根节点。对应生成的表达式即为后缀表达式。

## 二叉查找树

二叉树的一个重要应用就是查找。为了方便起见，我们给出一些假设：假设树中的每个节点存在一个关键字值，且每个关键字是互异的。更复杂的情况我们将在以后讨论。

使二叉树成为二叉查找树的性质是，对于树中的每个节点 $X$，其左子树中所有节点的关键字值小于 $X$ 的关键字值，右子树中所有节点的关键字值大于 $X$ 的关键字值。

我们首先给出二叉查找树的相关声明，不难分析得到，这样声明得到的二叉查找树的平均深度为 $O(\log n)$。

```c
struct TreeNode;
typedef struct TreeNode *Position;
typedef struct TreeNode *SearchTree;

struct TreeNode {
    ElementType Element;
    SearchTree Left, Right;
}
```

接下来，我们将讨论二叉查找树上的各种操作，并进行相关的复杂度分析。

### MakeEmpty

由于树的递归性质，我们也递归地进行初始化，其例程如下：

```c
SearchTree MakeEmpty(SearchTree T) {
    if (T != NULL) {
        MakeEmpty(T->Left);
        MakeEmpty(T->Right);
        free(T);
    }
    return NULL;
}
```

### Find

`Find` 操作一般返回树 $T$ 中具有关键字 $X$ 的节点的指针，若这样的节点不存在则返回 `NULL`。

同样的这一操作也是递归地进行即可。

```c
Position Find(ElementType X, SearchTree T) {
    if (T == NULL) {
        return NULL;
    }
    else if (X < T->Element) {
        return Find(X, T->Left);
    }
    else if (X > T->Element) {
        return Find(X, T->Right);
    }
    else {
        return T;
    }
}
```

### FindMin 和 FindMax

`FindMin` 和 `FindMax` 操作用于返回树中最小值和最大值的位置。由于二叉查找树的性质，这一操作是简单的，如 `FindMin` 操作只需不断查找左子树直到无左子树为止即可，`FindMax` 反之查找右子树。

???+ warning

    请注意，`FindMin` 和 `FindMax` 操作一般用于返回最小值或最大值的位置，而非其准确值。这是为了与 `Find` 操作相统一。

```c
Position FindMin(SearchTree T) {
    if (T == NULL) {
        return NULL;
    }
    else if (T->Left == NULL) {
        return T;
    }
    else {
        return FindMin(T->Left);
    }
}

Position FindMin(SearchTree T) {
    if (T == NULL) {
        return NULL;
    }
    else if (T->Right == NULL) {
        return T;
    }
    else {
        return FindMin(T->Right);
    }
}
```
### Insert

`Insert` 操作的逻辑与 `Find` 操作相仿。为了将 $X$ 插入到树 $T$ 中，只需在 $T$ 中查找 $X$，如果找到则无需操作（有关重复节点的情况将在后文说明）；否则将 $X$ 插入到查找路径的最后一点上。

> 我们以下图举例：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_3.png" width="70%" style="margin: 0 auto;">
> </div>
>
> 为了插入 $5$，我们按照 `Find` 的方法查找该值，最终到达值为 $4$ 的节点处并希望下一步查找其右子树。但是因为该节点无右子树，故 $5$ 不在该树上，且该位置即为 $5$ 应插入的位置。

如果要插入重复的值，比起再增加节点，我们倾向于记录每个节点的「出现次数」，然后只需将重复值对应节点的出现次数加 $1$ 即可。这样的做法有助于避免树的规模变得过于庞大。

同样地，我们给出 `Insert` 操作的例程。需要注意的是，由于 $T$ 指向该树的根，且根又在第一次插入时变化，所以我们将 `Insert` 的返回值设定为插入操作结束后指向新树根的指针，这一做法也有利于我们递归地实现 `Insert` 操作。

```c
SearchTree Insert(ElementType X, SearchTree T) {
    if (T == NULL) {
        T = malloc(sizeof(struct TreeNode));
        T->Element = X;
        T->Left = T->Right = NULL;
    }
    else {
        if (X < T->Element) {
            T->Left = Insert(X, T->Left);
        }
        else if (X > T->Element) {
            T->Right = Insert(X, T->Right);
        }
        /*Else X is in the tree already, we will do nothing*/
    }
    return T;
}
```

### Delete

鉴于删除时需要考虑的情况较多，`Delete` 操作相对难以实现。因此我们分情况依次讨论。

若目标节点是叶节点，则直接删除即可。

若目标节点有一个子节点，则只需让自己的子节点替代自己成为父节点的左节点或右节点，再进行删除。

> 一个例子如下图：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_4.png" width="70%" style="margin: 0 auto;">
> </div>

复杂的情况是处理具有两个子节点的目标节点。一般的删除策略是，用其右子树中值最小的节点的值替代自己的值，再删除右子树中值最小的节点。由于右子树中值最小的节点一定没有左子树，所以这一删除是容易的。

> 一个例子如下图：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_5.png" width="70%" style="margin: 0 auto;">
> </div>

在编写代码时，我们同样将 `Delete` 的返回值设定为删除操作结束后指向新树根的指针，这一做法也有利于我们递归地实现 `Delete` 操作。例程如下：

```c
SearchTree Delete(ElementType X, SearchTree T) {
    Position tmp;
    if (T == NULL) {
        Error("Element not found");
    }
    else if (X < T->Element) {
        T->Left = Delete(X, T->Left);
    }
    else if (X > T->Element) {
        T->Right = Delete(X, T->Right);
    }
    else if (T->Left == NULL || T->Right == NULL) { // Zero or one children
        tmp = T;
        if (T->Left == NULL) {
            T = T->Right;
        }
        else if (T->Right == NULL) {
            T = T->Left;
        }
        free(tmp);
    }
    else { // Two children
        tmp = FindMin(T->Right);
        T->Element = tmp->Element;
        T->Right = Delete(T->Element, T->Right);
    }
    return T;
}
```

尽管这样实现 `Delete` 操作的效率已经较高了，但我们需要建立这样的思想：最高效的操作就是不操作！因此，若删除的次数不多，则一个常用的策略是**懒惰删除** (lazy deletion)，即当一个元素要被删除时我们并不真的从树上删除它，而是给该节点添加一个被删除的记号。在处理有重复关键字的时，这一策略就更加符合直觉了，因为我们只需将该节点的出现次数减 $1$ 即可。

### 平均情形复杂度分析

一个重要的结论是：对于有 $N$ 个节点的二叉查找树，假设该树所有可能的形态出现的机会相等，则树的所有节点的平均深度为 $O(\log N)$。

直观上，除 `MakeEmpty` 外，其余操作都只花费 $O(d)$ 的时间，$d$ 是目标节点在树中的深度。理想情况下，我们希望访问任意节点，其深度都能达到二叉查找树的平均深度 $\log N$。

但事实上，如果我们对二叉搜索树的形态不人为地加以修正，往往在进行若干 `Insert` 和 `Delete` 操作后，这颗二叉查找树的形态会变得「不平衡」（最坏情况是退化成一条链）。这会导致二叉查找树的平均深度远大于 $\log N$，从而使得各项操作的时间复杂度增加。

> 例如，在进行 $\Theta (N^{2})$ 次 `Insert` 或 `Delete` 操作后，一棵二叉查找树的形态可能会如下图所示：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_3_6.png" width="70%" style="margin: 0 auto;">
> </div>

因此，为了保证二叉查找树这一数据结构的高效性，我们需要人为地干预其形态的变化，使得其维持较小的（接近理想条件的）深度。这一般有两种方法：

- 设定一个**平衡** (balance) 条件，即任何节点的深度不得过深。
- 允许树有任意深度，但是在每次操作后按一定方法对树的结构进行调整。这类数据结构称作**自调整** (self-adjusting) 类结构。

对二叉查找树的改进便是基于这两个思路。但是囿于课程限制，我们将不会在这里继续深入对二叉查找树的研究，这些内容留待以后的课程中再叙。
