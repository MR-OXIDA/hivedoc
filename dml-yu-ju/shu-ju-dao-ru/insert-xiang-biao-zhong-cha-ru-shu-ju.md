# Insert 向表中插入数据

当您想要向Hive表中插入数据时，可以使用INSERT语句。以下是INSERT语句的一般语法：

```sql
INSERT INTO table_name [PARTITION (partition_column = partition_value, ...)]
    [IF NOT EXISTS]
    [column_list]
    query_statement;
```

让我们来解释一下每个部分的含义：

* `table_name`：要插入数据的目标表的名称。
* `PARTITION`：如果您的表有分区，则可以指定要插入数据的特定分区。
* `IF NOT EXISTS`：可选项，表示如果目标表已经存在相同的记录，则不执行插入操作。
* `column_list`：可选项，用于指定要插入数据的列名列表。如果未提供列名列表，则假设与目标表的所有列匹配。
* `query_statement`：用于生成要插入的数据的查询语句。

接下来，让我们看一个示例，演示如何使用INSERT语句将数据插入到Hive表中：

假设我们有一个名为`employees`的表，具有以下结构和数据：

```sql
CREATE TABLE employees (
    id INT,
    name STRING,
    age INT,
    salary FLOAT
);

INSERT INTO employees VALUES
    (1, 'John Doe', 30, 5000.00),
    (2, 'Jane Smith', 35, 6000.00),
    (3, 'Bob Johnson', 28, 4500.00);
```

上面的示例首先创建了一个名为`employees`的表，然后使用INSERT语句将数据插入到该表中。

请注意，如果要从另一个表或查询结果中获取数据并插入到目标表中，可以在INSERT语句的`query_statement`部分中编写适当的查询。例如：

```sql
INSERT INTO employees
    SELECT id, name, age, salary FROM another_table;
```

上面的示例从名为`another_table`的表中选择特定列，并将其插入到`employees`表中。

### 多表（多分区） 插入模式

如果你想在Hive表中插入多个分区的数据，可以使用Hive的动态分区插入模式。这种模式允许你一次性插入多个分区的数据，而不需要逐个指定每个分区。

以下是一个示例的INSERT语句，在多表（多分区）插入模式下向Hive表中插入数据：

```sql
INSERT INTO table_name PARTITION (partition_column1=value1, partition_column2=value2, ...) 
SELECT column1, column2, ...
FROM source_table
WHERE condition;
```

让我解释一下这个语句的各个部分的含义：

* `table_name`：要插入数据的目标Hive表的名称。
* `partition_column1, partition_column2, ...`：分区列的名称。
* `value1, value2, ...`：要插入的分区列的值。
* `column1, column2, ...`：要插入的数据的列名。
* `source_table`：包含要插入数据的源表的名称。
* `condition`：可选项，用于筛选要插入的数据行的条件。

请确保在执行INSERT语句之前已经创建了目标表和相应的分区。此外，确保选择正确的源表，并根据需要提供合适的筛选条件。

以下是一个示例，演示了如何在Hive表中使用多表（多分区）插入模式插入数据：

假设我们有一个名为`employees`的目标表，它具有两个分区列：`year`和`department`。我们要从源表`source_employees`中选择符合条件的员工数据，并将其插入到`employees`表中。

```sql
INSERT INTO employees PARTITION (year=2023, department='HR')
SELECT employee_id, first_name, last_name
FROM source_employees
WHERE year = 2023 AND department = 'HR';

INSERT INTO employees PARTITION (year=2023, department='IT')
SELECT employee_id, first_name, last_name
FROM source_employees
WHERE year = 2023 AND department = 'IT';
```

上述示例中的第一条INSERT语句将满足条件`year = 2023`和`department = 'HR'`的员工数据插入到`employees`表的`(year=2023, department='HR')`分区中。类似地，第二条INSERT语句将满足条件`year = 2023`和`department = 'IT'`的员工数据插入到`employees`表的`(year=2023, department='IT')`分区中。

请根据你的实际需求修改表名、分区列、分区值以及筛选条件。

