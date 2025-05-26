---
comments: true
---

# 第八章 - 散列

## 一般想法

**散列** (hashing) 时一种以常数平均时间执行插入、删除和查找的技术，通过散列可以实现**散列表** (hash table) ADT。但是散列无法实现任何需要元素间排序信息的操作。

理想的散列表是一个含有关键字的具有固定大小的数组。典型情况下，一个关键字就是一个带有相关值的字符串。我们通常将表的大小记作 $\texttt{TableSize}$，并将每个关键字映射到在 $0$ 到 $\texttt{TableSize} - 1$ 这个范围中的某个数。这个映射就称作**散列函数** (hash function)，理想情况下它应该运算简单，并保证任何两个不同的关键字映射到不同单元。但事实上这个不可能的，因为表的大小有限，而关键字的数目无限，于是就会出现**冲突** (collision)，即两个关键字散列到同一个值时。

## 散列函数

### 整数关键字

如果输入的关键字是正数，则一个通常使用的方法就是将其映射到 $\texttt{Key} \mod \texttt{TableSize}$。然而容易意识到，当表的大小为合数时，冲突发生的概率是较高的，因此好的方法是保证表的大小为素数。这样当输入的关键字为随机整数时，散列函数的计算简单且关键字分配较均匀。

### 字符串关键字

散列表更常用的场景是用于处理字符串作为关键字，这里我们所讨论的字符串指的是由若干小写英文字母所组成的字符串。

一种简单的散列函数是将字符串中字符的 ASCII 码相加，但是这个方法的局限性是显然的。一方面，对于由同样字符组成但是顺序的不同的字符串，必然会出现冲突；另一方面，由于字符串的长度有限，而且每一个字符的值最多是 127（由 ASCII 码所决定），因此这样会导致散列表的分布不均匀。

在此基础上有一种改进，即只考察字符串的前三位，并按照 27 进制赋权，即计算 `Key[0] + 27 * Key[1] + 729 * Key[2]`。虽然这个方法容易计算，但当散列表足够大时，其利用率仍然是不理想的。

再给出一个新的方案，利用 Horner 法则计算字符串，即计算 $\sum_{i = 0}^{\texttt{KeySize} - 1} \texttt{Key}[\texttt{KeySize} - i - 1] \cdot 32^{i}$。容易意识到，如果对结果不加以处理，计算出来的值可能会特别大。因此通常我们将结果对一个较大的，但是可以被计算机接受的大质数取模。另一个需要说明的是，此处之所以采用 32 进制而非 27 进制，是因为乘以 32 等价于左移 5 位，这便于在硬件层面进行加速。

### 总结

到这里，我们已经给出了常见的散列函数的实现。后文中我们将讨论若干种方法，以解决散列中的冲突问题。

## 分离链接法

解决冲突的第一种方法称作**分离链接法** (separate chaining)，其做法是将散列到同一个值的所有元素保留在一个表中。

> 举一个例子，当散列函数 $\texttt{Hash}(X) = X \mod 10$ 时，对前 10 个完全平方数的散列并应用分离链接法得到的散列表如下：
>
> <div style="text-align: center; margin-top: 0px;">
> <img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/data_structure_basics/chapter_8_1.png" width="70%" style="margin: 0 auto;">
> </div>

接下来，我们将给出分离链接散列表的相关例程。首先是其类型声明：

```c
#ifndef __HashSep_H

struct ListNode;
typedef struct ListNode *Position;
struct HashTbl;
typedef struct HashTbl *HashTable;

HashTable InitializeTable( int TableSize );
void DestroyTable( HashTable H );
Position Find( ElementType Key, HashTable H );
void Insert( ElementType Key, HashTable H );
ElementType Retrieve( Position P );

#endif // __HashSep_H

struct ListNode {
    ElementType Element;
    Position Next;
};

typedef Position List;

struct HashTbl {
    int TableSize;
    List *TheLists;
};
```

初始化函数：

