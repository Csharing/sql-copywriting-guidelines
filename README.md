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
> SQL 语句在内部执行时会解析成树状展开的结构，SELECT，FROM，WHERE 等关键字定义
了结构体，这些关键词统一使用大写并配合缩进来直观的区分内容和结构。

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
> 同一级别的语句块保持相等距离的缩进，AND 放置在条件前面

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
> 子查询会成为一个完整的表嵌入到上层的结构中，它的内部又是一个完整的结构体，当然
也要使用缩进来定义结构，并且整体要往后缩进一个层次，与上层结构配合。

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
> JOIN 后两张表会形成一张新的大表，该大表需要保持缩进来嵌入到上层，同时内部的两
种表也要通过缩进保持结构

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
> 读者刚开始将逗号前置可能会不太习惯，但这样做会显著的带来两个好处,第一：长的SQL
语句往往选取的字段长短不一，若将逗号放在后面，当缺失逗号时很难发现，放在前面就很
容易排查，第二：调试 SQL 语句时，注释掉最后一个字段，也可以直接运行，减少出错几
率

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
> 当长的函数十分复杂时，若没有清晰的结构，很容易写完就忘。本质上函数与函数参数也
是呈子母对的性质，那么它们也就具有树状的表达结构，通过缩进形式也可以展现出这种树
状结构。

### 举个栗子
```
SELECT L.cloumn1,concat(L.cloumn1,R.cloumn2) FROM (SELECT cloumn1 FROM table1) AS L LEFT JOIN (SELECT cloumn2
 FROM table2) AS R ON L.cloumn3 = R.cloumn3 WHERE L.cloumn1 = 1 AND R.cloumn1 = 2 GROUP BY L.cloumn1,R.cloumn2 
 ORDER BY L.cloumn1,R.cloumn2
```

```
    SELECT
        L.cloumn1
        ,concat(L.cloumn1,R.cloumn2)
    FROM
            (
                SELECT
                    cloumn1
                FROM
                    table1
            ) AS L
        LEFT JOIN
            (
                SELECT
                    cloumn2
                FROM
                    table2
            ) AS R
        ON
            L.cloumn3 = R.cloumn3
    WHERE
        L.cloumn1 = 1
        AND R.cloumn1 = 2
    GROUP BY
        L.cloumn1
        ,R.cloumn2
    ORDER BY
        L.cloumn1
        ,R.cloumn2
```
解析
> 再复杂的语句也可以通过这样的方式拆分以增加可读性，在后期调试时也十分方便

### 结语

    知行合一：
        这个方法可以加深读者对SQL语句的理解，在练习的过程中仔细体会这种树状构，
        假以时日就可以融会贯通，达到一通百通的层次。
    学习函数：
        函数看似纷繁多样，其实基础结构十分简单，所有的函数都是围绕数字，文本，日
        期这三种数据类型，再辅以一些结构和增删查改的过程来展开。运用函数的过程应
        该是逻辑上对这三种类型进行运算，通过逻辑去搜索函数，最后组合起来达到想要
        的目的。so，学习函数的过程就应该是掌握(数字，文本，日期)*增删查改 ，这一
        表达式的过程。
