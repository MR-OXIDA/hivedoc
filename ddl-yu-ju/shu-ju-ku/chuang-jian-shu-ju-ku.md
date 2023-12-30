# 创建数据库

要在Hive中创建数据库，请使用以下语法：

```sql
CREATE DATABASE [IF NOT EXISTS] database_name
  [COMMENT 'database_comment']
  [LOCATION 'hdfs_directory_path']
  [WITH DBPROPERTIES ('key1'='value1', 'key2'='value2', ...)];
```

其中：

* `IF NOT EXISTS`：可选参数，表示如果数据库已经存在，则不会引发错误。
* `database_name`：指定要创建的数据库的名称。
* `COMMENT`：可选参数，用于提供对数据库的描述性注释。
* `LOCATION`：可选参数，指定数据库在HDFS上的存储路径。如果未指定，默认情况下将在Hive仓库目录中创建一个子目录来保存数据库数据。
* `WITH DBPROPERTIES`：可选参数，允许为数据库设置键值对属性。

以下是一个示例：

```sql
CREATE DATABASE IF NOT EXISTS my_database
  COMMENT 'This is a sample database'
  LOCATION '/user/hive/warehouse/my_database.db'
  WITH DBPROPERTIES ('owner'='my_user', 'created_at'='2023-09-17');
```

这个示例将创建一个名为"my\_database"的数据库，如果它不存在的话。它还包括了一个注释和自定义属性。

请注意，在执行此命令之前，确保您具有适当的权限以在Hive中创建数据库。
