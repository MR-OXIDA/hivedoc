# 查询语句

查询语句语法：

```plsql
SELECT [ALL | DISTINCT] select_expr, select_expr, ...
FROM table_reference
[WHERE where_condition]
[GROUP BY col_list]
[ORDER BY col_list]
[CLUSTER BY col_list
| [DISTRIBUTE BY col_list] [SORT BY col_list]
]
[LIMIT number]
```

### 全表查询

在 Hive 中进行全表查询，可以使用以下语法：

```sql
SELECT * FROM table_name;
```

其中，`table_name` 是您要查询的表名。这将返回指定表中的所有行和列。

### 选择特定列查询

选择特定列进行查询，可以在 `SELECT` 语句中指定这些列的名称。以下是示例代码：

```sql
SELECT column1, column2, column3 FROM table_name;
```

将 `column1, column2, column3` 替换为您要选择的实际列名，并将 `table_name` 替换为您要查询的表名。

这样，查询结果将仅包含您指定的列，并排除其他列的数据。

### 列别名

在 Hive 中，您可以为查询结果中的列定义别名。这样可以更改列的名称，使其更易于理解或与其他计算字段进行关联。以下是示例代码：

```sql
SELECT column1 AS alias1, column2 AS alias2 FROM table_name;
```

在上面的代码中，`column1` 和 `column2` 是要查询的实际列名，而 `alias1` 和 `alias2` 则是您为它们定义的别名。

通过使用别名，查询结果将显示为具有指定别名的列名，而不是原始列名。这对于提高可读性和编写复杂查询非常有用。

### Limit 语句

Hive 中的 LIMIT 语句用于限制查询结果返回的行数。它可以在 SELECT 查询中使用，以便只获取前几行结果。

下面是一个示例：

```sql
SELECT column1, column2
FROM table_name
LIMIT n;
```

在上面的代码中，`table_name` 是要查询的表名，`column1` 和 `column2` 是要选择的列名，而 `n` 是你想要返回的行数。通过将 `n` 替换为所需的行数，你可以限制查询结果返回的行数。

请注意，Hive 的 LIMIT 语句仅适用于顶层查询，并不适用于子查询或连接查询。此外，如果你正在处理大型数据集，LIMIT 可能会导致性能问题，因为它需要对整个数据集进行扫描并返回指定数量的行。

### &#x20;WHERE 语句

Hive 中的 WHERE 语句用于在查询中添加条件，以过滤出符合特定条件的行。它可以与 SELECT、UPDATE 和 DELETE 等语句一起使用。

下面是一个示例：

```sql
SELECT column1, column2
FROM table_name
WHERE condition;
```

在上面的代码中，`table_name` 是要查询的表名，`column1` 和 `column2` 是要选择的列名，而 `condition` 是你希望行满足的条件。通过将 `condition` 替换为实际的条件表达式，你可以根据特定的条件来筛选查询结果。

条件表达式可以包括比较运算符（如 =、<、>、<=、>=）和逻辑运算符（如 AND、OR、NOT）。你还可以使用通配符和函数来构建更复杂的条件。

以下是一些示例：

* 查询年龄大于等于 18 岁的用户：

```sql
SELECT name, age
FROM users
WHERE age >= 18;
```

* 查询国家为 "USA" 或 "Canada" 的订单：

```sql
SELECT order_id, customer_name
FROM orders
WHERE country = 'USA' OR country = 'Canada';
```

* 查询名称以 "John" 开头的员工：

```sql
SELECT employee_id, full_name
FROM employees
WHERE full_name LIKE 'John%';
```

请注意，在 WHERE 子句中使用字符串时，需要使用单引号将字符串括起来。

### Like 语句

Hive 中的 LIKE 语句用于模式匹配，可以在查询中使用通配符进行字符串的匹配操作。下面是 LIKE 语句的基本语法：

```
SELECT column1, column2, ...
FROM table_name
WHERE column_name LIKE pattern;
```

其中，`column_name` 是要匹配的列名，`pattern` 是要匹配的模式。在 `pattern` 中，你可以使用以下两个通配符：

* `%`：表示任意字符序列（包括空字符）
* `_`：表示单个字符

以下是一些示例：

*   查找以 "abc" 开头的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name LIKE 'abc%';
    ```
*   查找以 "abc" 结尾的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name LIKE '%abc';
    ```
