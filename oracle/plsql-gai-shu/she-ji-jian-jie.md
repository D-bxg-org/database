# 设计简介

## 1 块结构

```sql
DECLARE

BEGIN

EXCEPTION

END
-------------
一个对象的属性
CURSOR%ISOPEN
一个对象的方法
DBMS_OUTPUT.PUT_LINE()
```

```java
class Sql{
    int a=0;
    
    fun(){
        try{
        
        }catch{
        
        }
    }
}
/**************************************/
一个对象的属性
sql.value
一个对象的方法
sql.fun()
```

```sql
SET SERVEROUTPUT ON;--环境变量，相当于import或者include
BEGIN
    DBMS_OUTPUT.PUT_LINE('AAAAAAAA');--输出，相当于sout()或者printf()
END;
```

```sql
DECLARE
    v_length NUMBER := &length;
    v_width NUMBER := &width;
    v_area NUMBER;
BEGIN
    v_area := v_width * v_length;
    DBMS_OUTPUT.PUT_LINE('长方形面积：'||varea);
END;
```

