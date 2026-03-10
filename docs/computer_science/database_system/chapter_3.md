---
comments: true
---

# 第三章 - SQL 介绍

## SQL 查询语言概览

SQL 语言有几个部分：

- **数据定义语言** (Data-Definition Language, DDL)：SQL DDL 提供定义关系模式、删除关系以及修改关系模式的命令。
- **数据操纵语言** (Data-Manipulation Language, DML)：SQL DML 提供从数据库中查询信息以及在数据库中插入元组、删除元组、修改元组的能力。
- **完整性** (integrity)：SQL DDL 包括定义完整性约束的命令，保存在数据库中的数据必须满足所定义的完整性约束。破坏完整性约束的更新是不允许的。
- **视图定义** (view definition)：SQL DDL 包括定义视图的命令。
- **事务控制** (transaction control)：SQL 包括定义事务的开始点和结束点的命令。
- **嵌入式 SQL** (embedded SQL) 和**动态 SQL** (dynamic SQL)：嵌入式和动态 SQL 定义 SQL 语句如何嵌入诸如 C、C++ 和 Java 这样的通用编程语言中。
- **授权** (authorization)：SQL DDL 包括定义对关系和视图的访问权限的命令。

## SQL 数据定义

数据库中的关系集合是用数据定义语言定义的。SQL DDL 不仅能够定义关系的集合，还能够定义有关每个关系的信息，包括：

- 每个关系的模式
- 每个属性的取值类型
- 完整性约束
- 为每个关系维护的索引集合
- 每个关系的安全性和权限信息
- 每个关系在磁盘上的物理存储结构

### 基本类型

SQL 标准支持多种固有类型：

- `char(n)`：具有用户指定长度 $n$ 的固定长度的字符串
- `varchar(n)`：具有用户指定的最大长度 $n$ 的可变长度的字符串
- `int`：整数
- `smallint`：小整数
- `numeric(p, d)`：具有用户指定精度的定点数，整数和小数共有 $p$ 位数字（外加一个符号位），且小数点后有 $d$ 位数字
- `real`、`double precision`：浮点数与双精度浮点数
- `float(n)`：精度至少为 $n$ 位数字的浮点数

每种类型狗可能包含一个被称作**空值** (null) 的特殊值。空值表示一个缺失的值，该值可能存在但无法访问，或者可能根本不存在。

`char` 数据类型存放固定长度的字符串。因此当存入或比较 `char` 类型的值时，会自动在输入内容后补充空格使其长度适配。

### 基本模式定义

我们通过 `create table` 命令来定义 SQL 关系。其通用形式如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/database_system/chapter_3_1.png" width="70%" style="margin: 0 auto;">
</div>

其中 $r$ 是关系名，每个 $A_{i}$ 是关系 $r$ 的模式中的一个属性名，$D_{i}$ 是属性 $A_{i}$ 的域，即 $D_{i}$ 指定了属性 $A_{i}$ 的类型以及可选的约束，用于限制所允许的 $A_{i}$ 取值的集合。

SQL 支持许多不同的完整性约束，我们讨论其中少数几种：

- `primary key()`：主码声明表示括号内若干属性构成关系的主码。主码属性必须是非空且唯一的。
- `foreign key() references`：外码声明表示短息中任意元组在括号内属性上的取值必须对应于 `references` 所指明的关系中某元组在主码属性上的取值。
- `not null`：一个属性上的非空约束表明在该属性上不允许存在空值。

SQL 禁止破坏完整性约束的任何数据库更新，否则将标记一个错误并阻止更新。

一个新创建的关系最初是空的。向关系中插入元组、更新元组以及删除元组是通过数据操纵语句 `insert`、`update` 和 `delete` 来完成的，这些将在[数据库的修改]()一节介绍。

如果要从 SQL 数据库中去掉一个关系，我们使用 `drop table` 命令，其可以从数据库中删除关于指定关系的所有信息。需要注意的是，`drop table r;` 比 `delete from r;` 要更强。后者保留关系 $r$，但删除 $r$ 中的所有元组。前者不仅删除 $r$ 中的所有元组，还删除 $r$ 的模式。

