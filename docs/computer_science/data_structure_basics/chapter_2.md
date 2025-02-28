---
comments: true
---

# 第二章 - 表、栈和队列

## 抽象数据类型

**抽象数据类型** (abstract data type, ADT) 是一些操作的集合。

## 表

**表** (list) 是形如 $A_{1}, A_{2}, \cdots, A_{N}$ 的抽象数据类型，这个表的大小是 $N$。我们称大小为 $0$ 的表为**空表** (empty list)。

一般来说，表应当支持如下操作：

- `PrintList`：输出表元素
- `MakeEmpty`：创建空表
- `FindKth`：访问第 $k$ 位元素
- `Find`：查找某元素的位置
- `Insert`：在第 $k$ 位元素后插入新元素
- `Delete`：删除元素
- `Next`：访问当前元素的后继
- `Previous`：访问当前元素的前驱

### 表的简单数组实现

对表的所有操作都可以使用数组实现。但由于数组的申请是一次性的，所以需要对表的大小最大值进行估计。这往往会导致在处理一些位置大小的表时，会产生一定的空间浪费。

对于数组实现的表，`PrintList` 和 `Find` 都以线性时间执行，`FindKth` 只需要花费常数时间。但是 `Insert` 和 `Delete` 的效率较低，最坏情况均为 $O(N)$。

### 链表

在数组实现中，插入和删除较低的效率主要源于需要将表中的元素进行整体移动。基于改进这一缺点的想法，我们提出将表不连续存储，即使用**链表** (linked list) 实现。

链表由一系列不必在内存中相连的结构组成。每一个结构均含有表元素和指向包含该元素后继结构的指针，称其为 `Next` 指针。最后一个结构的 `Next` 指针指向 `NULL`。

不难得到，链表实现下的 `Insert` 和 `Delete` 操作是常数时间的。但是相对的 `FindKth` 的时间就变成了线性的。

在编写程序时，我们还会采用一些技巧使某些功能的实现相对统一优雅。

#### 表头

一个常用的方法是在新建链表时创建一个**表头** (header)，也称作**哑节点** (dummy node)。

不难发现，这一处理有如下优势：

- 给出了从表的起始端插入元素的显性方法
- 使从表的起始端删除元素和在其它位置删除元素的操作相统一，避免了对特殊情况的分类讨论

#### 双向循环链表

在某些算法中我们有倒序访问链表的需求，这在标准实现的链表中是较难完成的。对此，我们只需要为每一个结构添加一个指向包含该元素前驱结构的指针，即可简单地实现这一功能。这种链表被称作**双向链表** (doubly linked list)。

进一步地，一个常见的做法是：将链表的最后一个结构的后继设定为链表的第一个结构。这种处理下将不需要表头，这种链表被称作**循环链表** (linked circular list)。

将以上两种改进相结合，即可得到**双向循环链表** (doubly linked circular list)。注意需要将链表的第一个结构的前驱设定为链表的最后一个结构。

#### 多重表

对于以二维形式组织的数据，用传统的数组储存会造成很大的空间开销，尤其是当数据本身较为稀疏的时候。借鉴链表的思想，我们提出**多重表** (Multilist) 这一数据结构。

对于二维形式组织的数据，我们按照两个维度分别构造若干链表，使每个数据位于分属于两个维度的两个链表之中。这样就产生了一个类似于“十字交通网络”的结构，而我们可以相对便捷的在这个“交通网络”的任意“十字路口”，向任意我们需要的方向“行走”。
