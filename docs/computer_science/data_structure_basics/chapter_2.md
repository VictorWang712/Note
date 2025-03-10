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

对于二维形式组织的数据，我们按照两个维度分别构造若干链表，使每个数据位于分属于两个维度的两个链表之中。这样就产生了一个类似于「十字交通网络」的结构，而我们可以相对便捷的在这个「交通网络」的任意「十字路口」，向任意我们需要的方向「行走」。

## 栈

**栈** (stack) 是限制只能在一个位置插入和删除的表，这个位置是表的末端，称作栈的**顶** (top)。对栈的基本操作有 `Push` 和 `Pop`，即在栈顶插入或删除元素。同时我们还需要 `Top` 操作，以在进行 `Pop` 前进行检查。

???+ note

    对空栈进行 `Pop` 或 `Top` 被认为是栈这一数据结构的错误；但 `Push` 时空间用尽是一个实现错误，而非数据结构错误。

栈具有 LIFO (Last In First Out) 的性质。

一个影响栈的执行效率的情况是遍历元素，这意味着需要将栈中的元素全部 `Pop` 后再反序地 `Push` 进入。这是栈的特性所决定的缺陷。

### 栈的实现

由于栈是一个表，因此任何实现表的方法都能实现栈。常用的两种方法即为使用指针和使用数组实现。

#### 栈的链表实现

栈的第一种实现方法是使用单链表，通过在表前端插入实现 `Push`，通过删除表前端元素实现 `Pop`。`Top` 只需检查表前端元素并返回其值。

不难发现，所有操作均花费常数时间。但在实际的代码编写中存在一个问题：对 `malloc` 和 `free` 的调用所消耗的时间是较大的。

一种用来避免这一问题的方法是使用备用栈。即在主栈中 `Pop` 元素时，不将其所占用的内存之间释放，而是移入备用栈中。当主栈需要 `Push` 元素时，便从备用栈中调用值已被废弃的空间。

#### 栈的数组实现

因为能避免使用指针，栈的数组实现往往是更常用的。这种实现方式的唯一问题是我们需要提前声明一个数组的大小，存在潜在的空间浪费。

更换实现方式并不会影响操作的时间复杂度，故所有操作仍然花费常数时间。

### 栈的应用

得益于栈的特性，栈的基本操作只需要花费常数时间。故栈在解决某些问题上有很合适的应用。

#### 平衡符号

平衡符号问题指的是检验一个字符串中每个符号是否成对出现。常见的成对符号是各种括号。

> 举例来说，`[()]` 是合法的，`[(])` 是非法的。

利用栈可以提出这样一个算法：

$$
\begin{array}{ll}
1 &  \textbf{Input. } \text{The string } s . \\
2 &  \textbf{Output. } \text{Whether } s \text{ is valid.} \\
3 &  \textbf{Method. } \\
4 &  \text{make an empty stack} \\
5 &  \textbf{for} \text{ each } s_{i} \text{ in the string } s \\
6 &  \qquad \textbf{if } s_{i} \text{ is an open symbol} \\
7 &  \qquad\qquad \text{push } s_{i} \text{ into the stack } \\
8 &  \qquad \textbf{else if } s_{i} \text{ is a close symbol} \\
9 &  \qquad\qquad \textbf{if } \text{stack is empty } \\
10 &  \qquad\qquad\qquad \textbf{return } \text{invalid} \\
11 &  \qquad\qquad \textbf{else} \\
12 &  \qquad\qquad\qquad \text{pop } s_{j} \text{ from the stack } \\
13 &  \qquad\qquad\qquad \textbf{if } s_{j} \text{ is not the corresponding open symbol} \\
14 &  \qquad\qquad\qquad\qquad \textbf{return } \text{invalid} \\
15 &  \textbf{if } \text{the stack is not empty} \\
16 &  \qquad \textbf{return } \text{invalid} \\
17 &  \textbf{return } \text{valid}
\end{array}
$$

