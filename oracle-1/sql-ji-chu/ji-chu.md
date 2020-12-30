# 基础

## 1 DDL

### 1.1 数据类型

```sql
--数值型
INT
SMALLINT
NUMERIC(p,s)
FLOAT
REAL
DOUBLE PRECISION
--字符型
CHAR(n)
VARCHAR(n)
--位串型
BIT(n)
BIT VARYING(n)
--时间型
DATE
TIME
--布尔型
BOOLEAN
```

### 1.2 约束条件

```sql
PRIMARY KEY
FOREIGN KEY
NOT NULL
UNIQUE
CHECK()

```

## 2 DQL

### 2.1 查询条件

写在where后。

between and是闭区间，也就是说包含两个端点的数。

> 参考：[https://blog.csdn.net/itmyhome1990/article/details/73333896](https://blog.csdn.net/itmyhome1990/article/details/73333896)

| 查询条件 | 谓词 |
| :--- | :--- |
| 比较 | =, &gt;, &lt;, not |
| 确定范围 | between and |
| 确定集合 | in |
| 字符匹配 | like |
| 空值 | is null |
| 多重条件 | and, or |

### 2.2 聚组函数

写在select后

distinct和all写在函数中，列名前。例如：COUNT\( DISTINCT \* \)。

| 含义 | 函数 |
| :--- | :--- |
| 统计元组个数 | COUNT\(\) |
| 计算列值总和 | SUM\(\) |
| 计算列值平均 | AVG\(\) |
| 计算列值最大值 | MAX\(\) |
| 计算列值最小值 | MIN\(\) |

