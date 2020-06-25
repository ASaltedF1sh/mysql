### [获取所有非manager员工当前的薪水情况](https://www.nowcoder.com/practice/8fe212a6c71b42de9c15c56ce354bebe)

```sql
SELECT de.dept_no, de.emp_no, slr.salary
FROM dept_emp AS de INNER JOIN salaries AS slr
ON de.emp_no = slr.emp_no
WHERE slr.to_date = '9999-01-01' AND de.emp_no NOT IN(
SELECT emp_no FROM dept_manager)
```

### [获取员工其当前的薪水比其manager当前薪水还高的相关信息](获取员工其当前的薪水比其manager当前薪水还高的相关信息)

#### [方法1]
```sql
SELECT dp.emp_no, dm.emp_no AS manager_no, s1.salary AS emp_salary, s2.salary AS manager_salary
FROM dept_emp AS dp, dept_manager AS dm, salaries AS s1, salaries AS s2
WHERE dp.dept_no = dm.dept_no
AND dp.emp_no = s1.emp_no
and dm.emp_no = s2.emp_no
and s1.salary > s2.salary
and s2.to_date='9999-01-01'
and s1.to_date='9999-01-01';
```

#### [方法2]
```sql
SELECT s1.emp_no AS emp_no, s2.emp_no AS manager_no, s1.salary AS emp_salary, s2.salary AS manager_salary
FROM 
     #第一个表：所有员工当前的信息
     (SELECT s.salary, s.emp_no, de.dept_no 
      FROM salaries s INNER JOIN dept_emp de ON s.emp_no = de.emp_no AND s.to_date = '9999-01-01' ) AS s1, 
      INNER JOIN
     #第二个表：所有manager当前的信息
     (SELECT s.salary, s.emp_no, dm.dept_no
      FROM salaries s INNER JOIN dept_manager dm ON s.emp_no = dm.emp_no AND s.to_date = '9999-01-01' ) AS s2
#按照同部门进行连接
ON s1.dept_no = s2.dept_no
WHERE s1.salary > s2.salary;
```

### [汇总各个部门当前员工的title类型的分配数目](https://www.nowcoder.com/practice/4bcb6a7d3e39423291d2f7bdbbff87f8)

```sql
SELECT de.dept_no, dp.dept_name, tt.title, count(*) AS count
FROM dept_emp de INNER JOIN departments dp ON de.dept_no = dp.dept_no
INNER JOIN titles tt ON de.emp_no = tt.emp_no
WHERE tt.to_date ='9999-01-01' and de.to_date = '9999-01-01'
GROUP BY de.dept_no, tt.title;
```

### [每年薪水涨幅超过5000的员工](https://www.nowcoder.com/practice/3a303a39cc40489b99a7e1867e6507c5)

```sql
SELECT s1.emp_no, s1.from_date, (s1.salary - s2.salary) AS salary_growth
FROM salaries s1, salaries s2
WHERE s1.emp_no = s2.emp_no AND s1.from_date = s2.to_date AND s1.salary - s2.salary > 5000
ORDER BY salary_growth DESC;
```

### [使用join查询没有分类的电影名称和id](https://www.nowcoder.com/practice/eb9b13e5257744db8265aa73de04fd44)

#### [方法1]
```sql
SELECT f.film_id, f.title
FROM film f
WHERE f.film_id NOT IN(
     SELECT film_category.film_id
     FROM film_category LEFT JOIN film);
```
#### [方法2]
```sql
SELECT f.film_id, f.title FROM film f LEFT JOIN film_category fc
ON f.film_id = fc.film_id WHERE fc.category_id IS NULL;
```
