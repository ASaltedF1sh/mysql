### [查找所有员工的last_name和first_name以及对应部门编号dept_no](https://www.nowcoder.com/practice/dbfafafb2ee2482aa390645abd4463bf)

```sql
SELECT e.last_name, e.first_name, d.dept_no
FROM employees AS e LEFT JOIN dept_emp AS d
     ON e.emp_no = d.emp_no;
```

### [查找所有员工入职时候的薪水情况](https://www.nowcoder.com/practice/23142e7a23e4480781a3b978b5e0f33a)

```sql
SELECT s.emp_no, s.salary
FROM employees AS e INNER JOIN salaries AS s
     ON e.emp_no = s.emp_no AND e.hire_date = s.from_date
ORDER BY s.emp_no DESC;
```

### [查找薪水变动超过15次的员工号emp_no以及其对应的变动次数](https://www.nowcoder.com/practice/6d4a4cff1d58495182f536c548fee1ae)

```sql
SELECT emp_no, count(*) AS ct
FROM salaries
GROUP BY emp_no
HAVING ct > 15;
```
### [找出所有员工当前薪水salary情况](https://www.nowcoder.com/practice/ae51e6d057c94f6d891735a48d1c2397)

```sql
SELECT DISTINCT s.salary
FROM salaries AS s
WHERE s.to_date = '9999-01-01'
ORDER BY s.salary DESC;
```

### [获取所有部门当前manager的当前薪水情况，给出dept_no, emp_no以及salary](https://www.nowcoder.com/practice/4c8b4a10ca5b44189e411107e1d8bec1)

```sql
SELECT d.dept_no, d.emp_no, s.salary
FROM dept_manager as d INNER JOIN salaries as s
     ON d.emp_no = s.emp_no and d.to_date = s.to_date
WHERE d.to_date = '9999-01-01';
```

## 知识点
### [mysql中去重————distinct用法](https://www.cnblogs.com/shiluoliming/p/6604407.html)
### [主键关联、外键关联](https://www.cnblogs.com/printN/p/6405628.html)
### [数据库的一对多、多对一、一对一、多对多关系](https://www.iteye.com/blog/duanfei-1870746)
### [having和where的区别](https://www.cnblogs.com/ljf-Sky/p/9024683.html)
