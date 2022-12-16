# 1.查询的结构

```sql
#方式1：
SELECT ...,....,... FROM ...,...,.... WHERE 多表的连接条件 AND 不包含组函数的过滤条件 GROUP BY ...,... HAVING 包含组函数的过滤条件 ORDER BY ... ASC/DESC LIMIT ...,...
#方式2： 
SELECT ...,....,... FROM ... JOIN ... ON 多表的连接条件 JOIN ... ON ... WHERE 不包含组函数的过滤条件 AND/OR 不包含组函数的过滤条件 GROUP BY ...,... HAVING 包含组函数的过滤条件 ORDER BY ... ASC/DESC LIMIT ...,... 
#其中： #（1）from：从哪些表中筛选 #（2）on：关联多表查询时，去除笛卡尔积 #（3）where：从表中筛选的条件 #（4）group by：分组依据 #（5）having：在统计结果中再次筛选 #（6）order by：排序 #（7）limit：分页
```



# 2.关键字的顺序是不能颠倒的

```sql
SELECT ... FROM ... WHERE ... GROUP BY ... HAVING ... ORDER BY ... LIMIT...
```

# 3.select语句的执行顺序

```sql
FROM -> WHERE -> GROUP BY -> HAVING -> SELECT 的字段 -> DISTINCT -> ORDER BY -> LIMIT
```

![image-20220702154413592](images\image-20220702154413592.png)

比如你写了一个 SQL 语句，那么它的关键字顺序和执行顺序是下面这样的：

```sql
SELECT DISTINCT player_id, player_name, count(*) as num 
# 顺序 5 FROM player JOIN team ON player.team_id = team.team_id # 顺序 1 WHERE height > 1.80 # 顺序 2 GROUP BY player.team_id # 顺序 3 HAVING num > 2 # 顺序 4 ORDER BY num DESC # 顺序 6 LIMIT 2 # 顺序 7
```

在 SELECT 语句执行这些步骤的时候，每个步骤都会产生一个 虚拟表 ，然后将这个虚拟表传入下一个步

骤中作为输入。需要注意的是，这些步骤隐含在 SQL 的执行过程中，对于我们来说是不可见的。