```c
HashTable InitializeTable(int TableSize) {
    HashTable H;
    int i;

    if (TableSize < MinTableSize)
    {
        Error("Table size too small");
        return NULL;
    }

    /* Allocate table */
    H = malloc(sizeof(struct HashTbl));
    if (H == NULL) {
        FatalError("Out of space");
    }

    H->TableSize = NextPrime(TableSize);

    /* Allocate array of lists */
    H->TheLists = malloc(sizeof( List ) * H->TableSize);
    if(H->TheLists == NULL) {
        FatalError("Out of space");
    }

    /* Allocate list headers */
    for(i = 0; i < H->TableSize; i++)
    {
        H->TheLists[i] = malloc(sizeof(struct ListNode));
        if(H->TheLists[ i ] == NULL) {
            FatalError("Out of space");
        }
            
        else {
            H->TheLists[i]->Next = NULL;
        }
    }
    return H;
}
```

查找函数 $\texttt{Find}$，对 $\texttt{Find}(\texttt{Key}, H)$ 的调用将返回一个指针，指向包含 $\texttt{Key}$ 的单元。

```c
Position Find(ElementType Key, HashTable H) {
    Position P;
    List L;

    L = H->TheLists[Hash(Key, H->TableSize)];
    P = L->Next;
    while(P != NULL && P->Element != Key) {
        /*Probably need strcmp*/
        P = P->Next;
    }
    return P;
}
```

在插入操作中，如果要插入的项已经存在，那么我们就不用再操作；否则我们将目标项放到表的前端。

???+ note

    事实上，新插入的项可以放在表的任何一处。只是将其插入表的前端便于实现，而且新近插入的元素最有可能最先被访问。

```c
void Insert(ElementType Key, HashTable H) {
    Position Pos, NewCell;
    List L;

    Pos = Find(Key, H);
    if(Pos == NULL) { /*Key is not found*/
        NewCell = malloc(sizeof(struct ListNode));
        if(NewCell == NULL) {
            FatalError("Out of space");
        }
        else {
            L = H->TheLists[Hash(Key, H->TableSize)];
            NewCell->Next = L->Next;
            NewCell->Element = Key;  /*Probably need strcpy*/
            L->Next = NewCell;
        }
    }
}
```

我们定义散列表的**装填因子** (load factor) $\lambda$ 为散列表种的元素个数与散列表大小的比值。在上面的例子中，$\lambda = 1.0$。表的平均长度为 $\lambda$，执行一次查找所需要的时间是计算散列函数值所需的常数时间与遍历表所用的时间之和。

事实上，表的大小并不重要，装填因子才是重要的。分离链接散列的目标即为使得表的大小尽量与预料的元素个数相近，即令 $\lambda \approx 1$。使表的大小是素数以保证一个好的分布也是一个好的思路。

## 开放定址法

分离链接法的缺点在于需要指针，由于给新单元分配地址需要时间，就会导致算法速度减慢，同时这种方法还要求实现另一种数据结构，增大了代码的复杂性。

**开放定址法** (open addressing) 是另一种用链表解决冲突的方法。在这种算法中，如果有冲突发生，就尝试选择另外的单元，直到找出空的单元为止。具体来说相继试选 $h_{0}(X), h_{1}(X), \cdots $，其中 $h_{i}(X) = (\texttt{Hash}(X) + F(i)) \mod TableSize$，且 $F(0) = 0。可见，冲突的解决主要依赖于函数 $F$。同时不难理解，开放定址法所需的表比分离链接法要大，对应的装填因子 $\lambda$ 也一般小于 $0.5$。

接下来，我们讨论三种具体的函数 $F$ 的实现。

### 线性探测法

在线性探测法中，$F$ 是 $i$ 的线性函数，典型的方法即为令 $F(i) = i$。

但是，这种方法容易导致表中被占据的单元连续而形成一些区块，这种现象称作**一次聚集** (primary clustering)，这会导致每次试选的时间复杂度增大。

我们直接给出一个结论，使用线性探测法实现的散列表，每次操作的期望次数为：

- 查找成功：$\frac{1}{2} (1 + \frac{1}{1 - \lambda})$
- 插入、查找失败：$\frac{1}{2} (1 + \frac{1}{(1 - \lambda)^{2}})$

### 平方探测法

在平方探测法中，$F$ 是 $i$ 的二次函数，典型的方法即为令 $F(i) = i^{2}$。平方探测法即是用于解决线性探测法的一次聚集问题所被提出的。

