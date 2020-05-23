### [从titles表获取按照title进行分组，注意对于重复的emp_no进行忽略](https://www.nowcoder.com/practice/c59b452f420c47f48d9c86d69efdff20)

```sql
SELECT t.title, count(DISTINCT t.emp_no)  AS ct
FROM titles AS t
GROUP BY title
HAVING ct >= 2;
```

### [统计出当前各个title类型对应的员工当前薪水对应的平均工资](https://www.nowcoder.com/practice/c8652e9e5a354b879e2a244200f1eaae)

```sql
SELECT t.title, avg(s.salary)
FROM titles AS t LEFT JOIN salaries AS s
ON t.emp_no = s.emp_no
WHERE t.to_date='9999-01-01' and s.to_date='9999-01-01'
GROUP BY t.title;
```

### [获取当前薪水第二多的员工的emp_no以及其对应的薪水salary](https://www.nowcoder.com/practice/8d2c290cc4e24403b98ca82ce45d04db)

#### 考虑到重复的情况，需要用子查询去重
```sql
SELECT s.emp_no, s.salary
FROM salaries AS s
WHERE s.to_date = '9999-01-01'
AND s.salary = (  SELECT DISTINCT s_.salary AS ds
                  FROM salaries as s_
                  WHERE s_.to_date = '9999-01-01'
                  ORDER BY ds DESC
                  LIMIT 1,1);
```

### [获取当前薪水第二多的员工的emp_no以及其对应的薪水salary](https://www.nowcoder.com/practice/c1472daba75d4635b7f8540b837cc719)
#### 考虑到重复的情况，需要用子查询去重
```sql
SELECT e.emp_no, MAX(s.salary), e.last_name, e.first_name
FROM employees AS e INNER JOIN salaries AS s
ON e.emp_no = s.emp_no
WHERE s.to_date = '9999-01-01'
AND s.salary <> (SELECT MAX(s_.salary)
                 FROM employees e_ INNER JOIN salaries AS s_
                 WHERE s_.to_date = '9999-01-01')
```
