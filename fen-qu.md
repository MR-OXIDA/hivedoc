# 分区

### DISTRIBUTE BY语句

在Hive中，`DISTRIBUTE BY`语句用于指定数据的分布方式。它通常与`CLUSTER BY`或`SORT BY`语句一起使用，以控制数据在reduce任务之间的分发方式。

`DISTRIBUTE BY`语句会根据指定的列对数据进行分区，并将具有相同值的行分配到同一个reduce任务上。这可以帮助提高查询性能和并行处理效率。

以下是`DISTRIBUTE BY`语句的基本语法：

```sql
SELECT ...
FROM ...
DISTRIBUTE BY <column>;
```

其中，`<column>`是你想要根据其进行数据分区的列名。

例如，假设我们有一个表`employees`，包含`id`、`name`和`department`列，我们可以使用`DISTRIBUTE BY`语句按照`department`列进行数据分区：

```sql
SELECT *
FROM employees
DISTRIBUTE BY department;
```

这将确保具有相同`department`值的行被分配到同一个reduce任务上进行处理。

请注意，`DISTRIBUTE BY`语句只影响数据的分布方式，并不保证数据的排序。如果你需要按特定列进行排序，请使用`SORT BY`语句。

### Cluster By语句

在Hive中，`CLUSTER BY`语句用于指定数据的排序和分区规则。它与`DISTRIBUTE BY`语句一起使用，可以帮助你控制数据在reduce任务之间的分布方式，并按照指定的列对数据进行排序。

`CLUSTER BY`语句的基本语法如下：

```sql
SELECT ...
FROM ...
CLUSTER BY <column>;
```

其中，`<column>`是你选择的用于排序和分区的列名。

例如，假设你有一个表`employees`，包含以下字段：`employee_id`、`name`和`department`。如果你想按照`department`字段进行数据分区和排序，可以使用如下语句：

```sql
SELECT *
FROM employees
CLUSTER BY department;
```

这将根据部门对数据进行分区，并在每个分区内按照部门进行排序。这样可以确保同一部门的数据被发送到同一个reduce任务上进行处理，并且在每个reduce任务内部按照部门进行排序。

需要注意的是，`CLUSTER BY`语句会隐式地执行`DISTRIBUTE BY`语句，因此你不需要单独指定`DISTRIBUTE BY`语句来控制数据的分布。