我们使用 `alter table` 命令为已有关系增加属性，关系中的所有元组在新属性上的取值将被赋为 `null`。其格式为 `alter table r add A D;`，其中 $r$ 是现有关系的名称，$A$ 是待添加属性的名称，$D$ 是待添加属性的类型。我们也可以用 `alter table r drop A;` 从关系中去除属性，其中 $r$ 是现有关系的名称，$A$ 是关系的一个属性的名称。

## SQL 查询的基本结构

SQL 查询的基本结构由三个字句构成：`select`、`from` 和 `where`。查询以在 `from` 子句中列出的关系作为其输入，在这些关系上进行 `where` 和 `select` 子句中指定的运算，然后产生一个关系作为结果。

### 单关系查询

我们考虑一个示例查询：

```sql
select name
from instructor;
```

其结果是由属性名 `name` 的单个属性构成的关系。

上述查询可能得到重复的结果，如果我们想去除重复，可以使用 `select distinct`，如下例：

```sql
select distinct dept_name
from instructor;
```

此时查询结果中每一项最多出现一次。

SQL 允许我们使用关键字 `all` 来显式地指明不去除重复：

```sql
select all dept_name
from instructor;
```

`select` 子句还可以带有算术表达式，运算对象可以是常数或元组的属性：

```sql
select ID, name, dept_name, salary * 1.1
from instructor;
```

SQL 还提供了特殊数据类型，如各种形式的**日期** (date) 类型，并允许一些作用于这些类型上的算术函数。

`where` 子句允许我们只选出那些在 `from` 子句的结果关系中满足特定谓词的元组：

```sql
select name
from instructor
where dept_name = 'Comp. Sci.' and salary > 70000;
```

SQL 允许在 `where` 子句中使用逻辑连词 `and`、`or` 和 `not`。

### 多关系查询

有些查询需要从多个关系中获取信息，在 SQL 中我们把需要访问的关系都列在 `from` 子句中，并在 `where` 子句中指定匹配条件。如下例：

```sql
select name, instructor.dept_name, building
from instructor, department
where instructor.dept_name = department.dept_name;
```

可以注意到，上例中我们把重复的属性名前添加了关系名作为前缀。这种命名管理需要出现在 `from` 子句中的关系具有不同的名称。[后面]()我们会看到如何用更名运算来避免可能的冲突。

最后我们给出涉及多个关系的 SQL 查询的通用形式：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/database_system/chapter_3_2.png" width="70%" style="margin: 0 auto;">
</div>

其中每个 $A_{i}$ 代表一个属性，每个 $r_{i}$ 代表一个关系，$P$ 是一个谓词。每种子句的作用如下：

- `select` 子句用于列出查询结果中所需要的属性。
- `from` 子句是在查询求值中需要访问的关系列表，其定义了一个在该子句中所列出关系上的笛卡儿积。
- `where` 子句是作用在 `from` 子句中的关系的属性上的谓词。

## 附加的基本运算

SQL 中还支持几种附加的基本运算。

### 更名运算

SQL 提供了一种重命名结果关系中的属性的方式，其使用如下形式的 `as` 子句：

```sql
old-name as new-name
```

`as` 子句既可以出现在 `select` 子句中，也可以出现在 `from` 子句中。

更名关系的一个重要用途是为了适用于需要比较同一个关系中的元组的情况，为此我们需要把一个关系和它自身进行笛卡儿积运算。如下例：

```sql
select distinct T.name
from instructor as T, instructor as S
where T. salary > S.salary and S.sept_name = 'Biology';
```

像上述查询中 `T` 和 `S` 那样被用来更名关系的标识在 SQL 标准中被称作**相关名称** (correlation name)，也通常被称作**表别名** (table alias)、**相关变量** (correlation variable) 或**元组变量** (tuple variable)。

### 字符串运算

在 SQL 标准中，字符串上的相等运算是大小写敏感的。

SQL 允许在字符串上作用多种函数，例如连接字符串、提取子串、计算字符串长度、大小写转换、去掉字符串后的空格等。

在字符串上可以使用 `like` 运算符来实现模式匹配。我们使用两个特殊的字符来描述模式：

