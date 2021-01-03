# 基础

## 1 DDL

### 1.1 数据类型

date数据类型可以使用一些函数

> 参考：[https://www.cnblogs.com/ajian/archive/2009/03/25/1421063.html](https://www.cnblogs.com/ajian/archive/2009/03/25/1421063.html)
>
> select to\_char\(sysdate,'yyyy-mm-dd hh24:mi:ss'\) as nowTime from dual; //日期转化为字符串  
> select to\_char\(sysdate,'yyyy'\) as nowYear from dual; //获取时间的年  
> select to\_char\(sysdate,'mm'\) as nowMonth from dual; //获取时间的月  
> select to\_char\(sysdate,'dd'\) as nowDay from dual; //获取时间的日  
> select to\_char\(sysdate,'hh24'\) as nowHour from dual; //获取时间的时  
> select to\_char\(sysdate,'mi'\) as nowMinute from dual; //获取时间的分  
> select to\_char\(sysdate,'ss'\) as nowSecond from dual; //获取时间的秒

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

字符匹配：

```sql
WHERE SNAME LIKE '<匹配串>' [ESCAPE '<换码字符>']

--匹配串格式
'张%'--张三，张四，张五六
'_七%'--张七，陈七，陈七八
'jsq\_%g_' ESCAPE '\'--jsq_几个字g符，jsp_design
```

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

