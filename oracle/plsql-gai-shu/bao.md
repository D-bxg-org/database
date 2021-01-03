# 包

## 1 创建

可以把存储子程序都写到包里去。

### 1.1 包说明

相当于java的接口

```sql
CREATE [OR REPLACE] PACKAGE 包名
{IS|AS}
    公共变量的定义
    公共类型的定义
    公共出错处理的定义
    公共游标的定义
    函数说明
    过程说明
END 包名;
```

### 1.1 包主体

java的实现类

```sql
CREATE [OR REPLACE] PACKAGE BODY 包名
{IS|AS}
    私有变量的定义
    私有类型的定义
    私有出错处理的定义
    私有游标的定义
    函数定义
    过程定义
END 包名;
```

## 2 调用

```sql
packageName.fun

packageName.value
```

## 3 重载

和java重载的要求一致。

## 4 管理

#### 1.4.1 修改

删除后重新创建

#### 1.4.2 删除

```sql
DROP PACKAGE packageName;
```

#### 1.4.3 查看语法错误

```sql
SHOW ERRORS;
```

#### 1.4.4 查看结构

```sql
DESC packageName;
```

#### 1.4.5 查看源代码

```sql
SELECT TEXT
FROM USER_SOURCE
WHERE 'packageName';
```

#### 1.4.6 系统包

相当于java自带类。

> 参考：[系统包介绍-很详细](https://blog.csdn.net/bbliutao/article/details/10462919)

