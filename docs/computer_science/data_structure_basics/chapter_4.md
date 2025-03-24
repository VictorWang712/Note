---
comments: true
---

# 第四章 - 优先队列（堆）

## 模型

**优先队列** (priority queue)，又称**堆** (heap) 是允许至少下列两种操作的数据结构：

- `Insert`：插入新元素
- `DeleteMin`：找出、返回并删除优先队列中的最小元素

可以想见，只需要改变数据的大小判断方式，我们就可以对应地实现 `DeleteMax` 操作。因此我们只需要介绍一种操作的实现方式，下文将以 `DeleteMin` 操作为例。

## 二叉堆

**二叉堆** (binary heap) 是最常见的优先队列的实现方式，因此习惯上，不加修饰地提到「堆」时往往都指二叉堆。

### 结构性质

二叉堆是一棵**完全二叉树** (complete binary tree)，即除底层外全部填满，底层上的节点从左到右填入的二叉树。

容易证明，一棵高为 $h$ 的完全二叉树有 $2^{h}$ 到 $2^{h + 1} - 1$ 个节点，这意味着 $h = \lfloor \log N \rfloor$，故该树上的所有操作都是 $O(\log N)$。特别地，当节点数为 $2^{h + 1} - 1$ 时，我们称该完全二叉树为**理想二叉树** (perfectly binary tree)。

由于完全二叉树的结构具有很强的规律性，我们可以给出这样一种编号方式：即从最高层到最底层，从左到右依次编号。不难发现这种编号方式是可以唯一确定一棵完全二叉树，因此我们可以用一个数组来实现完全二叉树。具体地，对于数组中任意位置 $i$ 上的元素，其左子节点在位置 $2i$ 上，右子节点在位置 $2i + 1$ 上，父节点在位置 $\lfloor \frac{i}{2} \rfloor$ 上。

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_4_1.png" width="70%" style="margin: 0 auto;">
</div>

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_4_2.png" width="70%" style="margin: 0 auto;">
</div>

这种实现方式简便且高效，唯一的问题在于堆的大小需要实现估计。另外，我们一般不使用数组中下标为 $0$ 的位置存放数据，也就是说根节点应当位于下标为 $1$ 的位置。这么做的原因将在后文提到。

基于此，我们给出优先队列的声明：

```c
struct HeapStruct;
typedef struct HeapStruct *PriorityQueue;

struct HeapStruct {
    int Capacity, Size;
    ElementType *Elements;
}
```

同时给出优先队列初始化的例程：

```c
PriorityQueue Initiallise(int MaxElements) {
    PriorityQueue H;
    H = malloc(sizeof(struct HeapStruct));
    H->Elements = malloc((MaxElements + 1) * sizeof(ElementType));
    H->Capacity = MaxElements;
    H->Size = 0;
    H->Elements[0] = MinData;
    return H;
}
```

### 堆序性质

优先队列能够快速进行插入和查找最小值所依赖的性质是**堆序** (heap order) 性，即树上任意节点都应该小于其后裔。

根据这一性质，最小值总是位于根结点处，于是我们可以用常数时间完成附加操作 `FindMin`。

### 基本堆操作

堆操作中需要始终保持堆序性，这是堆操作高效进行的基础。

#### Insert

为将一个元素 $X$ 插入到堆中，我们在完全二叉树的下一个空闲位置创建一个空穴（这样做可以保证二叉树仍然是完全二叉树）。

如果 $X$ 可以放在该空穴位置而不破坏堆序性，则插入即可。否则我们将空穴的父节点上的元素移到空穴位置，空穴则移到原本的父节点位置，并再次判断 $X$ 能否插入在空穴中。

这种策略称作**上滤** (percolate up)。我们给出例程：

```c
void Insert(ElementType X, PriorityQueue H) {
    H->Size++;
    int o = H->Size;
    while (H->Elements[o / 2] > X) {
        H->Elements[o] = H->Elements[o / 2];
        o /= 2;
    }
    H->Elements[o] = X;
}
```

特别地，如果要插入的元素是新的最小值，那么空穴将一直上移到根节点。一种终止方式是做特判跳出循环；但更优越的做法是在位置 $0$ 处存放一个极小值，即小于等于所有可能插入的数据的值，这个值我们常称为**标记** (sentinel)。这种处理方法是数据结构中常见的策略，即添加**哑信息** (dummy piece of information) 以简化程序，提高算法运行效率。

