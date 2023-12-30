# 内部表与外部表互相转换

### 方式一：转数据

在Hive中，您可以通过以下方法将内部表转换为外部表或将外部表转换为内部表：

1.  将内部表转换为外部表：

    * 创建一个具有相同模式（schema）的外部表。
    * 使用`INSERT OVERWRITE DIRECTORY`语句将内部表的数据导出到外部表指定的目录中。
    * 使用`DROP TABLE`语句删除原始的内部表。

    请注意，在执行上述步骤之前，请确保已经备份了内部表的数据，并且您理解这些操作可能会影响到数据的持久性和访问权限。
2.  将外部表转换为内部表：

    * 创建一个具有相同模式（schema）的内部表。
    * 使用`INSERT INTO TABLE`语句将外部表的数据插入到新创建的内部表中。
    * 使用`DROP TABLE`语句删除原始的外部表。

    类似地，在执行上述步骤之前，请确保已经备份了外部表的数据，并且您理解这些操作可能会影响到数据的持久性和访问权限。

请记住，内部表和外部表之间的主要区别是数据存储位置和管理方式。内部表的数据由Hive直接管理，而外部表的数据存储在外部文件系统或存储平台中，并由Hive进行引用和查询。因此，在转换过程中，请确保您理解数据的位置和访问权限的变化。

### 方式二：不转数据（修改表属性）

#### &#x20;SET TBLPROPERTIES ('EXTERNAL'='FALSE')

`SET TBLPROPERTIES ('EXTERNAL'='FALSE')`语句用于将一个外部表（External Table）转换为内部表（Internal Table），即将表的存储方式从外部文件系统切换到Hive默认的内部存储。

以下是使用`SET TBLPROPERTIES`语句将外部表转换为内部表的示例：

```sql
-- 创建外部表
CREATE EXTERNAL TABLE my_external_table (
  column1 INT,
  column2 STRING
)
LOCATION '/path/to/external/table'
TBLPROPERTIES ('key1' = 'value1', 'key2' = 'value2');

-- 将外部表转换为内部表
ALTER TABLE my_external_table SET TBLPROPERTIES ('EXTERNAL'='FALSE');
```

在这个示例中，我们首先创建了一个外部表`my_external_table`，并指定了其存储位置和一些自定义属性。然后，通过执行`ALTER TABLE`语句并设置`EXTERNAL`属性为`FALSE`，我们将该外部表转换为内部表。

> 请注意，在将外部表转换为内部表之前，请确保数据已经被拷贝到Hive仓库目录下或其他适当的位置，并且不再需要对外部文件系统进行访问。

#### SET TBLPROPERTIES('EXTERNAL'='TRUE');

`SET TBLPROPERTIES`语句用于设置表的属性。在你提供的例子中，`EXTERNAL='TRUE'`是一个属性键值对，它指定将表的外部标志设置为`TRUE`。

这个语句可以用来修改已存在表的属性，也可以在创建表时使用。如果你想要将一个内部表转换为外部表，你可以使用`SET TBLPROPERTIES`语句将`EXTERNAL`属性设置为`TRUE`。

以下是一个示例，展示了如何使用`SET TBLPROPERTIES`语句将内部表转换为外部表：

```sql
-- 创建内部表
CREATE TABLE my_internal_table (
  column1 INT,
  column2 STRING
);

-- 将内部表转换为外部表
ALTER TABLE my_internal_table SET TBLPROPERTIES ('EXTERNAL'='TRUE');
```

在上面的示例中，我们首先创建了一个名为`my_internal_table`的内部表，并定义了其列。然后，通过执行`ALTER TABLE`语句并使用`SET TBLPROPERTIES`来将内部表转换为外部表。

> 请注意，在执行此操作之前，请确保该内部表的数据需要与外部数据源进行交互，并且你已经准备好将数据存储在指定的外部位置。因为一旦将内部表转换为外部表，表的数据将不再保存在Hive仓库中，而是与指定的外部位置相关联。



