# 循环

## 1 LOOP

```sql
DECLARE
    i NUMBER:=1;
BEGIN
    LOOP
        DBMS_OUTPUT.PUT_LINE(i||'的平方数是'||i*i);
        i:=i+1;
        
        EXIT WHEN i>10;
    END LOOP;
END;
--------------------------
DECLARE
    i NUMBER:=1;
BEGIN
    LOOP
        DBMS_OUTPUT.PUT_LINE(i||'的平方数是'||i*i);
        i:=i+1;
        IF i>10 THEN
            EXIT;
        EXIT IF;
    END LOOP;
END;
    
```

## 2 WHILE

```sql
DECLARE
    i NUMBER:=1;
BEGIN
    WHILE i<=10 LOOP
        DBMS_OUTPUT.PUT_LINE(i||'的平方数是'||i*i);
        i:=i+1;
    END LOOP;
END;
```

## 3 FOR

```sql
DECLARE
    n NUMBER:=1;
BEGIN
    FOR i IN 2..10 LOOP
        n:=n*i;
    END LOOP;
END;
---------------
DECLARE
    n NUMBER:=1;
BEGIN
    FOR i IN REVERSE 2..10 LOOP
        n:=n*i;
    END LOOP;
END;
```

