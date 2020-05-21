### [获取所有非manager的员工emp_no](https://www.nowcoder.com/practice/32c53d06443346f4a2f2ca733c19660c)

#### 子查询
```sql
SELECT e.emp_no
FROM employees as e
WHERE e.emp_no NOT IN (
                        SELECT d.emp_no
                        FROM dept_manager as d);
```

#### 连接
```sql
SELECT e.emp_no
FROM employees as e LEFT JOIN dept_manager as d
ON e.emp_no = d.emp_no
WHERE dept_no IS NULL;
```

### [获取所有员工当前的manager](https://www.nowcoder.com/practice/e50d92b8673a440ebdf3a517b5b37d62)

```sql
SELECT de.emp_no, dm.emp_no
FROM dept_emp AS de INNER JOIN dept_manager AS dm
ON de.dept_no = dm.dept_no
WHERE de.emp_no <> dm.emp_no AND dm.to_date = '9999-01-01' AND de.to_date = '9999-01-01';
```

### [获取所有部门中当前员工薪水最高的相关信息](https://www.nowcoder.com/practice/4a052e3e1df5435880d4353eb18a91c6)

```sql
SELECT d.dept_no, s.emp_no, MAX(s.salary)
FROM salaries AS s INNER JOIN dept_emp as d
ON s.emp_no = d.emp_no
WHERE s.to_date =  '9999-01-01' AND d.to_date =  '9999-01-01'
GROUP BY d.dept_no;
```

### [从titles表获取按照title进行分组](https://www.nowcoder.com/practice/72ca694734294dc78f513e147da7821e)

```sql
SELECT t.title, count(*)
FROM titles as t
GROUP BY t.title
HAVING COUNT(*) >= 2;
```

### [查找employees表](https://www.nowcoder.com/practice/a32669eb1d1740e785f105fa22741d5c)

```sql
SELECT *
FROM employees AS e
WHERE e.last_name <> 'Mary' AND e.emp_no - e.emp_no / 2 * 2 <> 0
ORDER BY e.hire_date DESC;
```