- `%`：匹配任意字串
- `_`：匹配任意一个字符

SQL 通过使用比较运算符 `like` 来表达模式。如下例：

```sql
select dept_name
from department
where building like '%Watson%';
```

为使模式能够包含特殊的模式字符 `%` 和 `_`，SQL 允许定义转移字符。转义字符直接用在特殊的模式字符前，表示该特殊的模式字符被当作普通字符。我们在 `like` 比较运算中使用 `escape` 关键字来定义转义字符，例如：

- `like 'ab\%cd%' escape '\'`
- `like 'ab\\cd%' escape '\'`

SQL 也允许我们通过使用 `not like` 比较运算符来搜索不匹配项。

### `select` 子句中的属性说明

`*` 可以用在 `select` 子句中表示「所有的属性」。如下例：

```sql
select instructor.*
from instructor, teaches
where instructor.ID = teaches.ID;
```

此时 `instructor.*` 表示 `instructor` 的所有属性都被选中。形如 `select *` 的 `select` 子句表示 `from` 子句的结果关系的所有属性都被选中。

### 排列元组的显示次序

SQL 为用户提供了对关系中元组显示次序的一些控制。`order by` 子句的可以让查询结果中的元组按排列顺序显示。如下例：

```sql
select name
from instructor
where dept_name = 'Pysics'
order by name;
```

在缺省情况下，`order by` 子句按升序列出项。如果要说明排序顺序，我们可以用 `desc` 表示降序，或用 `asc` 表示升序。此外，排序可以在多个属性上进行。如下例：

```sql
select *
from instructor
order by salary desc, name asc;
```

### `where` 子句谓词

为了简化 `where` 子句，SQL 提供 `between` 比较运算符来说明一个值小于或等于某个值，同时大于或等于另一个值。如下例：

```sql
select name
from instructor
where salary between 90000 and 100000;
```

类似地，我们也可以使用 `not between` 比较运算符。

SQL 允许我们用符号 $(v_{1}, v_{2}, \cdots, v_{n})$ 来表示一个包含值 $v_{1}, v_{2}, \cdots, v_{n}$ 的 $n$ 维元组，这被称作**行构造器** (row constructor)。在元组上可以运用比较运算符，其将按字典顺序进行比较运算。如下例：

```sql
select name, course_id
from instructor, teaches
where (instructor.ID, dept.name) = (teaches.ID, 'Biology')
```

## 集合运算

SQL 作用在关系上的 `union`、`intersect` 和 `except` 运算对应于集合的并、交和集差运算。

### 并运算

如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
union
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

与 `select` 子句不同，`union` 运算自动去除重复。如果我们想保留所有重复项，就要使用 `union all`。如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
union all
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

### 交运算

如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
intersect
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

`intersect` 运算自动去除重复。如果我们想保留所有重复项，就要使用 `intersect all`。如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
intersect all
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

### 差运算

如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
except
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

`except` 运算自动去除重复。如果我们想保留所有重复项，就要使用 `except all`。如下例：

```sql
    select course_id
    from section
    where semester = 'Fall' and year = 2017
except all
    select course_id
    from section
    where semester = 'Spring' and year = 2018
```

## 空值

涉及**空值** (null value) 的运算有特定的规则。

如果算术表达式的任一输入值为空，则该表达式的结果为空。

涉及空值的任何比较运算和布尔运算的结果是 `unknown`，这是 `true` 和 `false` 之外的第三种逻辑值。

SQL 在谓词中使用特殊的关键字 `is null` 来测试空值。如下例：

```sql
select name
from instructor
where salary is null;
```

同理还有谓词 `is not null`。

SQL 也允许我们使用 `is unknown` 和 `in not unknown` 来测试一个比较运算的结果是否为 `unknown`。

需要注意的是，谓词 `null = null` 返回 `unknown`，但是使用 `delect distinct` 子句时，`{('A', null), ('A', null)}` 这样的两个元组会被认为是相同的。

## 聚集函数