*   查找包含 "abc" 的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name LIKE '%abc%';
    ```

请注意，LIKE 语句对大小写敏感，默认情况下区分大小写。如果你希望不区分大小写，可以使用 `RLIKE` 或 `REGEXP` 运算符，并结合正则表达式来实现更复杂的模式匹配。

### RLIKE 子句

在 Hive 中，RLIKE 子句用于进行基于正则表达式的模式匹配。它可以与 SELECT、WHERE 和 HAVING 等子句一起使用。

下面是 RLIKE 子句的基本语法：

```
SELECT column1, column2, ...
FROM table_name
WHERE column_name RLIKE pattern;
```

其中，`column_name` 是要匹配的列名，`pattern` 是一个正则表达式模式。

以下是一些示例：

*   查找以 "abc" 开头的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name RLIKE '^abc';
    ```
*   查找以 "abc" 结尾的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name RLIKE 'abc$';
    ```
*   查找包含 "abc" 的所有行：

    ```sql
    SELECT *
    FROM table_name
    WHERE column_name RLIKE 'abc';
    ```

请注意，RLIKE 使用的是 Java 正则表达式语法。如果你对正则表达式不熟悉，可能需要参考相关文档或教程来编写符合你需求的正则表达式模式。

### GROUP BY 语句

GROUP BY 语句是用于将查询结果按照一个或多个列进行分组的 SQL 语句。它常与聚合函数（如 COUNT、SUM、AVG 等）一起使用，以对每个分组进行计算和汇总。

基本语法如下：

```
SELECT 列1, 列2, ... FROM 表名
GROUP BY 列1, 列2, ...
```

在 GROUP BY 子句中，你需要指定想要分组的列。查询结果将按照这些列的值进行分组，并为每个分组返回一个结果行。

例如，假设我们有一个存储销售订单信息的表格 "orders"，其中包含列 "product\_name"、"category" 和 "quantity"。如果我们想要按照产品类别对销售数据进行分组并计算每个类别的销售总量，可以使用以下查询：

```
SELECT category, SUM(quantity) as total_quantity
FROM orders
GROUP BY category;
```

上述查询将返回每个产品类别及其对应的销售总量。

需要注意的是，在 SELECT 子句中，除了被分组的列外，还可以使用聚合函数来计算其他统计值。但是，非聚合的列必须出现在 GROUP BY 子句中或者作为聚合函数的参数。

### HAVING 语句

HAVING 语句是在 GROUP BY 语句之后使用的，用于筛选分组后的结果。它允许你在查询中使用聚合函数，并对聚合结果进行过滤。

基本语法如下：

```
SELECT 列1, 列2, ...
FROM 表名
GROUP BY 列1, 列2, ...
HAVING 条件;
```

在 HAVING 子句中，你可以使用聚合函数（如 COUNT、SUM、AVG 等）来定义条件表达式。只有满足这些条件的分组才会被包含在查询结果中。

例如，假设我们有一个存储销售订单信息的表格 "orders"，其中包含列 "product\_name"、"category" 和 "quantity"。如果我们想要找出销售总量大于 100 的产品类别，并计算每个类别的销售总量，可以使用以下查询：

```
SELECT category, SUM(quantity) as total_quantity
FROM orders
GROUP BY category
HAVING total_quantity > 100;
```

上述查询将返回销售总量大于 100 的产品类别及其对应的销售总量。

需要注意的是，HAVING 子句仅适用于对分组后的结果进行筛选，而 WHERE 子句适用于原始数据行的筛选。因此，在使用 HAVING 子句时，必须先指定 GROUP BY 子句。

### Join 语句

Join 语句用于将两个或多个表格根据它们之间的关联列进行连接。通过 Join，我们可以从不同的表中获取相关数据，并将其组合在一起以便进行更复杂的查询和分析。

常见的 Join 类型包括：

1. 内连接（Inner Join）：返回两个表中满足连接条件的匹配行。
2. 左连接（Left Join）：返回左表中所有的行，以及右表中满足连接条件的匹配行。
3. 右连接（Right Join）：返回右表中所有的行，以及左表中满足连接条件的匹配行。
4. 全外连接（Full Outer Join）：返回左表和右表中的所有行，并将它们根据连接条件进行匹配。

下面是一个 Inner Join 的示例：

```sql
SELECT Orders.OrderID, Customers.CustomerName
FROM Orders
INNER JOIN Customers ON Orders.CustomerID = Customers.CustomerID;
```

上述查询将从 "Orders" 表和 "Customers" 表中选择 OrderID 和 CustomerName 列，并且只返回那些具有相同 CustomerID 值的行。

请注意，在使用 Join 语句时，需要指定连接条件（ON 子句），以确保正确地连接表格中的数据。

#### 内连接

在 Hive 中，内连接使用 JOIN 关键字来执行。Hive 支持多种类型的 JOIN 操作，包括内连接、左连接、右连接和全外连接。

要执行内连接操作，可以使用以下语法：

```sql
SELECT <columns>
FROM table1
JOIN table2 ON join_condition;
```

其中，table1 和 table2 是要连接的两个表格，join\_condition 是连接条件。

下面是一个示例，展示如何在 Hive 中执行内连接操作：

```sql
SELECT orders.order_id, customers.customer_name
FROM orders
JOIN customers ON orders.customer_id = customers.customer_id;
```

上述查询将从 "orders" 表和 "customers" 表中选择 order\_id 和 customer\_name 列，并且只返回那些具有相同 customer\_id 值的行。

需要注意的是，在 Hive 中进行连接操作时，默认情况下会执行 MapReduce 作业，这可能导致较高的开销。为了提高性能，可以考虑对数据进行适当的分区和排序，以及使用 Bucketing 等技术来优化连接操作。

#### 左外连接

在 Hive 中，左外连接（Left Outer Join）是一种用于将两个表按照指定的条件进行连接的操作。左外连接会返回左表中所有的记录，并根据连接条件匹配右表中的记录。

以下是一个示例查询语句，演示了如何在 Hive 中执行左外连接：

```
SELECT *
FROM left_table
LEFT OUTER JOIN right_table
ON left_table.key = right_table.key;
```

在这个例子中，我们从 `left_table` 和 `right_table` 进行左外连接，连接条件是它们的 `key` 列相等。结果将包含左表中的所有记录以及与之匹配的右表记录，如果没有匹配的右表记录，则对应的字段值为 NULL。

请注意，上述查询中的 `*` 号表示选择所有列，你可以根据需要替换成具体的列名。

#### 右外连接

右外连接（Right Outer Join）是一种将两个表按照指定条件进行连接的操作，它会返回右表中所有的记录，并根据连接条件匹配左表中的记录。

在 Hive 中执行右外连接可以使用以下示例查询语句：

```
SELECT *
FROM left_table
RIGHT OUTER JOIN right_table
ON left_table.key = right_table.key;
```

在这个例子中，我们从 `left_table` 和 `right_table` 进行右外连接，连接条件是它们的 `key` 列相等。结果将包含右表中的所有记录以及与之匹配的左表记录，如果没有匹配的左表记录，则对应的字段值为 NULL。

同样地，上述查询中的 `*` 号表示选择所有列，你可以根据需要替换成具体的列名。

#### 满外连接

满外连接是一种连接操作，它返回两个表中所有匹配和不匹配的行。如果在一个表中找不到与另一个表匹配的行，则会填充 NULL 值。

以下是一个示例查询语句，演示如何在 Hive 中执行满外连接：

```
SELECT *
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

