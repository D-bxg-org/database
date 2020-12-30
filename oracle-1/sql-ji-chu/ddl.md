---
description: 数据定义语言（data definition language）
---

# DDL

## 1 数据定义语句

| 操作对象 |  | 操作方式 |  |
| :---: | :---: | :---: | :---: |
|  | 创建 | 删除 | 修改 |
| 表 | CREATE TABLE | DROP TABLE | ALTER TABLE |
| 视图 | CREATE VIEW | DROP VIEW |  |
| 索引 | CREATE INDEX | DROP INDEX |  |

## 2 创建表

是小括号，不是大括号。

每条语句后是逗号，不是分号。

语句结束是分号。

oracle不区分大小写。但如果使用了字符串，则需要区分，因为“Age”和“AGE”是不同的。

下面三张表符合第三范式。

{% tabs %}
{% tab title="创建学生表" %}
```sql
CREATE TABLE T_STUDENT(
    SNO CHAR(8) PRIMARY KEY,/*主键约束*/
    SNAME VARCHAR2(20) UNIQUE,/*唯一约束*/
    SEX CHAR(4) NOT NULL,/*非空约束*/
    AGE INT CHECK(Age>16),/*检查约束：年龄大于16*/
    DEPT VARCHAR2(15)
);
```
{% endtab %}

{% tab title="创建课程表" %}
```sql
CREATE TABLE T_COURSE(
    CNO CHAR(8) PRIMARY KEY,
    CNAME VARCHAR2(10),
    TNAME VARCHAR2(10),
    CPNO CHAR(8) REFERENCES T_COURSE(Cno),
    CREDIT NUMBER
);
```
{% endtab %}

{% tab title="创建选课表" %}
```sql
CREATE TABLE T_STUDENT_COURSE(
    SNO CHAR(8),
    CNO CHAR(8),
    GRADE NUMBER,
    PRIMARY KEY(SNO,CNO),
    FOREIGN KEY(SNO) REFERENCES T_STUDENT(SNO),
    FOREIGN KEY(CNO) REFERENCES T_COURSE(CNO)
);
```
{% endtab %}
{% endtabs %}

## 3 修改表

```sql
--加一个属性
ALTER TABLE T_STUDENT ADD Height INT;
--修改属性的数据类型
ALTER TABLE T_STUDENT MODIFY Height REAL;
--加检查约束
ALTER TABLE T_STUDENT ADD CONSTRAINT Chk1 CHECK(Height>140);
--删除约束
ALTER TABLE T_STUDENT DROP CONSTRAINT Chk1;
--删除属性
ALTER TABLE T_STUDENT DROP COLUMN Height;
```

## 4 删除表

```sql
/*加了cascade constraints后，会把相关依赖对象一并删除*/
DROP TABLE T_STUDENT [CASCADE CONSTRAINTS];
```

