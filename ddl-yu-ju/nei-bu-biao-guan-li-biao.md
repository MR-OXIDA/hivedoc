# 内部表（管理表）

内部表（Internal Table）是在Hive中创建的一种表，它将数据存储在Hive自己的文件系统或指定的Hadoop分布式文件系统（如HDFS）上。与外部表不同，内部表的元数据和数据都由Hive管理。（默认创建的表都是所谓的管理表，有时也被称为内部表。）因为这种表， Hive 会（或多或 少地）控制着数据的生命周期。 Hive 默认情况下会将这些表的数据存储在由配置项 hive.metastore.warehouse.dir(例如， /user/hive/warehouse)所定义的目录的子目录下。管理表不适合和其他工具共享数据。

当你删除一个内部表时，Hive会同时删除该表的元数据和关联的数据。这意味着删除内部表将永久删除相关数据，所以请谨慎操作。

### 查询表类型

要查询表的类型，你可以使用Hive的元数据管理命令`DESCRIBE FORMATTED`。这个命令将返回有关表的详细信息，包括表的类型。

下面是一个示例：

```sql
DESCRIBE FORMATTED my_table;
```

在这个示例中，`my_table`是你想要查询的表名。执行该命令后，你将获得一份包含表的详细信息的结果集。其中，你可以查看到表的类型信息。

另外，你也可以使用Hive的元数据查询语句来获取表的类型信息。以下是一个示例：

```sql
SELECT table_name, table_type
FROM information_schema.tables
WHERE table_name = 'my_table';
```

在这个示例中，我们使用了`information_schema.tables`系统表来获取表的名称和类型信息。你可以将`table_name`替换为你要查询的具体表名。执行该查询后，你将获得包含表名和类型的结果集。

无论你选择使用哪种方法，都能够帮助你查询表的类型信息。
