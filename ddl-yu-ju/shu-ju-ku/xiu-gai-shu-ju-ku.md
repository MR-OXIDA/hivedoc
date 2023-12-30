# 修改数据库

在Hive中，使用`ALTER DATABASE`语句来更改数据库的属性。

以下是一些可以使用`ALTER DATABASE`语句进行修改的常见属性：

1.  修改数据库的所有者：

    ```sql
    ALTER DATABASE my_database SET OWNER USER user_name;
    ```

    将`my_database`替换为要修改的数据库名称，将`user_name`替换为新的所有者用户名。
2.  修改数据库的位置：

    ```sql
    ALTER DATABASE my_database SET LOCATION 'new_location';
    ```

    将`my_database`替换为要修改的数据库名称，将`new_location`替换为新的数据库存储位置。

请注意，某些属性可能无法直接修改，例如数据库的名称。如果您需要对数据库进行更复杂的更改，建议创建一个新的数据库，并将原始数据库中的表和数据移动到新的数据库中。

### DBPROPERTIES 设置

使用 ALTER DATABASE 命令为某个数据库的 DBPROPERTIES 设置，可以按照以下语法进行操作：

```sql
ALTER DATABASE database_name SET DBPROPERTIES (property_name=property_value, ...);
```

其中，`database_name` 是要修改属性的数据库的名称。`property_name` 是要设置的属性名称，而 `property_value` 则是对应属性的值。

下面是一个示例，演示如何使用 ALTER DATABASE 命令来设置数据库的属性：

```sql
ALTER DATABASE my_database SET DBPROPERTIES ('owner'='John', 'location'='/user/hive/my_database');
```

在这个示例中，我们将名为 `my_database` 的数据库的所有者设置为 `'John'`，并将其位置设置为 `/user/hive/my_database`。

请注意，通过设置 DBPROPERTIES，您可以自定义数据库的属性和值，以满足您的需求。
