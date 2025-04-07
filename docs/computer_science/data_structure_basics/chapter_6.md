---
comments: true
---

# 第六章 - 图论算法

## 概念

### 图的定义

一个**图** (graph) $G = (V, E)$ 由**顶点** (vertex) 集 $V$ 和**边** (edge) 集 $E$ 组成。每一条边是一个点对 $(u, v)$，有时边也称作**弧** (arc)。如果点对是有序的，那么图就是**有向** (directed) 的，图称作**有向图** (diagraph)。有向图上去掉每条边的方向性而得到的无向图称作该有向图的**基础图** (underlying graph)。顶点 $v$ 和 $w$ **邻接** (adjacent) 当且仅当 $(v, w) \in E$。有时边具有**权** (weight) 或**值** (cost)。

图中的一条**路径** (path) 是一个顶点序列 $w_{1}, w_{2}, \cdots, w_{N}$ 满足 $(w_{i}, w_{i + 1}) \in E, 1 \leq i < N$。这样一条路径的**长** (length) 即为路径上各边的边权之和。一条**简单路径** (simple path) 即为一条路径上各顶点互异，但第一个顶点和最后一个顶点可能相同的路径。

???+ note

    如果图含有一条从一个顶点到它自身的边 $(v, v)$，那么路径 $v, v$ 称作一个**环** (loop)。后文我们要讨论的图都是无环的。

有向图中的**圈** (cycle) 是满足 $w_{1} = w_{N}$ 且长至少为 $1$ 的一条路径。如果该路径是简单路径，那么这个圈就是简单圈。如果一个有向图没有圈，则称这个图是**无圈的** (acyclic)，这个图称作**有向无圈图** (directed acyclic graph, DAG)。

如果在一个无向图中从每一个顶点到每个其它顶点都存在一条路径，则称该无向图是**连通的** (connected)。具有这样性质的有向图称作**强连通的** (strongly connected)。如果一个有向图不是强连通的，但其基础图是连通的，则称该有向图是**弱联通的** (weakly connected)。**完全图** (complete graph) 是每一对顶点间都存在一条边的图。

???+ note

    从以上定义不难发现，树即为一个连通无圈图。

### 图的表示

常用的表示图的方法有两种：邻接矩阵和邻接表。

#### 邻接矩阵

**邻接矩阵** (adjacent matrix) 表示法即使用一个二维数组来表示图。其中 `A[u][v]` 置为边 `(u, v)` 的权。在具体问题中，我们常用一个非法的极小值（如 $0$）或极大值（如 $\infty$）表示不存在的边。

邻接矩阵的实现和调用都非常简单，潜在的问题在于其空间需求太大，为 $\Theta(|V|^{2})$。如果图是**稠密** (dense) 的，即 $|E| = \Theta(|V|^{2})$，那么邻接矩阵是合适的表示方法。但如果图是**稀疏** (sparse) 的，即边的数量远小于 $|V|^{2}$，那么使用邻接矩阵的空间需求就不大可接受了。

#### 邻接表

对于稀疏图，更好的表示方法是使用**邻接表** (adjacency)。其结构示例如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_6_1.png" width="70%" style="margin: 0 auto;">
</div>

由图可见，对每一个顶点，我们使用一个表存放所有与该顶点邻接的顶点。同时我们再用一个**头单元** (header cell) 数组，即图中最左边的结构作为各顶点的索引。此时的空间需求为 $O(|E| + |V|)$。

## 拓扑排序

**拓扑排序** (topological sorting) 是对有向无圈图各顶点的一种排序得到一个拓扑序列，其保证对于任何有向边 $(u, v)$，在排序得到的序列中都有 $u$ 在 $v$ 的前面。

为了解决这个问题，我们先再作出以下定义：称一个顶点 $v$ 的**入度** (indegree) 为以 $v$ 为终点的边 $(u, v)$ 的条数，其**出度** (outdegree) 为以 $v$ 为起点的边 $(v, u)$ 的条数。两者之和称作顶点 $v$ 的**度** (degree)。

构造拓扑序列的算法是简单的，只需要重复以下两步：

1. 从图中选择一个入度为 0 的点。
2. 输出该顶点，从图中删除此顶点及其所有的出边。

其伪代码如下：

```c
void Topsort(Graph G) {
    int Counter;
    Vertex V, W;
    for (Counter = 0; Counter < NumVertex; Counter++) {
        V = FindNewVertexOfIndegreeZero();
        if (V == NotAVertex) {
            Error("Graph has a cycle");
            break;
        }
        TopNum[V] = Counter;
        for each W adjacent to V {
            Indegree[W]--;
        }
    }
}
```

不难得到，这个算法的复杂度为 $O(|V|^{2})$。

接下来我们着手改进这个算法。可以发现其最大的时间复杂度开销源自于寻找入度为 0 的点，每次寻找都要花费 $O(|V|)$ 的时间，而这样的寻找有 $|V|$ 次。但事实上，如果我们能对入度为 0 的点用一个集合进行记录，并在删除边时对这个集合进行更新，我们就能避免 $O(|V|)$ 的寻找而达到相同的效果。

在具体的实现中，这个集合可以用栈或队列实现。我们给出用队列实现的伪代码：

```c
void Topsort(Graph G) {
    Queue Q;
    int Counter = 0;
    Vertex V, W;
    Q = CreateQueue(NumVertex); MakeEmpty(Q);
    for each vertex V {
        if (Indegree[V] == 0) {
            Enqueue(V, Q);
        }
    }
    while (!IsEmpty(Q)) {
        V = Dequeue(Q);
        TopNum[V] = ++Counter;
        for each W adjacent to V {
            if (--Indegree[W] == 0) {
                Enqueue(W, Q);
            }
        }
    }
    if (Counter != NumVertex) {
        Error("Graph has a cycle");
    }
    DisposeQueue(Q);
}
```

当使用邻接表表示图时，这个算法的时间复杂度即为 $O(|E| + |V|)$。

从以上讨论中我们可以发现，拓扑排序的结果是不唯一的。如果我们希望得到字典序最小（或最大）的拓扑序列，我们只需将上述算法中存放入度为 0 的顶点的数据结构由队列换为最小堆（或最大堆）即可。
