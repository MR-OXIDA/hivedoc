# 创建表

### 建表语法

```sql
CREATE [EXTERNAL] TABLE [IF NOT EXISTS] table_name
[(col_name data_type [COMMENT col_comment], ...)]
[COMMENT table_comment]
[PARTITIONED BY (col_name data_type [COMMENT col_comment], ...)]
[CLUSTERED BY (col_name, col_name, ...)
[SORTED BY (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS]
[ROW FORMAT row_format]
[STORED AS file_format]
[LOCATION hdfs_path]
[TBLPROPERTIES (property_name=property_value, ...)]
[AS select_statement]
```

### 字段解释说明

* **CREATE TABLE**：创建一个指定名字的表。如果相同名字的表已经存在， 则抛出异常； 用户可以用 IF NOT EXISTS 选项来忽略这个异常。
* **EXTERNAL**：关键字可以让用户创建一个外部表，在建表的同时可以指定一个指向实 际数据的路径（LOCATION） ， <mark style="color:red;">在删除表的时候，内部表的元数据和数据会被一起删除，而外 部表只删除元数据，不删除数据。</mark>
* **COMMENT**：为表和列添加注释。
* **PARTITIONED BY**：创建分区表。
* **CLUSTERED BY**：创建分桶表。
* **SORTED BY**：不常用， 对桶中的一个或多个列另外排序。
* **ROW FORMAT DELIMITED \[FIELDS TERMINATED BY char] \[COLLECTION ITEMS TERMINATED BY char] \[MAP KEYS TERMINATED BY char] \[LINES TERMINATED BY char] | SERDE serde\_name \[WITH SERDEPROPERTIES (property\_name=property\_value, property\_name=property\_value, ...)]**：用户在建表的时候可以自定义 SerDe 或者使用自带的 SerDe。如果没有指定 ROW FORMAT 或者 ROW FORMAT DELIMITED，将会使用自带的 SerDe。在建表的时候，用户还需 要为表指定列，用户在指定表的列的同时也会指定自定义的 SerDe， Hive 通过 SerDe 确定表 的具体的列的数据。 SerDe 是 Serialize/Deserilize 的简称， hive 使用 Serde 进行行对象的序列与反序列化。
* **STORED AS**：指定存储文件类型。常用的存储文件类型： SEQUENCEFILE（二进制序列文件）、 TEXTFILE（文本）、 RCFILE（列 式存储格式文件） 如果文件数据是纯文本，可以使用STORED AS TEXTFILE。如果数据需要压缩，使用 STORED AS SEQUENCEFILE。
* **LOCATION**：指定表在 HDFS 上的存储位置。
* **AS**：后跟查询语句， 根据查询结果创建表。
* **LIKE**：允许用户复制现有的表结构，但是不复制数据。
