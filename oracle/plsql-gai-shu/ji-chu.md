# 基础

## 1 命名

变量：v\_开头

常量：c\_开头

游标：\_cursor结尾

异常：e\_开头

记录：\_record结尾

序列：

自定义数据类型（结构体）：\_TYPE结尾

## 2 数据类型

### 2.1  变量与常量

```sql
--变量
v_flag VARCHER2(20) NOT NULL := 'true';
--常量
c_pi CONSTANT NUMBER(8,7) := 3.1415926535;
```

### 2.2 参考类型

```sql
%TYPE--某个字段的数据类型，是基础数据类型
v_no T_STUDENT.SNO%TPYE

%ROWTYPE--某个表中的所有的数据类型，可以理解为一个类。
v_sc T_STUDENT_COURSE%ROWTYPE
```

### 2.3 LOB类型

暂时不介绍

### 2.4 自定义类型

和C语言中的结构体、java中的类的概念相同

```sql
CREATE OR REPLACE TYPE STUDENT_TYPE AS OBJECT(--定义了一个叫STUDENT_TYPE的数据类型
    SNO CHAR(8),
    SNAME VARCHAR2(20),
    AGE INT(3)
);
```

## 4 常用的一些语言规范（SE）

```sql
--输出
DBMS_OUTPUT.PUT_LINE()
--输入
&

--赋值
:=    --与其他语言中的 = 是同等的。

SELECT '字段' INTO '变量名（ v_XXX ）'
--连接
||    --与java中的 + 是同等的。

--一些函数

```

对于select XXX into XXX的说明：

就是select语句，额外附带了into 变量。把查出来的数据存放到了变量中，其余没变。例如：

```sql
SELECT SNAME,AGE INTO V_SNAME,V_AGE
FROM T_STUDENT
WHERE SNO='20180100';
```

