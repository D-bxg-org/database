# 设计简介

## 1 块结构

```sql
DECLARE

BEGIN

EXCEPTION

END
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

