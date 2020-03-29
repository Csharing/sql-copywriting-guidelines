# SQL 高效排版指北
统一 SQL 排版的相关用法，极大提高编写和维护 SQL 的效率。

---
### 语句结构
错误
```
SELECT column1 FROM table1 ORDER BY column1
```
正确
```
    SELECT 
        column1 
    FROM 
        table1
    ORDER BY 
        column1
```
解析
> de 

### 判断条件
错误
```
SELECT column1 FROM table1 WHERE column1=1 AND column2 = 2 
```
正确
```
    SELECT 
        column1 
    FROM 
        table1
    WHERE
        column1 = 1 
        AND column2 = 2 
```
解析
> de 

### 子查询
错误
```
SELECT L.column1 FROM (SELECT column1 FROM table1 ) as L
```
正确
```
    SELECT 
        L.column1 
    FROM 
        (
            SELECT 
                column1 
            FROM 
                table1 
        ) as L
```
解析
> de 

### 连接
错误
```
SELECT table1.column1,table2.column2 FROM table1 LEFT JOIN table2 ON table1.column1 = table2.column1
```
正确
```
    SELECT 
        table1.column1
        ,table2.column2
    FROM
            table1
        LEFT JOIN
            table2
        ON
            table1.column1 = table2.column1
```
解析
> de 

### 逗号
错误
```
SELECT column1,column2,column3 FROM table1
```
正确
```
    SELECT 
        column1
        ,column2
        ,column3
    FROM 
        table1
```
解析
> de 

### 长函数
错误
```
SELECT concat(column1,column2,column3) FROM table1
```
正确
```
    SELECT
        concat(
            column1
            ,column2
            ,column3
        ) 
    FROM 
        table1
```
解析
> de 

### 举个栗子
```
SELECT cloumn1,cloumn2 FROM table1 WHERE cloumn1 = 1 AND cloumn1 = 2 GROUP BY cloumn1,cloumn2 ORDER BY cloumn1,cloumn2
```

```
    SELECT
        cloumn1
        ,cloumn2
    FROM
        table1
    WHERE
        cloumn1 = 1
        AND cloumn1 = 2
    GROUP BY
        cloumn1
        ,cloumn2
    ORDER BY
        cloumn1
        ,cloumn2

```
解析
> de 

### 总结
    层次递进有序，读者可以根据这个规则，自行演化

### 结语
