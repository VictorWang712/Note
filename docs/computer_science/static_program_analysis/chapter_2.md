---
comments: true
---

# 第二章 - 中间语言

## 编译器和静态分析

**编译器** (compiler) 的基本框架：

- **扫词法分析** (scanner)：利用**正则表达式** (regular expression) 进行**词法分析** (lexical analysis)，最终生成**词元** (token) 到下一步。
- **语法分析器** (parser)：利用**上下文无关文法** (context-free grammar) 进行**语法分析** (syntax analysis)，最终生成**抽象语法树** (abstract syntax tree，AST) 到下一步。
- **类型检查器** (typre checker)：利用**属性文法** (attribute grammar) 进行**语义分析** (semantic analysis)，将 AST 作标记后传输给下一步。
- **转换器** (translator)：将被标记的 AST 转换为**中间语言** (intermediate representation, IR) 进行静态分析。
- **机器码生成器** (code generator)：将 AST 转换为**机器码** (machine code)。

因此，静态分析需要先通过编译生成中间语言后才能进行。

## 抽象语法树和中间表示

我们从一个具体的例子出发，考察 `do i = i + 1; while (a[i] > v)` 这行代码。

其 AST 如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/static_program_analysis/chapter_2_1.png" width="70%" style="margin: 0 auto;">
</div>

用三地址码表示的 IR 如下：

``` linenums="1"
i = i + 1
t1 = a [ i ]
if t1 < v goto 1
```

参照这个例子，我们总结以下有关 AST 和 IR 的特点：

- AST
    - 相对高级而贴近文法结构
    - 通常和编程语言类型有关
    - 适合于快速的类型检查
    - 缺少控制流信息
- IR
    - 相对低级而贴近机器码
    - 通常和编程语言类型无关
    - 简洁而统一的
    - 包含控制流信息
    - 通常作为静态分析的基础

## 三地址码

### 形式

**三地址码** (3-address code, 3AC) 最重要的形式特性在于其命令的右式最多只有一个操作符。

> 举例来说，为了完成 `c = a + b + 3`，三地址码下需要通过两步：`t1 = a + b`，`c = t1 + 3` 来完成。

这一特性也是这种形式得名的由来，即每个三地址码中最多有三个**地址** (address)，其中地址可以是以下类型：

- 变量名：`a`，`b`
- 常量：`3`
- 编译器生成的临时变量：`t1`，`t2`

### 指令

常见指令的三地址码形式如下：

- 二元运算：`x = y bop z`
- 一元运算：`x = uop y`
- 赋值：`x = y`
- 无条件跳转：`goto L`
- 条件跳转：`if x goto L`
- 带关系比较运算的条件跳转：`if x rop y goto L`

## Soot

Soot 是最流行的 Java 静态分析框架，其采用的中间语言是 Jimple，这是一种带类型的三地址码。

我们将介绍一些 Soot 下，常见代码结构所对应的三地址码。

???+ note

    因为 Soot 是面向工程设计的，因此下文中给出的一些三地址码可能并不典型，即存在很多被「过度优化」而不符合一般逻辑的写法。我们希望读者通过阅读以下例子更多把握三地址码的整体结构形式，而非具体的实现细节。

### for 循环

代码：

```java
package nju.sa.examples;
public class ForLoop3AC {
    public static void main(String[] args) {
        int x = 0;
        for (int i = 0; i < 10; i++) {
            x = x + 1;
        }
    }
}
```

三地址码：

```
public static void main(java.lang.String[])
{
    java.lang.String[] r0;
    int i1;

    r0 := @parameter0: java.lang.String[];

    i1 = 0;

 label1:
    if i1 >= 10 goto label2;

    i1 = i1 + 1;

    goto label1;

 label2:
    return;
}
```

### do-while 循环

代码：

```java
package nju.sa.examples;
public class DoWhileLoop3AC {
    public static void main(String[] args) {
        int[] arr = new int[10];
        int i = 0;
        do {
            i = i + 1;
        } while (arr[i] < 10);
    }
}
```

三地址码：

```
public static void main(java.lang.String[])
{
    java.lang.String[] r0;
    int[] r1;
    int $i0, i1;

    r0 := @parameter0: java.lang.String[];

    r1 = newarray (int)[10];

    i1 = 0;

 label1:
    
    i1 = i1 + 1;

    $i0 = r1[i1];

    if $i0 < 10 goto label1;

    return;
}
```

### 方法调用

代码：

```java
package nju.sa.examples;
public class MethodCall3AC {

    String foo(String para1, String para2) {
        return para1 + " " + para2;
    }

    public static void main(String[] args) {
        MethodCall3AC mc = new MethodCall3AC()        ;
        String result = mc.foo("hello", "world");
    }
}
```

三地址码：

```
java.lang.String foo(java.lang.String para1, java.lang.String para2)
{
    nju.sa.examples.MethodCall3AC r0;
    java.lang.String r1, r2, $r7;
    java.lang.StringBuilder $r3, $r4, $r5, $r6;

    r0 := @this: nju.sa.examples.MethodCall3AC;

    r1 := @parameter0: java.lang.String;

    r2 := @parameter1: java.lang.String;

    $r3 = new java.lang.StringBuilder;

    specialinvoke $r3<java.lang.StringBuilder: void <init>()>();

    $r4 = virtualinvoke $r3.<java.lang.StringBuilder: java.lang.StringBuilder append(java.lang.String)>(r1);

    $r5 = virtualinvoke $r4.<java.lang.StringBuilder: java.lang.StringBuilder append(java.lang.String)>(" ");

    $r6 = virtualinvoke $r5.<java.lang.StringBuilder: java.lang.StringBuilder append(java.lang.String)>(r2);

    $r7 = virtualinvoke $r6.<java.lang.StringBuilder: java.lang.String toString()>();

    return $r7;
}

public static void main(java.lang.String[])
{
    java.lang.String[] r0;
    nju.sa.examples.MethodCall3AC $r3;
    r0 =:= @parameter0: java.lang.String[];
    $r3 = new nju.sa.examples.MethodCall3AC;

    specialinvoke $r3.<nju.sa.examples.MethodCall3AC: vois <init>()>();

    virtualinvoke $r3.<nju.sa.examples.MethodCall3AC: java.lang.String foo(java.lang.String, java.lang.String)>("hello", "world");

    return;
}
```

### 类

代码：

```java
package nju.sa.examples;
public class Class3AC {
    public static final double pi = 3.14;
    public static void main(String[] args) {

    }
}
```

三地址码：

```
public class nju.sa.examples.Class3AC extends java.lang.Object
{
    public static final double pi;

    public void <init>()
    {
        nju.sa.examples Class3AC r0;

        r0 := @this: nju.sa.examples.Class3AC;

        specialinvoke r0.<java.lang.Object: void <init>()>();

        return;
    }

    public static void main(java.lang.String[])
    {
        java.lang.String[] r0;

        r0 := @parameter0: java.lang.String[];

        return;
    }

    public static void <clinit>()
    {
        <nju.sa.examples.Class3AC: double pi> = 3.14;

        return;
    }
}
```

## 静态单赋值

## 基本块

## 控制流图
