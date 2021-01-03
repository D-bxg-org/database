# 异常处理

> 参考：[https://www.cnblogs.com/huyong/archive/2011/05/06/2038743.html](https://www.cnblogs.com/huyong/archive/2011/05/06/2038743.html)
>
> | 错误号 | 异常错误信息名称 | 说明 |
> | :--- | :--- | :--- |
> | ORA-0001 | Dup\_val\_on\_index | 违反了唯一性限制 |
> | ORA-0051 | Timeout-on-resource | 在等待资源时发生超时 |
> | ORA-0061 | Transaction-backed-out | 由于发生死锁事务被撤消 |
> | ORA-1001 | Invalid-CURSOR | 试图使用一个无效的游标 |
> | ORA-1012 | Not-logged-on | 没有连接到ORACLE |
> | ORA-1017 | Login-denied | 无效的用户名/口令 |
> | ORA-1403 | No\_data\_found | SELECT INTO没有找到数据 |
> | ORA-1422 | Too\_many\_rows | SELECT INTO 返回多行 |
> | ORA-1476 | Zero-divide | 试图被零除 |
> | ORA-1722 | Invalid-NUMBER | 转换一个数字失败 |
> | ORA-6500 | Storage-error | 内存不够引发的内部错误 |
> | ORA-6501 | Program-error | 内部错误 |
> | ORA-6502 | Value-error | 转换或截断错误 |
> | ORA-6504 | Rowtype-mismatch | 宿主游标变量与 PL/SQL变量有不兼容行类型 |
> | ORA-6511 | CURSOR-already-OPEN | 试图打开一个已处于打开状态的游标 |
> | ORA-6530 | Access-INTO-null | 试图为null 对象的属性赋值 |
> | ORA-6531 | Collection-is-null | 试图将Exists 以外的集合\( collection\)方法应用于一个null pl/sql 表上或varray上 |
> | ORA-6532 | Subscript-outside-limit | 对嵌套或varray索引得引用超出声明范围以外 |
> | ORA-6533 | Subscript-beyond-count | 对嵌套或varray 索引得引用大于集合中元素的个数. |

## 1 基本写法

```sql
DECLARE
    e_exception EXCEPTION;
    PRAGMA EXCEPTION_INIT(e_exception,-02291);
BEGIN

EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('AAAAAAAAAAA');
END;
```

## 2 非预定异常

### 2.1 基本写法

#### 2.1.1 定义

```sql
DECLARE
    e_exception EXCEPTION;
```

#### 2.1.2 关联错误

```sql
PRAGMA EXCEPTION_INIT(e_XXXX,-02291);
```

####  2.1.3 异常处理

```sql
EXCEPTION
    WHEN DUP_VAL_ON_INDEX THEN
        DBMS_OUTPUT.PUT_LINE('AAAAAAAAAAA');
```

### 2.2 异常抛出

```sql
DECLARE
    V_i NUMBER:=1;
    e_e EXCEPTION;
BEGIN
    IF v_i = 1 THEN
        RAISE e_e;
    END IF;
EXCEPTION
    WHEN e_e THEN
        DBMS_OUTPUT.PUT_LINE('AAAAAAAAAAA');
END;
```

## 3 重点异常

```sql
DUP_VAL_ON_INDEX--主键错误
```

