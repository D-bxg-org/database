# 判断

## 1 IF

和一般的if相似

```c
int a = 1;
if( a > 0){
    return a;
}
```

```sql
DECLARE
    v_sno T_STUDENT.SNO%TYPE:=&sno;
    v_grade T_STUDENT_COURSE.GRADE%TYPE;
BEGIN
    SELECT AVG(GRADE) INTO v_grade
    FROM T_STUDENT_COURSE
    WHERE SNO=v_sno;
    
    IF v_grade > 85 THEN
        DBMS_OUTPUT.PUT_LINE('此同学的平均成绩是'||v_grade||'，一等奖学金');
    ELSIF v_grade > 75 THEN
        DBMS_OUTPUT.PUT_LINE('此同学的平均成绩是'||v_grade||'，二等奖学金');
    ELSE
        DBMS_OUTPUT.PUT_LINE('此同学的平均成绩是'||v_grade||'，三等奖学金');
    END IF;
END;
```

## 2 CASE

类似switch

```sql
DECLARE
    v_grade VARCHAR2(10):='B';
BEGIN
    CASE v_grade
        WHEN 'A' THEN DBMS_OUTPUT.PUT_LINE('AAA');
        WHEN 'B' THEN DBMS_OUTPUT.PUT_LINE('BBB');
    END CASE;
END;
-------------------------------
DECLARE
    v_grade NUMBER:=20;
BEGIN
    CASE
        WHEN v_grade >=d 10 THEN
            DBMS_OUTPUT.PUT_LINE('AAA');
        WHEN 'B' THEN
            DBMS_OUTPUT.PUT_LINE('BBB');
        ELSE
            DBMS_OUTPUT.PUT_LINE('NO');
    END CASE;
END;
```

