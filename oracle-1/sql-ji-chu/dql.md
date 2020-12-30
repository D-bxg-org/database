---
description: 数据查询语言（data query language）
---

# DQL

## 0 查询的一般形式

```sql
SELECT [ALL|DISTINCT] <列名1 [新列名]>[,<列名2>,<列名3>]
FROM <表名>
WHERE <条件表达式>
GROUP BY <列名> HAVING <组条件表达式>
ORDER BY <列名> [ASC|DESC]
```

## 1 单表查询

### 1.1 列

```sql
SELECT SNO,SNAME,AGE
FROM T_STUDENT;
```

```sql
SELECT *
FROM T_COURSE;
```

```sql
--查询出生日期。
--也就是说，属性名可以简单计算。
SELECT 2018-AGE
FROM T_STUDENT;
--修改列名
SELECT 2018-AGE 出生年份,SEX 性别,SNAME 学生姓名
FROM T_STUDENT;
```

### 1.2 行

```sql
SELECT DISTINCT DEPT
FROM T_STUDENT;
```

使用了查询条件：

```sql
SELECT SNAME
FROM T_STUDENT
WHERE DEPT='数学系';
```

