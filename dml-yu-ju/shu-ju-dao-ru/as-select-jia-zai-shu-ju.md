# As Select 加载数据

你可以使用以下语法在Hive中创建表并加载数据：

```sql
CREATE TABLE new_table AS
SELECT column1, column2, ...
FROM existing_table
WHERE condition;
```

这个查询语句将从现有的`existing_table`中选择特定的列，并根据给定的条件进行过滤。然后，它会将结果插入到新创建的`new_table`中。

请注意，`column1, column2, ...`应该替换为你想要选择的实际列名，`existing_table`应该替换为你要查询的实际表名，而`condition`是一个可选项，用于指定筛选条件。

例如，假设你有一个名为`employees`的表，其中包含`name`和`salary`两列。你想要创建一个新表`high_salary_employees`，其中只包含薪水高于100000的员工信息，你可以执行以下操作：

```sql
CREATE TABLE high_salary_employees AS
SELECT name, salary
FROM employees
WHERE salary > 100000;
```

这样就会在Hive中创建一个名为`high_salary_employees`的新表，并将符合条件的员工信息插入其中。

