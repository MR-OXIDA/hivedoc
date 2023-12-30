# HDFS导出到本地

要将HDFS上的文件导出到本地文件系统，您可以使用Hadoop命令行工具中的`hadoop fs -get`命令。以下是一个示例：

```shell
hadoop fs -get hdfs://<namenode>:<port>/path/to/hdfs/file /path/to/local/directory
```

请确保替换`<namenode>`和`<port>`为您的Hadoop集群的正确名称节点和端口号。同时，将`/path/to/hdfs/file`替换为您想要导出的HDFS文件的路径，将`/path/to/local/directory`替换为您希望保存导出文件的本地目录。

如果成功执行该命令，HDFS上的文件将被复制到指定的本地目录中。

注意：在运行此命令之前，请确保您有足够的权限来访问HDFS上的文件，并且您的本地文件系统具有写入权限。
