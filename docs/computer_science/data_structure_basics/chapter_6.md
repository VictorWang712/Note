---
comments: true
---

# 第六章 - 图论算法

## 概念

### 图的定义

一个**图** (graph) $G = (V, E)$ 由**顶点** (vertex) 集 $V$ 和**边** (edge) 集 $E$ 组成。每一条边是一个点对 $(u, v)$，有时边也称作**弧** (arc)。如果点对是有序的，那么图就是**有向** (directed) 的，图称作**有向图** (diagraph)。有向图上去掉每条边的方向性而得到的无向图称作该有向图的**基础图** (underlying graph)。顶点 $v$ 和 $w$ **邻接** (adjacent) 当且仅当 $(v, w) \in E$。有时边具有**权** (weight) 或**值** (cost)。

图中的一条**路径** (path) 是一个顶点序列 $w_{1}, w_{2}, \cdots, w_{N}$ 满足 $(w_{i}, w_{i + 1}) \in E, 1 \leq i < N$。一条**简单路径** (simple path) 即为一条路径上各顶点互异，但第一个顶点和最后一个顶点可能相同的路径。

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

1. 从图中选择一个入度为 0 的顶点。
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

## 最短路径算法

对于一个赋权图，即每条边 $(v_{i}, v_{j})$ 具有边权 $c_{i, j}$，则路径 $v_{1} v_{2} \cdots v_{N}$ **赋权路径长** (weighted path length) 即为 $\sum_{i = 1}^{N - 1} c_{i, i + 1}$，**无权路径长** (unweighted path length) 只是路径上的边数，即 $N - 1$。

一般地，我们要解决单源最短路径问题，即给定一个赋权图 $G = (V, E)$ 和一个指定顶点 $s$ 作为输入，找出 $s$ 到 $G$ 中每个其他顶点的最短赋权路径。

在讨论解决这一问题的算法之前，我们需要先关注一些可能的特殊情况。

首先，对于有向图，两个节点之间不一定有路径。其次，如果一个图中存在「负权边」，即边权为负数的边，那么就要关注是否有**负值圈** (negative-cost cycle)，即一个总路径长为负数的循环路径。如果有负值圈存在，那么路径就可以包含循环路径任意多次，故这种情况下没有最短路径。

### 无权最短路径

对于无权图，每条边都是等价的，故我们只需考察起点到达每个终点的最少边数。一个简单的想法是利用**广度优先搜索** (breadth-first search)，即按层处理顶点。

为了做到这一点，我们需要记录一些信息。我们用 $d_{v}$ 记录从 $s$ 出发到达顶点 $v$ 的路径长度。在开始时除 $d_{s} = 0$ 外，其余顶点的 $d_{v}$ 均为 $\infty$。我们用 $p_{v}$ 记录顶点 $v$ 第一次被访问的来源，即是从哪个前驱顶点出发的路径被访问到的。记录 $p_{v}$ 可以得到最短路的路径。最后，我们自然需要一个 `Known` 来记录每个顶点是否被访问到了。当一个顶点已经被访问过了，我们就不会再去寻找到达它的更短路径了。

有了这些信息，算法的伪代码如下：

```c
void Unweighed(Table T) {
    int CurrDist;
    Vertex V, W;
    for (CurrDist = 0; CurrDist < NumVertex; CurrDist++) {
        for each vertex V {
            if (!T[V].Known && T[V].Dist == CurrDist) {
                T[V].Known = True;
                for each W adjacent to V {
                    if (T[W].Dist == Infinity) {
                        T[W].Dist = CurrDist + 1;
                        T[W].Path = V;
                    }
                }
            }
        }
    }
}
```

注意到双层嵌套的 `for` 循环，该算法的时间复杂度为 $O(|V|^{2})$。算法的低效之处在于，就算所有顶点都已经有 `Known` 标记了，最外层的循环仍然要继续。这一点在不修改核心算法的情况下是难以改进的。

分析代码，可以发现如果我们能记录所有 $d_{v} = \texttt{CurrDist}$ 和 $d_{v} = \texttt{CurrDist} + 1$ 的顶点，我们就不必每次遍历全图来寻找适于下一次访问的顶点。于是我们采用队列这一数据结构来完成记录。

在每轮迭代开始时，队列中含有距离为 $\texttt{CurrDist}$ 的顶点。然后我们将这些顶点顺次出队，并将由它们出发访问得到的，距离为 $\texttt{CurrDist} + 1$ 的顶点入队。当所有距离为 $\texttt{CurrDist}$ 的顶点出队后，一轮迭代结束，此时队列里就只含有距离为 $\texttt{CurrDist} + 1$ 的顶点，即为下一轮迭代的初始条件。

容易想到，按照这样的迭代方法，如果一个顶点到最后距离仍然为 $\infty$，则表明其是从开始结点出发不可达的。于是我们便不再需要 `Known` 标记。改进后的伪代码如下：

```c
void Unweighted(Table T) {
    Queue Q;
    Vertex V, W;
    Q = CreateQueue(NumVertex); MakeEmpty(Q);
    Enqueue(S, Q);
    while (!IsEmpty(Q)) {
        V = Dequeue(Q);
        for each W adjacent to V {
            if (T[W].Dist == Infinity) {
                T[W].Dist = T[V].Dist + 1;
                T[W].Path = V;
                Enqueue(W, Q);
            }
        }
    }
    DisposeQueue(Q);
}
```

使用邻接表储存图的话，该算法的时间复杂度即为 $O(|E| + |V|)$。

### Dijkstra 算法

对于赋权图，处理方法就有所不同了。但我们仍然可以沿用处理无权图时记录的信息，$d_{v}, p_{v}$ 和 `Known`。

解决单源最短路径问题的一般方法为 Dijkstra 算法，其是一个**贪心算法** (greedy algorithm)。其核心思想为：对于每轮迭代，在所有未知顶点中选择具有最小 $d_{v}$ 的顶点 $v$，声明 $s$ 到 $v$ 的路径已经为最短路，并更新所有从 $v$ 出发的边的终点节点的路径最小值。

既然我们要动态地更新并调用每个时刻下具有最小 $d_{v}$ 的顶点 $v$，那么容易想到采用优先队列来辅助算法实现，以避免每次 $O(|V|)$ 地寻找这个最小距离顶点。

采用邻接表存储图的话，其声明、初始化和 Dijkstra 算法的伪代码如下：

```c
typedef int Vertex;

struct TableEntry {
    List Header;
    int Known;
    DistType Dist;
    Vertex Path;
};

#define NotAVertex (-1)
typedef struct TableEntry Table[NumVertex];

void InitTable(Vertex Start, Graph G, Table T) {
    ReadGraph(G, T);
    for (int i = 0; i < NumVertex; i++) {
        T[i].Known = False;
        T[i].Dist = Infinity;
        T[i].Path = NotAVertex;
    }
    T[Start].Dist = 0;
}

void Dijkstra(Table T) {
    Vertex V, W;
    while (True) {
        V = smallest unknown distance vertex;
        if (V == NotAVertex) {
            break;
        }
        T[V].Known = True;
        for each W adjacent to V {
            if (!T[W].Known) {
                if (T[V].Dist + Cvw < T[W].Dist) {
                    Decrease(T[W].Dist to T[V].Dist + Cvw);
                    T[W].Path = V;
                }
            }
        }
    }
}
```

如果采用优先队列维护距离最小值，那么每次查找最小值的时间复杂度即为 $O(\log |V|)$，算法的总复杂度即为 $O(|E| \log |V| + |V| \log |V|) = O(|E| \log |V|)$。
