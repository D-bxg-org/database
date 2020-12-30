---
description: 数据操纵语言（data manipulate language）
---

# DML

## 1 插入数据

oracle不支持一次性插入多条数据。

习惯在values和一条记录间加空格，因为他们本身是在一行的。

{% tabs %}
{% tab title="无列名" %}
```sql
INSERT INTO T_STUDENT
VALUES ('05880111','张三','男','23','数学系');
```
{% endtab %}

{% tab title="有列名" %}
```sql
INSERT INTO T_STUDENT (SNO,SNAME,SEX,AGE,DEPT)
VALUES ('05880111','张三','男','23','数学系');
```
{% endtab %}
{% endtabs %}

## 2 修改数据

{% tabs %}
{% tab title="修改一个元组" %}
```sql
UPDATE T_COURSE
SET CREDIT=4
WHERE CNAME='java';
```
{% endtab %}

{% tab title="修改多个元组" %}
```sql
    UPDATE T_STUDENT
    SET AGE=AGE+2
    WHERE SEX='男';
```
{% endtab %}

{% tab title="无条件修改" %}
```sql
UPDATE T_COURSE
SET CREDIT=CREDIT-1;
```
{% endtab %}
{% endtabs %}

## 3 删除数据

```sql
DELETE FROM T_STUDENT
WHERE SNO='20180100';

DELETE FROM T_STUDENT_COURSE
WHERE SNO='20180100';

DELETE FROM T_STUDENT_COURSE;
```