#### DeleteMin

得益于堆序性，找出最小元素是容易的，主要问题在于如何删除它。我们可以用类似于插入的方式处理。

当删除最小元素时，在根结点处产生了一个空穴。为保证树仍然是一棵完全二叉树，我们希望堆中的最后一个元素 $X$ 能移动到某个地方。如果 $X$ 可以放在该空穴位置而不破坏堆序性，则插入即可。否则我们将空穴的左右子节点中较小的一个移到空穴位置，空穴则移到原本较小的子节点位置，并再次判断 $X$ 能否插入在空穴中。

这种策略称作**下滤** (percolate down)。

在代码实现中需要特别注意的是，完全二叉树上可能有一个节点只有一个子结点。因此我们在考察子节点前总是应该判断右子节点是否存在。我们给出例程：

```c
ElementType DeleteMin (PriorityQueue H) {
    int o = 1, child;
    ElementType MinElement = H->Elements[1], LastElement = H->Elements[H->Size];
    H->Size--;
    while (o * 2 <= H->Size) {
        child = o * 2;
        if (child != H->Size && H->Elements[child] > H->Elements[child + 1]) {
            child++;
        }
        if (LastElement > H->Elements[child]) {
            H->Elements[o] = H->Elements[child];
            o = child;
        }
        else {
            break;
        }
    }
    H->elements[o] = LastElement;
    return MinElement;
}
```

### 其它堆操作

一般地，在仅有堆序性保证下，在堆中可以高效进行的操作即为插入和删除最小值。为使堆能支持其它高效操作，一个关键的额外信息是堆中每个元素的位置。

假设我们通过某种额外的方法知道了每一个元素的位置，那么就可以高效地进行以下几种操作。

#### DecreaseKey

$\texttt{DecreaseKey}(P, \Delta, H)$ 操作减小在位置 $P$ 处的关键字的值，减小的值为正的量 $\Delta$。由于单独的减小操作可能会破坏堆序性，因此必须通过上滤对堆进行调整。

#### IncreaseKey

$\texttt{IncreaseKey}(P, \Delta, H)$ 操作增大在位置 $P$ 处的关键字的值，增大的值为正的量 $\Delta$。由于单独的增大操作可能会破坏堆序性，因此必须通过下滤对堆进行调整。

#### Delete

$\texttt{Delete}(P, H)$ 操作删除堆中位置 $P$ 上的节点。这一操作只需要先执行 $\texttt{DecreaseKey}(P, \infty, H)$，再执行 $\texttt{DeleteMin}(H)$ 来完成。

#### BuildHeap

$\texttt{BuildHeap}(H)$ 操作将 $N$ 个关键字插入到空堆中。一个简单的实现方式是进行 $N$ 次 `Insert` 操作，但这样做的时间复杂度是 $O(N \log N)$ 的。

一个更好的实现方式是将 $N$ 个关键字先以任意顺序放入完全二叉树中，再从树的倒数第二层开始，对每一层的每一个节点执行下滤操作。其核心代码如下：

```c
for (int i = N / 2; i > 0; i--) {
    PercolateDown(i);
}
```

可以证明，这样的方式保证了 `BuildHeap` 操作结束后完全二叉树满足堆序性，同时这一操作的时间复杂度是 $O(N)$ 的。

## d-堆

d-堆是二叉堆的简单推广，即保证树上没和节点有 $d$ 个子节点的堆。二叉堆即为 2-堆。

随着 $d$ 的增大，`Insert` 操作的时间复杂度将减小，因为树的层数变少了；但是 `DeleteMin` 操作的时间复杂度将增大，因为找出最小子节点所需的比较次数增多了。因此选用 $d$ 为多少的 d-堆，需要从实际问题中 `Insert` 操作和 `DeleteMin` 操作的次数出发综合考量。

???+ note

    有分析认为，4-堆的效率高于二叉堆。
    
    在实际编写程序时，除了考虑算法效率外，还应当考虑代码实现的简易程度和易维护性。因此二叉堆仍然是使用最广泛的堆结构。
