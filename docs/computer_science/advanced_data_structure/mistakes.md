---
comments: true
---

# 错题整理

第一周 选择题 2-5

Consider the following buffer management problem. Initially the buffer size (the number of blocks) is one. Each block can accommodate exactly one item. As soon as a new item arrives, check if there is an available block. If yes, put the item into the block, induced a cost of one. Otherwise, the buffer size is doubled, and then the item is able to put into. Moreover, the old items have to be moved into the new buffer so it costs $k + 1$ to make this insertion, where k is the number of old items. Clearly, if there are $N$ items, the worst-case cost for one insertion can be $\Omega (N)$.  To show that the average cost is $O(1)$, let us turn to the amortized analysis. To simplify the problem, assume that the buffer is full after all the $N$ items are placed. Which of the following potential functions works?

=== "A"

    The number of items currently in the buffer

=== "B"

    The opposite number of items currently in the buffer

=== "C"

    The number of available blocks currently in the buffer

=== "D"

    The opposite number of available blocks in the buffer

??? abstract "答案解析"

    正确答案：D

    解析：在不需要扩容的插入操作中，剩余的空缓存数可以使势能减少。又每次操作我们需要「加上」操作的势能，因此势能函数应当为负值。

---

第三周 判断题 1-2

When evaluating the performance of data retrieval, it is important to measure the relevancy of the answer set.

??? abstract "答案解析"

    正确答案：F

    解析：评估**数据检索** (data retrieval) 的性能时，我们只关注搜索的响应时间和使用的存储大小。评估**信息检索** (information retrieval) 的性能时，我们才关注检索结果的相关性。
