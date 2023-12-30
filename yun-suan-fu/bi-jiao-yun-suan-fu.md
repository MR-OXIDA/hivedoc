# 比较运算符

在 Hive 中，你可以使用以下比较运算符来进行条件判断和筛选：

* 等于：`=`。例如：`age = 25`
* 不等于：`<>` 或 `!=`。例如：`country <> 'USA'`
* 大于：`>`。例如：`salary > 5000`
* 小于：`<`。例如：`rating < 4.5`
* 大于等于：`>=`。例如：`quantity >= 10`
* 小于等于：`<=`。例如：`price <= 100`

这些比较运算符可以用于 WHERE 子句中的条件表达式，以过滤出满足特定条件的行。

除了上述基本的比较运算符外，Hive 还支持其他一些高级的比较运算符，如：

* BETWEEN AND：用于检查一个值是否在指定的范围内。例如：`age BETWEEN 18 AND 30`
* IN：用于检查一个值是否属于指定的值列表。例如：`country IN ('USA', 'Canada')`
* LIKE：用于模式匹配，通常与通配符一起使用。例如：`name LIKE 'J%'`
* RLIKE：用于正则表达式匹配。例如：`email RLIKE '^([a-z0-9]+)@([a-z]+)\.com$'`

这些比较运算符可以根据不同的查询需求进行灵活组合和应用。