请注意，`table1` 和 `table2` 是要连接的两个表，而 `column` 是用于连接的列名。这将返回包含两个表中所有行的结果集，其中匹配的行按照连接条件进行匹配，而不匹配的行将以 NULL 值填充。

#### 多表连接查询

```
SELECT e.ename, d.dname, l.loc_name
FROM emp e
JOIN dept d
ON d.deptno = e.deptno
JOIN location l
ON d.loc = l.loc;
```

大多数情况下， Hive 会对每对 JOIN 连接对象启动一个 MapReduce 任务。本例中会首先 启动一个 MapReduce job 对表 e 和表 d 进行连接操作，然后会再启动一个 MapReduce job 将 第一个 MapReduce job 的输出和表 l;进行连接操作。 注意：为什么不是表 d 和表 l 先进行连接操作呢？这是因为 Hive 总是按照从左到右的 顺序执行的。 优化： 当对 3 个或者更多表进行 join 连接时，如果每个 on 子句都使用相同的连接键的 话，那么只会产生一个 MapReduce job。

### 表的别名

在 SQL 查询中，可以使用表的别名来简化查询语句并提高可读性。通过为表分配一个临时的名称或缩写，我们可以在查询中引用该别名而不是完整的表名。

表的别名可以在 FROM 子句中使用 AS 关键字进行定义，也可以直接省略 AS 关键字。

下面是一个使用表的别名的示例：

```sql
SELECT o.OrderID, c.CustomerName
FROM Orders AS o
INNER JOIN Customers AS c ON o.CustomerID = c.CustomerID;
```

上述查询中，Orders 表被赋予了别名 "o"，Customers 表被赋予了别名 "c"。这样，在 SELECT 语句和 JOIN 条件中就可以使用这些别名来引用相应的表格。

需要注意的是，表的别名只在当前查询中有效，并且仅限于该查询内部使用。它们对数据库本身没有任何影响，只是为了方便查询编写和阅读。

####
