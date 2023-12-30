# Sqoop 导出

要使用Sqoop将数据从Hive导出到其他外部系统（如关系型数据库），可以使用Sqoop的`export`命令。以下是一个示例代码：

```bash
sqoop export \
--connect jdbc:<database_url> \
--username <username> \
--password <password> \
--table <target_table> \
--export-dir <hdfs_path> \
--input-fields-terminated-by ',' \
--input-lines-terminated-by '\n'
```

在这个命令中，你需要做以下替换：

* `<database_url>`：目标数据库的连接URL。
* `<username>`：用于连接目标数据库的用户名。
* `<password>`：用于连接目标数据库的密码。
* `<target_table>`：目标数据库中的表名。
* `<hdfs_path>`：包含要导出数据的HDFS路径。

此命令将从指定的HDFS路径读取数据，并将其导出到目标数据库的指定表中。

请确保已经安装了Sqoop，并且能够访问目标数据库和Hadoop集群来执行该命令。