这个算法的正确性是不难验证的。进一步地，因为这是一个**在线** (on-line) 算法，所以其运行速度也很快，只需要 $O(N)$ 的时间复杂度。

#### 后缀表达式

**后缀表达式** (postfix notation)，也称**逆波兰表达式** (reverse Polish notation) 是一种数学表达式的记法，其中运算符位于操作数之后。其准确定义源于[在表达式树上的后序遍历](https://victorwang712.github.io/Note/computer_science/data_structure_basics/chapter_3/#_9)，这一点我们会在第三章讨论。

> 对应地，在表达式树上进行先序遍历得到的表达式被称作**前缀表达式** (prefix notation) 或**波兰表达式** (Polish notation)。

计算一个后缀表达式所花费的时间是 $O(N)$ 的，这一过程且后缀表达式的求值可以用栈简单实现。

$$
\begin{array}{ll}
1 &  \textbf{Input. } \text{The expression } s \text{ under infix notation.} \\
2 &  \textbf{Output. } \text{The value of the expression} \\
3 &  \textbf{Method. } \\
4 &  \text{make an empty stack} \\
5 &  \textbf{for} \text{ each } s_{i} \text{ in the expression } s \\
5 &  \qquad \textbf{if } s_{i} \text{ is a symbol} \\
6 &  \qquad\qquad \textbf{let } a_{i} \text{ be the top of the stack} \\
7 &  \qquad\qquad \text{pop } a_{i} \text{ from the stack} \\
8 &  \qquad\qquad \textbf{let } a_{j} \text{ be the top of the stack} \\
9 &  \qquad\qquad \text{pop } a_{j} \text{ from the stack} \\
10 &  \qquad \text{let } a_{k} \text{ be the result of the operation with } a_{i}, a_{j} \text{ and the symbol } s_{i} \\
11 &  \qquad \text{push } a_{k} \text{ into the stack}\\
12 &  \qquad \textbf{else} \\
13 &  \qquad\qquad \text{push } s_{i} \text{ into the stack} \\
14 &  \textbf{output } \text{the top of the stack } s_{i} \\
\end{array}
$$

值得注意的是，以后缀表达式形式给出的表达式的运算顺序是唯一确定的，也就意味着不需要给出运算符的优先级。得益于以上优势，后缀表达式在计算机领域有广泛的应用。

#### 中缀到后缀的转换

我们常见的标准形式的表达式被称作**中缀表达式** (infix notation)，因此一个常见的问题就是如何将中缀表达式转换为后缀表达式。

假设我们的中缀表达式只含有 $+, -, \times, /, ()$ 五种符号和由一个字母所表示的变量，且符号优先级与通用的数学运算相一致，我们同样可以用栈来完成这一转换过程。

$$
\begin{array}{ll}
1 &  \textbf{Input. } \text{The expression } s \text{ under infix notation.} \\
2 &  \textbf{Output. } \text{The expression } s \text{ under postfix notation.} \\
3 &  \textbf{Method. } \\
4 &  \text{make an empty stack} \\
5 &  \textbf{for} \text{ each } s_{i} \text{ in the expression } s \\
5 &  \qquad \textbf{if } s_{i} \text{ is a letter} \\
6 &  \qquad\qquad \textbf{output } s_{i} \\
7 &  \qquad \textbf{else if } s_{i} \text{ is } ) \\
8 &  \qquad\qquad \textbf{while } \text{the top of the stack } s_{j} \text{ is not } ( \\
9 & \qquad\qquad\qquad \textbf{output } s_{j} \\
10 & \qquad\qquad\qquad \text{pop } s_{j} \text{ from the stack} \\
11 & \qquad\qquad \text{pop the top of the stack } s_{j} \text{ from the stack} \\
12 &  \qquad \textbf{else} \\
13 &  \qquad\qquad \textbf{while } \text{the priority of top of the stack } s_{j} \text{ is not lower than } s_{i} \\
14 & \qquad\qquad\qquad \textbf{output } s_{j} \\
15 & \qquad\qquad\qquad \text{pop } s_{j} \text{ from the stack} \\
16 & \qquad\qquad \text{push } s_{i} \text{ into the stack} \\
17 &  \textbf{while } \text{the stack is not empty} \\
18 &  \qquad \textbf{output } \text{the top of the stack } s_{i} \\
19 &  \qquad \text{pop } s_{i} \text{ from the stack} \\
\end{array}
$$

#### 函数调用

在一个复杂的程序中，函数的调用往往互相嵌套，但不难发现这一过程和前述的平衡符号问题是一致的。因此我们也可以使用栈来解决这一问题。

一般地，在实现递归的程序设计语言中，所存储的信息称作**活动记录** (activation record)，或称作**栈帧** (stack frame)。函数的调用即是以入栈和出栈的方式有序执行的。

在实际情况中，计算机的内存是有限的，这便导致了一个常见的问题，即栈溢出。栈溢出往往发生在函数调用不当的情况下，尤其是在递归不当的情况下。

一个使用递归极端不当的情况称作**尾递归** (tail recursion)，即在程序的末尾进行递归调用。由于尾递归可以简单地通过带参数的顺序实现所替代，而两者对空间的消耗是天差地别的，所以在编写程序时要力图避免出现尾递归的情况。

事实上，所有的递归总是能转变成非递归的实现，这也正是编译器在将代码编译为汇编语言时所做的事情。但出于程序逻辑性和易读性的考量，我们仍然在编写程序时使用递归。

## 队列

**队列** (queue) 也是一种表。其基本操作有 `Enqueue` 和 `Dequeue`，即在**队尾** (rear) 插入一个元素和在**队头** (front) 删除一个元素

队列具有 FIFO (First In First Out) 的性质。

### 队列的实现

由于队列是一个表，因此任何实现表的方法都能实现队列。常用的两种方法即为使用指针和使用数组实现，且无论用哪种实现方式，队列的每个基本操作均只需要 $O(1)$ 的运行时间。

#### 队列的数组实现

对于一个队列数据结构，我们声明一个数组 `Queue[]` 和变量 `Front`、`Rear`，表示队列的两端。为了操作的方便，还需要声明变量 `Size` 用于记录队列中的元素个数。

操作的实现非常清晰。若使元素 $X$ 入队，只需让 `Size` 和 `Rear` 增 $1$，然后令 `Queue[Rear]` $= X$；若使元素队首元素出队，只需返回 `Queue[Front]`，并让 `Size` 减 $1$，`Front` 增 $1$。

数组实现下一个潜在的问题仍然是空间的浪费。考虑到队列的特殊性质，我们常使用**循环数组** (circular array) 这种方式进行优化，即只要 `Front` 或 `Rear` 到达数组尾端就使其绕回开头。

队列的循环实现下有两个需要注意的问题。

- 第一，检测队列是否为空是很重要的，这确保了 `Dequeue` 操作的合法性。
- 第二，某些时候队列的大小不由单独的 `Size` 给出，而是通过判断 `Front` 和 `Rear` 是否满足 `Rear` $=$ `Front` $- 1$ 来进行判定（因此创建一个空队列时应当赋值 `Front` $= 0$，`Rear` $= -1$）。

### 队列的应用

鉴于现实中很多问题存在队列的结构，队列本身就有很多应用。在实际情况中，队列的操作往往带有一定的随机性（比如每个元素入队和出队的时间），因此在数学上常用概率的方法处理队列问题，这产生了名为**排队论** (queueing theory) 的完整数学分支，在此不过多赘述。

在计算机科学中，队列是一种非常基本的数据结构，在很多高级算法（如图论中的部分算法）中都有所应用。因此队列是一种非常重要的数据结构。