有关平方探测法，一个重要的定理是：如果使用平方探测，且表的大小为素数，那么当表至少有一半是空的时候，总能够插入一个新的元素。

我们给出基于平方探测法的开放定址法的散列例程，这包括其类型声明、初始化、查找和插入。

```c
#ifndef __HashQuad_H

typedef unsigned int Index;
typedef Index Position;

struct HashTb1;
typedef struct HashTb1 *HashTable;

HashTable InitializeTable(int TableSize);
void DestroyTable(HashTable H);
Position Find(ElementType Key, HashTable H);
void Insert(ElementType Key, HashTable H);
ElementType Retrieve(Position P, HashTable H);
HashTable Rehash(HashTable H);

#endif // __HashQuad_H

enum KindOfEntry {Legitimate, Empty, Deleted};

struct HashEntry {
    ElementType Element;
    enum KindOfEntry Info;
};

typedef struct HashEntry Cell;

struct HashTbl {
    int TableSize;
    Cell *TheCells;
};

HashTable InitializeTable(int TableSize) {
    HashTable H;
    int i;

    if (TableSize < MinTableSize) {
        Error("Table size too small");
        return NULL;
    }

    /* Allocate table */
    H = malloc(sizeof(struct HashTbl));
    if (H == NULL) {
        FatalError("Out of space");
    }

    H->TableSize = NextPrime(TableSize);

    /* Allocate array of Cells */
    H->TheCells = malloc(sizeof(Cell) * H->TableSize);
    if (H->TheCells == NULL) {
        FatalError("Out of space");
    }

    for (i = 0; i < H->TableSize; i++) {
        H->TheCells[i].Info = Empty;
    }

    return H;
}

Position Find(ElementType Key, HashTable H) {
    Position CurrentPos;
    int CollisionNum;

    CollisionNum = 0;
    CurrentPos = Hash(Key, H->TableSize);
    while (H->TheCells[CurrentPos].Info != Empty && H->TheCells[CurrentPos].Element != Key) { // Probably need strcmp
        CurrentPos += 2 * ++CollisionNum - 1;
        if (CurrentPos >= H->TableSize) {
            CurrentPos -= H->TableSize;
        }
    }
    return CurrentPos;
}

void Insert(ElementType Key, HashTable H) {
    Position Pos;

    Pos = Find(Key, H);
    if (H->TheCells[Pos].Info != Legitimate) {
        /* OK to insert here */
        H->TheCells[Pos].Info = Legitimate;
        H->TheCells[Pos].Element = Key;
        /* Probably need strcpy */
    }
}
```

虽然平方探测有效解决了一次聚集的问题，但是也会存在类似的**二次聚集** (secondary clustering) 问题。尽管在实际情况中，二次聚集带来的性能问题较小，但是仍然不能忽略。

### 双散列

**双散列** (double hashing) 解决冲突的思路是直观的，即进行两次散列映射。

一个常用的双散列是 $F(i) = i \cdot \texttt{hash}_{2} (X)$，其中 $\texttt{hash}_{2} (X) = R - (X \mod R)$，$R$ 为小于 $\texttt{TableSize}$ 的素数。

在使用双散列时，保证表的大小为素数同样时重要的。

## 再散列

对于使用平方探测的开放定址散列法，如果表的元素填的太满，那么操作的运行时间也会增长，且 `Insert` 操作可能失败。此时，一种解决方法是建立另外一个大约两倍大的表，并使用一个相关的新散列函数扫描整个原始散列表，计算每个元素的新散列值并将其插入到新表中。

这个操作称作**再散列** (rehashing)，显然其时间复杂度为 $O(N)$，相对时间复杂度是较大的。但是其意图也是明显的，即当元素数量过多是的原来的散列有性能退化的风险时，就将表扩大以维护性能。同时考虑到表的大小是倍增的，因此需要扩表的次数是对数级的，这一般是可以接受的。

常用的实现再散列的方法是采用平方探测法，并采用**途中** (middle-of-the-road) 策略来确定再散列的时机，即当表到达某一个装填因子时进行再散列。