**聚集函数** (aggregate function) 是以值集为输入并返回单个值的函数。SQL 提供了五个标准的固有聚集函数：`avg`、`min`、`max`、`sum` 和 `count`。其中 `sum` 和 `avg` 的输入必须是数字集，但另外三个也可以作用在非数字数据类型的集合上。

### 基本聚集

考虑下例：

```sql
select avg (salary) as avg_salary
from instructor
where dept_name = 'Comp. Sci.';
```

有时在计算聚集函数前需要去重。如下例：

```sql
delect count (distinct ID)
from teaches
where semester = 'Spring' and yaer = 2018;
```

此外，如果我们想统计关系的全部元组，可以使用关键字 `*`。如下例：

```sql
select count (*)
from course;
```

### 分组聚集

有时候我们不仅希望将聚集函数作用在单个元组集上，还希望其作用在一组元组集上。这可以通过 SQL 中的 `group by` 子句实现，其给出一个或多个属性来构造分组。如下例：

```sql
select dept_name, avg (salary) as avg_salary
from instructor
group by dept_name;
```

使用 `group by` 子句时，一个重点在于保证 `select` 中出现但没有被聚集的属性只能是出现在 `group by` 子句中的那些属性。换言之，任何没有出现在 `group by` 子句中的属性如果出现在 `select` 子句中，就只能作为聚集函数的参数。

### `having` 子句

有时候，对分组限定条件比对元组限定条件更有用。SQL 中的 `having` 谓词就可以做到这一点。如下例：

```sql
select dept_name, avg (salary) as avg_salary
from instructor
group by dept_name
having avg (salary) > 42000;
```

与 `select` 子句的情况类似，任何出现在 `having` 子句中，但没有被聚集的属性必须出现在 `group by` 子句中。

### 对空值和布尔值的聚集

在 SQL 中，除了 `count` 之外的所有聚集函数都忽略其输入集合中的空值。规定空集的 `count` 运算值为 0，并且当作用在空集上时，其它所有聚集运算返回一个空值。

聚集函数 `some` 和 `every` 可应用于布尔值的集合，分别用于计算这些值的析取和合取。

## 嵌套子查询

### 集合成员资格

SQL 允许测试元组在关系中的成员资格，由连接词 `in` 来完成。对应的有连接词 `not in` 用于测试集合成员资格的缺失。如下例：

```sql
select distinct course.id
from section
where semester = 'Fall' and year = 2017 and
      course.id in (select course_id
                    from section
                    where semester = 'Spring' and year = 2018);
```

### 集合比较

考虑前文中提到的一个查询示例：

```sql
select distinct T.name
from instructor as T, instructor as S
where T. salary > S.salary and S.sept_name = 'Biology';
```

我们也可以用 `some` 来对应地改写为如下形式：

```sql
select name
from instructor
where salary > some (select salary
                     from instructor
                     where dept.name = 'Biology');
```

类似的比较也可以用于关键字 `all`。如下例：

```sql
select dept_name
from instructor
group by dept_name
having avg (salary) >= all (select avg(salary)
                           from instructor
                           group by dept_name);
```

### 空关系测试

SQL 可以测试一个子查询的结果中是否存在元组，通过 `exists` 结构实现。如下例：

```sql
select distinct course.id
from section as S
where semester = 'Fall' and year = 2017 and
     exists (select *
             from section as T
             where semester = 'Spring' and year = 2018 and S.course_id = T.course_id);
```

上述查询还说明了 SQL 的一个特性：来自外层查询的相关名称可以用在 `where` 子句的子查询中。使用了来自外层查询的相关名称的子查询称作**相关子查询** (correlated subquery)。

类似地，也有 `not exists` 结构用于测试一个子查询的结果中是否不存在元组。

### 重复元组存在性测试

SQL 可以测试一个子查询的结果中是否存在重复元组，通过 `unique` 结构实现。如下例：

```sql
select T.course_id
from course as T
where unique (select R.course_id
              from section as R
              where T.course_id = R.course_id and R.year = 2017);
```

需要注意的是，`unique` 谓词在空集上计算返回真值。

类似地，也有 `not unique` 结构用于测试一个子查询的结果中是否不存在重复元组。

### `from` 子句中的子查询

SQL 允许在 `from` 子句中使用子查询表达式。如下例：

