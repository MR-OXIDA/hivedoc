# Export 导出到 HDFS

要将整个 Hive 表导出到 HDFS 上，可以使用 `EXPORT TABLE` 命令。以下是示例代码：

```bash
EXPORT TABLE <table_name> TO '<hdfs_path>';
```

在这个命令中，你需要将 `<table_name>` 替换为你要导出的表名，`<hdfs_path>` 替换为你希望保存结果的HDFS路径。

例如，如果你想将表 `my_table` 导出到 `/user/hadoop/output` 目录下，你可以使用以下命令：

```bash
EXPORT TABLE my_table TO '/user/hadoop/output';
```

请确保对目标 HDFS 目录具有写权限，并且能够连接到 Hive 和 HDFS 集群来执行该命令。

