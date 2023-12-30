# Insert 导出

### 将查询的结果导出到本地

使用HiveQL中的INSERT OVERWRITE LOCAL DIRECTORY语句结合SELECT语句来实现。以下是一个示例：

```sql
INSERT OVERWRITE LOCAL DIRECTORY '/path/to/output'
SELECT * FROM your_table;
```

在上面的示例中，'/path/to/output' 是指定的输出目录路径，你可以根据自己的需求修改它。

执行以上语句后，查询结果会以原始的数据格式直接写入到指定的本地目录下。确保 Hive 用户对该目录具有写入权限，并且目录不存在或为空，否则可能会导致写入失败。

请注意，LOCAL 关键字用于指定将数据导出到本地文件系统而不是分布式文件系统（如HDFS）。这样做可能会影响性能，因为数据需要从集群节点传输到客户端机器。所以在实际应用中，请根据情况选择合适的导出方式。

### 将查询的结果格式化导出到本地

要将查询结果格式化导出到本地，你可以使用HiveQL中的INSERT OVERWRITE DIRECTORY语句结合SELECT语句来实现。以下是一个示例：

```sql
INSERT OVERWRITE DIRECTORY '/path/to/output'
ROW FORMAT DELIMITED
FIELDS TERMINATED BY '\t'
LINES TERMINATED BY '\n'
SELECT * FROM your_table;
```

在上面的示例中，'/path/to/output' 是指定的输出目录路径，你可以根据自己的需求修改它。ROW FORMAT DELIMITED 子句用于指定字段和行的分隔符，这里使用了制表符作为字段分隔符（'\t'），换行符作为行分隔符（'\n'）。你也可以根据需要选择其他的分隔符。

执行以上语句后，查询结果会以指定的格式写入到指定的目录下的文本文件中。确保 Hive 用户对该目录具有写入权限，并且目录不存在或为空，否则可能会导致写入失败。

请注意，如果目录已经存在并且不为空，Hive 将无法覆盖其中的文件，因此建议选择一个空的目录或者先清空目标目录。

### 将查询的结果导出到 HDFS 上

要将查询结果导出到HDFS（分布式文件系统）上，你可以使用HiveQL中的INSERT OVERWRITE DIRECTORY语句结合SELECT语句来实现。以下是一个示例：

```sql
INSERT OVERWRITE DIRECTORY 'hdfs://namenode:port/path/to/output'
SELECT * FROM your_table;
```

在上面的示例中，'hdfs://namenode:port/path/to/output' 是指定的输出目录路径，你需要将其替换为你实际的HDFS路径。确保 Hadoop 集群正常运行，并且 Hive 用户对该目录具有写入权限。

执行以上语句后，查询结果会以原始的数据格式直接写入到指定的HDFS目录下。

请注意，在执行前，请确保已经启动了Hadoop集群并配置好了HDFS。如果没有正确配置Hadoop和HDFS，可能会导致导出失败。
