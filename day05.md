### [查找所有员工的last_name和first_name以及对应的dept_name，也包括暂时没有分配部门的员工]https://www.nowcoder.com/practice/5a7975fabe1146329cee4f670c27ad55?tpId=82&&tqId=29771&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)
#### [JOIN的嵌套]
```sql
SELECT em.last_name, em.first_name, d.dept_name
FROM employees AS em LEFT JOIN dept_emp AS de ON em.emp_no = de.emp_no
LEFT JOIN departments AS d ON de.dept_no =  d.dept_no;
```

```sql
SELECT last_name, first_name, dept_name
FROM (SELECT *
FROM employees
LEFT JOIN dept_emp
ON employees.emp_no=dept_emp.emp_no
) AS a
LEFT JOIN departments
ON a.dept_no=departments.dept_no;
```

### [查找员工编号emp_no为10001其自入职以来的薪水salary涨幅]https://www.nowcoder.com/practice/c727647886004942a89848e2b5130dc2)

```sql
SELECT (
(SELECT salary FROM salaries WHERE emp_no = '10001' ORDER BY from_date DESC LIMIT 1) - 
(SELECT salary FROM salaries WHERE emp_no = '10001' ORDER BY from_date LIMIT 1))
AS growth;
```

### [查找所有员工自入职以来的薪水涨幅情况]https://www.nowcoder.com/practice/fc7344ece7294b9e98401826b94c6ea5)

```sql
SELECT em.emp_no, (slr.salary - c.salary) AS growth
#先连接两张表得出在职员工信息
FROM employees AS em INNER JOIN salaries AS slr
ON em.emp_no = slr.emp_no AND slr.to_date = '9999-01-01'
#再次连接两张表以备相减
INNER JOIN salaries AS c
ON em.emp_no = c.emp_no AND em.hire_date = c.from_date
ORDER BY growth
```

### [统计各个部门的工资记录数]https://www.nowcoder.com/practice/6a62b6c0a7324350a6d9959fa7c21db3)

```sql
SELECT dp.dept_no, dp.dept_name, count(slr.emp_no) AS sum
FROM departments AS dp INNER JOIN dept_emp AS de ON dp.dept_no = de.dept_no 
INNER JOIN salaries as slr ON de.emp_no = slr.emp_no
GROUP BY dp.dept_no;
```

### [对所有员工的薪水按照salary进行按照1-N的排名]https://www.nowcoder.com/practice/b9068bfe5df74276bd015b9729eec4bf)

####[使用窗函数(sql server、Oracle)]
```sql
select emp_no, salary, dense_rank() over(order by salary desc) as rank
from salaries 
where to_date='9999-01-01'
order by rank,emp_no;
```

####[表的复用]
```sql
#一同使用 DISTINCT 和 COUNT 关键词，来计算非重复结果的数目。
SELECT s1.emp_no, s1.salary, COUNT(DISTINCT s2.salary) AS rank
FROM salaries AS s1, salaries AS s2
#s1.salary <=s2.salary，意思是在输出s1.salary的情况下，有多少个s2.salary大于等于s1.salary
WHERE s1.to_date = '9999-01-01'  AND s2.to_date = '9999-01-01' AND s1.salary <= s2.salary
#用到了count，需要group by
GROUP BY s1.emp_no
ORDER BY s1.salary DESC, s1.emp_no ASC;
```

### 一些知识点
#### [MySQL 8.0窗口函数](https://www.cnblogs.com/DataArt/p/9961676.html)
#### [sql 四大排名函数（ROW_NUMBER、RANK、DENSE_RANK、NTILE）简介](https://blog.csdn.net/shaiguchun9503/article/details/82349050)
