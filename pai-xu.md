# 排序

### Order By语句

在Hive中，可以使用`ORDER BY`语句对查询结果进行排序。`ORDER BY`子句用于指定按照哪个列或表达式进行排序，并且可以选择升序（ASC，默认）或降序（DESC）。

以下是使用`ORDER BY`语句的示例：

假设有一个名为"students"的表格，包含学生姓名（name）、成绩（score）和班级（class）。

```sql
SELECT name, score, class
FROM students
ORDER BY score DESC;
```

这将返回按照成绩降序排列的学生信息。得分最高的学生将出现在结果集的顶部。

如果要按照多个列进行排序，可以在`ORDER BY`子句中提供多个列名，并按照优先级逐个指定排序顺序。例如，按照成绩降序排列，如果成绩相同，则按照姓名升序排列：

```sql
SELECT name, score, class
FROM students
ORDER BY score DESC, name ASC;
```

注意：在Hive中，`ORDER BY`会导致全局排序，即所有数据都会被收集到一个节点上进行排序。对于大规模数据集，可能需要考虑性能和资源消耗的因素。如果只需要获取前几行数据，可以结合使用`LIMIT`子句来限制结果集的大小。

#### 按照别名排序

```sql
select ename, sal*2 twosal from emp order by twosal;
```

这个语句是一个Hive查询语句，它从`emp`表中选择了两列数据：`ename`和`sal*2`（即工资的两倍），然后按照`twosal`这个别名进行排序。

让我们逐步解释这个语句：

1. `SELECT ename, sal*2 twosal`: 这部分指定了要选择的列。`ename`表示员工姓名，`sal*2`表示工资的两倍，并使用别名`twosal`来表示这一计算结果。
2. `FROM emp`: 这部分指定了查询要从哪个表中获取数据，这里是从`emp`表中获取数据。
3. `ORDER BY twosal`: 这部分指定了按照`twosal`这个别名进行排序。也就是说，根据工资的两倍值对结果进行升序排序。

执行以上查询后，将会得到按照工资的两倍值进行排序的结果集。

请注意，当使用别名进行排序时，实际上是按照别名所代表的原始列进行排序。在这个例子中，`twosal`代表的是`sal*2`这个计算结果，而不是实际存在于表中的某一列。

### Sort By语句

在 Hive 中，你可以使用 `SORT BY` 语句来对结果进行排序。与 `ORDER BY` 不同的是，`SORT BY` 只会对当前任务或子查询的输出进行排序，并不保证全局排序。

下面是 `SORT BY` 语句的基本语法：

```
SELECT 列1, 列2, ...
FROM 表名
SORT BY 列1 [ASC|DESC], 列2 [ASC|DESC], ...
```

其中，`列1`、`列2` 等表示你想要排序的列名，`表名` 表示你要查询的表。

每个列名后面可以选择性地添加 `ASC`（升序，默认）或 `DESC`（降序），以指定排序的方式。如果没有指定排序方式，默认为升序。

以下是一个示例查询语句，展示了如何在 Hive 中使用 `SORT BY` 进行排序：

```
SELECT name, age, salary
FROM employees
SORT BY name ASC, age DESC;
```

这个查询将从名为 "employees" 的表中选择 "name"、"age" 和 "salary" 三列，并按照 "name" 列的升序和 "age" 列的降序对结果进行排序。

需要注意的是，`SORT BY` 并不支持多个字段之间的优先级排序，它只能对整个结果集进行排序。

### 附录：设置 reduce 个数

在Hive中，你可以使用`SET`语句来设置reduce任务的个数。Reduce任务的个数决定了数据处理过程中并行执行的任务数量。

要设置reduce任务的个数，可以使用以下命令：

```
SET mapreduce.job.reduces=<number>;
```

其中，`<number>`是你想要设置的reduce任务的个数。请注意，这个值应该根据你的数据量和集群配置进行调整，以获得最佳性能。

例如，如果你想将reduce任务的个数设置为10，可以运行以下命令：

```
SET mapreduce.job.reduces=10;
```

请记住，在某些情况下，Hive可能会忽略你对reduce任务个数的设置，因为它会自动根据输入数据的大小和可用资源进行优化。

### 查看设置 reduce 个数

要查看在Hive中设置的reduce任务个数，你可以使用以下命令：

```
SET mapreduce.job.reduces;
```

这将显示当前设置的reduce任务个数。如果你还没有显式地设置过reduce任务个数，则会显示默认值。

例如，运行以下命令来查看当前设置的reduce任务个数：

```
SET mapreduce.job.reduces;
```

输出将类似于：

```
mapreduce.job.reduces=10
```

这表示当前设置的reduce任务个数为10。

