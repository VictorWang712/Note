---
comments: true
---

# 程序设计与算法基础

??? info "课程信息"

    - 教师：何钦铭
    - 学分：4.0
    - 学期：大一秋冬
    - 分数：94 / 4.8

## 习题代码

以下代码适用于**何钦铭**老师班级布置的习题，其他老师的习题安排有较大差异。

<div class="card file-block" markdown="1">
<div class="file-icon"><img src="/Note/assets/images/icons/zip.svg" style="height: 3em;"></div>
<div class="file-body">
<div class="file-title">习题代码</div>
<div class="file-meta">4.66 MB / 2025-01-24</div>
</div>
<a class="down-button" target="_blank" href="/Note/assets/files/computer_science/programming_and_algorithm_basics_code.zip" markdown="1">:fontawesome-solid-download: 下载</a>
</div>

??? note "文件说明"

    - `Curricular`：课堂练习
    - `Experiment`：实验课习题
    - `Homework`：课后作业


## 易错题整理

第二周 判断题 1-4

 为了检查以下 else-if 语句的三个分支是否正确，至少需要设计 5 组测试用例，即 x 的取值至少有五组（小于 0 的数、0、大于 0 且小于 15 的数、15 和大于 15 的数）。

```c
if (x < 0) {
    y = 0;
}
else if (x <= 15) {
    y = 4 * x / 3;
}
else { 
    y = 2.5 * x - 10.5;
}   
```

??? abstract "答案解析"

    正确答案：T

    解析：边界条件需要单独设计一组数据测试。

---

第二周 判断题 1-5

为了检查以下省略 else 的 if 语句的分支是否正确，至少需要设计 3 组测试用例，即 grade 的取值至少有三组（小于 60、等于 60、大于 60）。

```c
if (grade < 60) {    
    printf("Fail\n"); 
}
```

??? abstract "答案解析"

    正确答案：T

    解析：边界条件需要单独设计一组数据测试。

---

第四周 判断题 1-2

可以在一个函数中定义另一个函数。

??? abstract "答案解析"

    正确答案：F

    解析：C 语言中不允许在函数中嵌套定义另一个函数。

---

第四周 判断题 1-3

`sizeof()` 是 C 语言的一个函数，可以计算参量所占内存的字节数。如 `sizeof(int)` 可计算整型所占的内存字节数。

??? abstract "答案解析"

    正确答案：F

    解析：`sizeof` 不是一个函数，而是一个**操作符**。

---

第四周 判断题 1-4

C 语言中，通过函数调用只能获得一个返回值。

??? abstract "答案解析"

    正确答案：F

    解析：函数可以有一个返回值或**无返回值**。

---

第四周 选择题 2-1

在 C 语言程序中，若对函数类型未加显式说明，则函数的隐含类型为（ ）。

??? abstract "答案解析"

    正确答案：`int`

    解析：在无返回值的函数定义中，`void` 不能省略；否则，函数类型被默认定义为 `int` 型。

---

第五周 选择题 2-6

以下说法正确的是：

??? abstract "答案解析"

    正确答案：在一个可以正确执行的 C 语言程序中，一个 C 语言函数的声明（原型）可以出现任意多次。

    解析：一个函数的声明可以出现很多次；一个 C 语言的项目可以包含很多 `.c` 文件，其中有且只能有一个 `main` 函数；`.c` 文件中可以无 `main` 函数，但此时该函数无法单独编译。

---

第五周 选择题 2-15

If all variables have been defined and declared in the following program, all the variables which can be used in function `fun()` are ___.

```c
void fun(int x) {
    static int y;
    return;
}
int z;
void main()
{
    int a, b;
    fun(a);
}
```

??? abstract "答案解析"

    正确答案：`x`,`y`

    解析：只有声明在函数之前的变量才可以在函数中被调用，故 `z` 不可以在 `fun()` 中使用。

---

第十周 判断题 1-6

假设有定义如下：`int array[10];`，则该语句定义了一个数组 `array`。其中 `array` 的类型是整型指针（即：`int *`）。

??? abstract "答案解析"

    正确答案：F

    解析：数组名本身是一个**指针常量**（而非常量指针），其值为数组首元素。虽然在很多情况下，数组名会自动转换为指向数组首元素的指针，但也不能说数组名本身是一个指针。

---

第十周 判断题 1-7

变量定义：`int *p, q;` 中，`p` 和 `q` 都是指针。

??? abstract "答案解析"

    正确答案：F

    解析：`*` 总是与变量名结合，这表明按上述代码定义得到的是指针 `p` 和整型变量 `q`。

---

第十周 选择题 2-3

Among the following assignments or initializations, __ is wrong.

??? abstract "答案解析"

    正确答案：`char str[10]; str="string";`

    解析：Incompatible types in assignment of `const char [7]` to `char [10]`.

---

第十周 选择题 2-11

Among the following assignments or initializations, __ is wrong.

??? abstract "答案解析"

    正确答案：`char s[10]; s="hello";`

    解析：Incompatible types in assignment of `const char [6]` to `char [10]`.

---

第十三周 判断题 1-6

`fseek` 函数一般用于文本文件。

??? abstract "答案解析"

    正确答案：F

    解析；`fseek` 函数一般用于二进制文件，也可以用于文本文件。

---

第十三周 选择题 2-2

按数据的组织形式划分，文件可以分为：

??? abstract "答案解析"

    正确答案：文本文件和二进制文件

    解析：按数据的组织形式划分，文件可以分为文本文件和二进制文件；按存储介质划分，文件可以分为程序文件和数据文件。

---

第十三周 选择题 2-6

以下可作为函数 `fopen` 中第一个参数的正确格式是（ ）。

??? abstract "答案解析"

    正确答案：`"c:\\user\\text.txt"`

    解析：在C语言中单个的 `\` 会被视作转义字符，需要输入 `\\` 才能得到反斜线。

---

第十三周 选择题 2-9

利用函数 `fseek` 可实现的操作是（ ）。

??? abstract "答案解析"

    正确答案：改变文件指针 `fp` 的值；文件的顺序读写；文件的随机读写

    解析：`fseek` 原本的功能是改变文件指针 `fp` 的值，可利用这一功能实现文件的顺序读写和随机读写。

---

第十四周 判断题 1-2

静态局部变量如果没有赋值，其存储单元中将是随机值。

??? abstract "答案解析"

    正确答案：F

    解析：静态局部变量在声明时如果没有被初始化，则自动被赋予 0 值。反之自动变量如果不显式初始化，则其值是不确定的，即其存储单元中将是随机值。

---

期末复习

若变量已正确定义，表达式 `(j=3, j++)` 的值是（ ）。

??? abstract "答案解析"

    正确答案：3

    解析：整个逗号表达式的值为系列中最后一个表达式的值，`j++` 的返回值是自增前的 `j` 的值。