```sql
select dept_name, avg_salary
from (select dept_name, avg (salary) as avg_salary
      from instructor
      group by dept_name)
where avg_salary > 42000;
```

我们可以用 `as` 子句给子查询的结果关系命名。如下例：

```sql
select dept_name, avg_salary
from (select dept_name, avg (salary) as avg_salary
      from instructor
      group by dept_name)
      as dept_avg (dept_name, avg_salary)
where avg_salary > 42000;
```

### `with` 子句

`with` 子句提供了一种定义临时关系的方式，这个定义只对包含 `with` 子句的查询有效。如下例：

```sql
with max_budget (value) as
     (select max (budget)
    from department)
select budget
from department, max_budget
where department.budget = max_budget.value;
```

该查询中的 `with` 子句定义了临时关系 `max_budget`，此关系包含定义了此关系的子查询的结果元组，只能在同一查询的后面部分使用。

### 标量子查询

SQL 允许子查询出现在返回单个值的表达式能够出现的任何地方，只要该子查询只返回一个包含单个属性的元组。这样的子查询称作**标量子查询** (scalar subquery)。如下例：

```sql
select dept_name,
       (select count (*)
        from instructor
        where department.dept_name = instructor.dept_name)
       as num_instructors
from department;
```

该例中的子查询保证只返回单个值，因为它使用了不带 `group by` 的 `count` 聚集函数。

标量子查询可以出现在 `select`、`where` 和 `having` 子句中，也可以不使用聚集函数来定义标量子查询。

### 不带 `from` 子句的标量

某些查询需要计算，但不需要引用任何关系。类似地，某些拆线呢可能有包含 `from` 子句的子查询，但外层查询不需要 `from` 子句。

## 数据库的修改

### 删除

**删除** (delete) 请求的表达方式与查询非常类似。我们只能删除整个元组，而不能只删除某些属性上的值。SQL 用如下语句表示删除：

```sql
delete from r
where P;
```

其中 $P$ 代表一个谓词，$r$ 代表一个关系。`delete` 语句首先从 $r$ 中找出使 $P(t)$ 为真的所有元组 $t$，然后将它们从 $r$ 中删除。`where` 子句可以省略，此时 $r$ 中的所有元组都将被删除。

一条 `delete` 命令只能作用于一个关系。

### 插入

最简单的 `insert` 语句是插入一个元组的请求。SQL 允许在 `insert` 语句中指定属性，这便于插入内容和关系属性的排列顺序相一致。如下例：

```sql
insert into course (course_id, title, dept_name, credits)
    values ('CS-437', 'Database Systems', 'Comp. Sci.', 4);
```

更常见的情况是，我们可能想再查询结果的基础上插入元组。如下例：

```sql
insert into instructor
    select ID, name, dept_name, 18000
    from student
    where dept_name = 'Music' and tot_cred > 144;
```

### 更新

在某些情况下，我们可能希望在不改变一个元组所有值的情况下改变其某个属性的值。为达到这一目的，可以使用 `update` 语句。如下例：

```sql
update instructor
set salary = salary * 1.05
where salary < 70000;
```

`update` 语句的 `where` 子句可以包含 `select` 语句的 `where` 子句中的任何合法结构。

SQL 提供 `case` 结构，其一般格式如下：

<div style="text-align: center; margin-top: 0px;">
<img src="https://raw.githubusercontent.com/VictorWang712/Note/refs/heads/main/docs/assets/images/computer_science/database_system/chapter_3_3.png" width="70%" style="margin: 0 auto;">
</div>

当 $i$ 是第一个满足的 $\text{pred}_{1}, \text{pred}_{2}, \cdots. \text{pred}_{n}$ 时，此操作就会返回 $\text{result}_{i}$。`case` 语句可以用在应该出现值的任何地方。

标量子查询在 SQL 更新语句中非常有用，它们可以用在 `set` 子句中。如下例：

```sql
update student
set tot_cred = (
    select sum (credits)
    from takes, course
    where student.ID = takes.ID and
          takes.course_id = course.course_id and
          takes.grade <> 'F' and
          takes.grade is not null);
```
