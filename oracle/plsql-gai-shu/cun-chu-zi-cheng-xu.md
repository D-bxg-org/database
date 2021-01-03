# 存储子程序

## 1 存储过程

相当于构造器

### 1.1 创建

过程名中可以定义一些形参，这些形参和java或者其他语言不同，他们也同时表达的return。

| 模式 | 描述 |
| :--- | :--- |
| IN | 形参 |
| OUT | 返回值 |
| IN OUT | 既是形参，又是返回值 |

```sql
CREATE [OR REPLACE] PROCEDURE 过程名()

{IS|AS}--相当于declare

BEGIN

END;
```

无参数：

```sql
CREATE OR REPLACE PROCEDURE OUT_DATE
IS
BEGIN
    DBMS_OUTPUT.PUT_LINE(SYSDATE);
END OUT_DATE;
```

有参数：

```sql
CREATE OR REPLACE PROCEDURE QUERY_STUDENT(
    v_sno IN T_STUDNET.SNO%TYPE,
    v_sname OUT T_STUDNET.SNAME%TYPE,
    v_dept OUT T_STUDNET.DEPT%TYPE
)
IS
BEGIN
    SELECT SNAME,DEPT INTO v_sname,v_dept FROM T_STUDNET WHERE SNO = v_sno;
END QUERY_STUDENT;
```

### 1.2 调用

直接在新建查询中：

```sql
EXECUTE OUT_DATE;
```

在语句中：

```sql
BEGIN
    OUT_DATE;
END;
```

有参数的过程：

```sql
DECLARE
    v_sname T_STUDNET.SNAME%TYPE;
    v_dept T_STUDNET.DEPT%TYPE;
BEGIN
    QUERY_STUDENT('20180100',v_sname,v_dept);
    DBMS_OUTPUT.PUT_LINE(v_sname||v_dept);
END;
```

### 1.3 管理

#### 1.3.1 修改

删除后重新创建

#### 1.3.2 删除

```sql
DROP PROCEDURE RAISE_SAL;
```

#### 1.3.3 查看语法错误

```sql
SHOW ERRORS;
```

#### 1.3.4 查看结构

```sql
DESC QUERY_STUDENT;
```

#### 1.3.5 查看源代码

```sql
SELECT TEXT
FROM USER_SOURCE
WHERE 'QUERY_STUDENT';
```

## 2 存储函数

### 1.1 创建

```sql
CREATE [OR REPLACE] FUNCTION 函数名()

RETURN 数据类型

{IS|AS}--相当于declare

BEGIN

    RETURN

END;
```

无参数：

```sql
CREATE OR REPLACE FUNCTION MAX_SAL
RETURN EMP.SAL%TYPE
IS
    V_SAL EMP.SAL%TYPE
BEGIN
    SELECT MAX(SAL) INTO V_SAL FROM EMP;
    RETURN V_SAL;
END MAX_SAL;
```

有参数：

```sql
CREATE OR REPLACE FUNCTION NUM_DEPT(v_dept T_STUDENT.DEPT%TYPE)
RETURN NUMBER
IS
    v_num NUMBER;
BEGIN
    SELECT COUNT(*) INTO v_num FROM T_STUDNET WHERE DEPT = v_dept;
    RETURN v_NUM;
END NUM_DEPT;
```

### 1.2 调用

```sql
SELECT MAX_SAL FROM dual;
```

```sql
DECLARE
    V_SAL EMP.SAL%TYPE;
BEGIN
    V_SAL:=MAX_SAL;
    DBMS_OUTPUT.PUT_LINE(V_SAL);
END;
```

### 1.3 管理

#### 1.3.1 修改

通过创建来覆盖

#### 1.3.2 删除

```sql
DROP FUNCTION MAX_SAL;
```

#### 1.3.3 查看语法错误

```sql
SHOW ERRORS;
```

#### 1.3.4 查看结构

```sql
DESC MAX_SAL;
```

#### 1.3.5 查看源代码

```sql
SELECT TEXT
FROM USER_SOURCE
WHERE 'MAX_SAL';
```

