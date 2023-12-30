# 删除数据库

在 Hive 中删除数据库，可以使用以下语法：

```
DROP DATABASE [IF EXISTS] database_name [RESTRICT|CASCADE];
```

其中，`database_name` 是要删除的数据库的名称。`IF EXISTS` 关键字是可选的，如果指定了它，当数据库不存在时不会报错。`RESTRICT` 和 `CASCADE` 是用于控制删除操作的选项。

* 使用 `RESTRICT` 选项时，只有当数据库为空（没有任何表）才能被删除。否则，将抛出错误并拒绝删除操作。
* 使用 `CASCADE` 选项时，无论数据库是否为空，都会强制删除该数据库以及其所有相关对象，如表、视图等。

下面是一些示例，演示如何删除数据库：

1. 删除名为 `my_database` 的数据库：

```sql
DROP DATABASE my_database;
```

2. 如果存在，则删除名为 `my_database` 的数据库：

```sql
DROP DATABASE IF EXISTS my_database;
```

3. 强制删除名为 `my_database` 的数据库及其相关对象：

```sql
DROP DATABASE my_database CASCADE;
```
