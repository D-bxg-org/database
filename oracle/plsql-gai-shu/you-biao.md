# 游标

## 0 游标的用处

* 首先，我们把select查询出来的结果，作为一张新的表。属性是select中查询的字段，记录是select一共查出来的记录结果。
* 然后我们用游标，截取这张新表中的一部分连续的记录，并存储到一个记录变量中去（XXX\_record）。
* 这就是游标的用处。

## 1 基本写法（显式游标）

### 1.1 游标的数据类型

游标的数据类型，应该和**查询结果的表**的rowtype一致。

当然，也可以自定义游标的内部，定义游标参数是为了传入该值到select语句中去，例如：

```sql
DECLARE
    CURSOR 游标变量_cursor(v_a NUMBER) IS SELECT * FROM T_SUTDNET WHERE SNO=v_a;

OPEN 游标变量_cursor(1)

FETCH 游标变量_cursor INTO v_XXX--注意：此处写游标变量的名称

CLOSE 游标变量_cursor;--和fetch一样，是写游标名称
```

此外，游标类也有一些自带属性可以使用，分别有以下几种：

> 参考：[https://www.breakyizhan.com/oracle/15711.html](https://www.breakyizhan.com/oracle/15711.html)

| 属性 | 描述 |
| :--- | :--- |
| %FOUND | 如果DML语句在更新后或DQL找到结果后影响了数据，则返回true。否则，它返回false。 |
| %NOTFOUND | 如果DML语句在更新后影响数据或DQL找到结果，则返回false。否则，它返回true。 |
| %ISOPEN | 如果游标已打开，则返回true，否则返回false。 |
| %ROWCOUNT | 返回执行DML之后受影响的行数。 |

### 1.2 基本写法

```sql
--定义游标
DECLARE
    CURSOR 游标变量_cursor IS SELECT;
--打开游标
OPEN 游标变量_cursor
--提取到变量中
FETCH 游标变量_cursor INTO v_XXX
--关闭游标
CLOSE 游标变量_cursor
```

> 参考：
>
> [游标与序列的区别](https://blog.csdn.net/weixin_30340617/article/details/99780724)
>
> [游标与序列号](https://blog.csdn.net/qq_44458558/article/details/95944779)

## 2 几个例子

### 2.1 简单循环LOOP

```sql
DECLARE
    v_dept T_STUDENT.DEPT%TYPE:=P_DEPT;
    v_sname T_STUDENT.SNAME%TYPE;
    v_age T_STUDENT.AGE%TYPE;
    CURSOR student_cursor IS SELECT SNAME,AGE FROM T_STUDENT WHERE DEPT=v_dept;
BEGIN
    OPEN student_cursor;
    LOOP
        FETCH student_cursor INTO v_sname,v_age;
        EXIT WHEN student_cursor%NOTFOUND;
    END LOOP;
    CLOSE student_cursor;
END;
```

### 2.2 WHILE循环

```sql
DECLARE
    v_dept T_STUDENT.DEPT%TYPE:=P_DEPT;
    CURSOR student_cursor IS SELECT SNAME,AGE FROM T_STUDENT WHERE DEPT=v_dept;
    student_record student_cursor%ROWTYPE;
BEGIN
    OPEN student_cursor;
    FETCH student_cursor INTO student_record;
    WHILE student_cursor%FOUND LOOP
        DBMS_OUTPUT.PUT_LINE(student_record.SNAME||student_record.AGE);
        FETCH student_cursor INTO student_record;
    END LOOP;
    CLOSE student_cursor;
END;
```

### 2.3 FOR循环

游标处理数据的步骤：

1. 定义游标
2. 打开游标
3. 启动循环
4. fetch游标到变量
5. 检查是否所有行返回
6. 处理返回的行
7. 结束循环
8. 关闭游标

但在for中，不需要打开游标、不需要fetch游标到变量、不需要关闭游标。

#### 2.3.1 基本写法

```sql
FOR XXX_record IN XXX_cursor LOOP

END LOOP;
```

#### 2.3.2 FOR循环中简化的地方

```sql
DECLARE
    v_dept T_STUDENT.DEPT%TYPE:=P_DEPT;
    CURSOR student_cursor IS SELECT SNAME,AGE FROM T_STUDENT WHERE DEPT=v_dept;
    --student_record student_cursor%ROWTYPE;
BEGIN
    --OPEN student_cursor;
    --FETCH student_cursor INTO student_record;
    FOR student_record IN student_cursor LOOP
        DBMS_OUTPUT.PUT_LINE(student_record.SNAME||student_record.AGE);
        --FETCH student_cursor INTO student_record;
    END LOOP;
    --CLOSE student_cursor;
END;
```

## 3 操作数据库

我们知道，我们手动写一个语句时，只能达到操作一条记录的目的，而游标可以帮助我们操作多条记录。

```sql
DECLARE
    CURSOR student_cursor IS SELECT * FROM T_STUDENT WHERE DEPT='计算机系';
BEGIN
    FOR student_record IN student_cursor LOOP
        DELETE FROM T_STUDENT WHERE CURRENT OF student_cursor;
    END LOOP;
END;
```

## 4 带参游标

```sql
DECLARE
    CURSOR student_cursor(v_dept CHAR) IS
    SELECT SNAME,AGE FROM T_STUDENT WHERE DEPT=v_dept;
BEGIN
    FOR student_record IN student_cursor('数学系') LOOP
        DBMS_OUTPUT.PUT_LINE(student_record.SNAME||student_record.AGE);
    END LOOP;
END;
```

## 5 隐式游标

隐式游标都写成SQL

```sql
BEGIN
    DELETE FROM T_STUDENT WHERE DEPT=&P_DEPT;
    IF SQL%NOTFOUND THEN
        DBMS_OUTPUT.PUT_LINE('失败');
    ELSE
        DBMS_OUTPUT.PUT_LINE('成功');
    END IF;
END;
```

