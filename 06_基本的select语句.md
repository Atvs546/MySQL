# 1.select

SELECT 1; #没有任何子句 

SELECT 9/2; #没有任何子句 

# 2.select...from...

语法:

SELECT 标识选择哪些列 

FROM 标识从哪个表中选择 

## 1.选择全部列:

```sql
SELECT * 

FROM departments;
```

注意:一般情况下，除非需要使用表中所有的字段数据，最好不要使用通配符‘*’。使用通配符虽然可以节

省输入查询语句的时间，但是获取不需要的列数据通常会降低查询和所使用的应用程序的效率。通

配符的优势是，当不知道所需要的列的名称时，可以通过它获取它们。

在生产环境下，不推荐你直接使用 SELECT * 进行查询。

## 2.选择特定的列

```sql
SELECT department_id, location_id 

FROM departments; 
```

注意:MySQL中的SQL语句是不区分大小写的，因此SELECT和select的作用是相同的，但是，许多开发人

员习惯将关键字大写、数据列和表名小写，读者也应该养成一个良好的编程习惯，这样写出来的代

码更容易阅读和维护。



## 3.列的别名

- 重命名一个列

- 便于计算

- 紧跟列名，也可以**在列名和别名之间加入关键字****AS****，别名使用双引号**，以便在别名中包含空格或特

- 殊的字符并区分大小写。

- AS 可以省略

- 建议别名简短，见名知意

- 举例

  ```sql
  SELECT last_name AS name, commission_pct comm 
  
  FROM employees;
  ```

  

  ## 4.去除重复行

  默认情况下,查询会返回全部行**在****SELECT****语句中使用关键字****DISTINCT****去除重复行**

  ```sql
  SELECT DISTINCT department_id FROM employees;
  ```

  注意：
  distinct语句中select显示的字段只能是distinct指定的字段，其他字段是不可能出现的。例如，假如表A有“备注”列，如果想获取distinc name，以及对应的“备注”字段，想直接通过distinct是不可能实现的。

## 5.空值参与运算

所有运算符或列值遇到null值，运算的结果都为null

```sql
SELECT employee_id,salary,commission_pct, 

12 * salary * (1 + commission_pct) "annual_sal" 

FROM employees; 
```

这里你一定要注意，在 MySQL 里面， 空值不等于空字符串。一个空字符串的长度是 0，而一个空值的长

度是空。而且，在 MySQL 里面，空值是占用空间的。

## 6.着重号

我们需要保证表中的字段、表名等没有和保留字、数据库系统或常用方法冲突。如果真的相同，请在

SQL语句中使用一对``（着重号）引起来。

 

SELECT * FROM `order`; 

## 7.对常数进行查询

SELECT 查询还可以对常数进行查询。对的，就是在 SELECT 查询结果中增加一列固定的常数列。这列的

取值是我们指定的，而不是从数据表中动态取出的。

你可能会问为什么我们还要对常数进行查询呢？

SQL 中的 SELECT 语法的确提供了这个功能，一般来说我们只从一个表中查询数据，通常不需要增加一个

固定的常数列，但如果我们想整合不同的数据源，用常数列作为这个表的标记，就需要查询常数。

比如说，我们想对 employees 数据表中的员工姓名进行查询，同时增加一列字段 corporation ，这个

字段固定值为“尚硅谷”，可以这样写：

```sql
SELECT '尚硅谷' as corporation, last_name FROM employees;
```

# 3.显示表结构

使用DESCRIBE 或 DESC 命令，表示表结构。

```sql
DESCRIBE employees; 或DESC employees;
```

![image-20220702111819013](images\image-20220702111819013.png)

各个字段含义的如下:

Field：表示字段名称。

Type：表示字段类型，这里 barcode、goodsname 是文本型的，price 是整数类型的。

Null：表示该列是否可以存储NULL值。

Key：表示该列是否已编制索引。PRI表示该列是表主键的一部分；UNI表示该列是UNIQUE索引的一

部分；MUL表示在列中某个给定值允许出现多次。

Default：表示该列是否有默认值，如果有，那么值是多少。

Extra：表示可以获取的与给定列有关的附加信息，例如AUTO_INCREMENT等。



# 4.select...from...where

语法:

SELECT 字段1,字段2 

FROM 表名 

WHERE 过滤条件

1. 使用WHERE 子句，将不满足条件的行过滤掉
2. **WHERE****子句紧随** **FROM****子句**

举例:

```sql
SELECT employee_id, last_name, job_id, department_id FROM employees WHERE department_id = 90 ;
```

