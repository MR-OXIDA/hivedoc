# 通过 Location 指定加载数据路径

在 Hive 中，可以使用 `LOCATION` 关键字来指定加载数据的路径。下面是语法和示例：

```sql
CREATE TABLE table_name (
  column1 data_type,
  column2 data_type,
  ...
)
LOCATION 'hdfs://path/to/data';
```

在上述语法中：

* `table_name` 是要创建的表的名称。
* `column1`, `column2`, ... 是表的列名和对应的数据类型。
* `'hdfs://path/to/data'` 是数据存储的路径，需要以 HDFS (Hadoop Distributed File System) 的格式指定。

以下是一个具体的示例：

```sql
CREATE TABLE employee (
  id INT,
  name STRING,
  age INT
)
LOCATION 'hdfs://my_hdfs_path/employee_data';
```

在这个示例中，我们创建了一个名为 `employee` 的表，它有三列：`id`、`name` 和 `age`。数据将被加载到位于 `hdfs://my_hdfs_path/employee_data` 的位置。

请确保你已经正确配置了 Hadoop 和 Hive，并且指定的路径在 HDFS 上是可访问的。
