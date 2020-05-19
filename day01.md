### [找出属于Action分类的所有电影对应的title,description](https://www.nowcoder.com/practice/2f2e556d335d469f96b91b212c4c203e)

#### 使用子查询的方式

```sql
SELECT f.title,f.description
FROM film AS f
WHERE f.film_id IN (
    SELECT fc.film_id
    FROM film_category AS fc
    WHERE fc.category_id IN 
            (
            SELECT c.category_id
            FROM category AS c
            WHERE c.name = 'Action'));
)
```

#### Inner Join方式

```sql
SELECT f.title, f.description
FROM film AS f INNER JOIN film_category AS fc ON f.film_id = fc.film_id
               INNER JOIN category AS c ON c.category_id = fc.category_id
WHERE c.name = 'Action';
```

### [创建唯一索引和普通索引](https://www.nowcoder.com/practice/e1824daa0c49404aa602cf0cb34bdd75)

```sql
CREATE UNIQUE INDEX uniq_idx_firstname ON actor(first_name);
CREATE INDEX idx_lastname ON actor(last_name);
```

### [删除emp_no重复的记录，只保留最小的id对应的记录](https://www.nowcoder.com/practice/3d92551a6f6d4f1ebde272d20872cf05)

```sql
DELETE
FROM titles_test
WHERE id NOT IN(
         SELECT 
                MIN(id)
                FROM
                         titles_test
                GROUP BY
                         emp_no)
```

### [查找最晚入职员工的所有信息](https://www.nowcoder.com/practice/218ae58dfdcd4af195fff264e062138f)

```sql
SELECT *
FROM employees
WHERE hire_date IN(
                SELECT
                      MAX(hire_date)
                FROM employees);
```
### [查找入职员工时间排名倒数第三的员工所有信息(需要考虑入职时间重复的情况)](https://www.nowcoder.com/practice/ec1ca44c62c14ceb990c3c40def1ec6c)

```sql
SELECT *
FROM employees
WHERE hire_date = (
        SELECT hire_date
        FROM employees
        ORDER BY hire_date DESC
        LIMIT 2,1
        );
```

### [查找当前薪水详情以及部门编号dept_no](https://www.nowcoder.com/practice/c63c5b54d86e4c6d880e4834bfd70c3b)

```sql
SELECT s.*, d.dept_no
FROM salaries AS s INNER JOIN dept_manager AS d
              ON s.emp_no = d.emp_no
WHERE d.to_date = '9999-01-01' AND s.to_date='9999-01-01';
```

### [查找所有已经分配部门的员工的last_name和first_name以及dept_no](https://www.nowcoder.com/practice/6d35b1cd593545ab985a68cd86f28671)

```sql
SELECT e.last_name, e.first_name, d.dept_no
FROM dept_emp AS d LEFT JOIN employees AS e
     ON e.emp_no = d.emp_no;
```


### 一些知识点

#### [mysqlL数据类型介绍](https://www.cnblogs.com/-xlp/p/8617760.html)
#### [left join,right join,inner join,full join之间的区别](https://www.cnblogs.com/lijingran/p/9001302.html)
#### [mysql的子查询](https://blog.csdn.net/qq_26594041/article/details/89438382)
#### [mysql的limit用法](https://www.cnblogs.com/xiaoshen666/p/10824117.html)
#### [mysql索引详细介绍](https://www.jianshu.com/p/0d6c828d3c70)
#### [SQL语句编写规范](https://blog.csdn.net/qq_34100655/article/details/82904797?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.nonecase)
