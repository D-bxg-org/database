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
CREATE TABLE T_STUDENT-COURSE(
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



