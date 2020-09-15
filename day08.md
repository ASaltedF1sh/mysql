### [将所有to_date为9999-01-01的全部更新为NULL,且 from_date更新为2001-01-01](https://www.nowcoder.com/practice/859f28f43496404886a77600ea68ef59?tpId=82&&tqId=29811&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
update titles_test
set to_date = NULL ,from_date = '2001-01-01'
where to_date = '9999-01-01';
```


### [分页查询employees表，每5行一页，返回第2页的数据](https://www.nowcoder.com/practice/f24966e0cb8a49c192b5e65339bc8c03?tpId=82&&tqId=29823&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
SELECT * FROM employees LIMIT 5,5;
```

### [查找排除最大、最小salary之后的当前(to_date = '9999-01-01' )员工的平均工资avg_salary](https://www.nowcoder.com/practice/95078e5e1fba4438b85d9f11240bc591?tpId=82&&tqId=29822&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
select avg(salary) as avg_salary
from salaries
where to_date = '9999-01-01'  
and salary not in(
    select min(salary)
    from salaries
    where to_date = '9999-01-01')
and salary not in(
    select max(salary)
    from salaries
    where to_date = '9999-01-01' );
```

### [使用含有关键字exists查找未分配具体部门的员工的所有信息](https://www.nowcoder.com/practice/c39cbfbd111a4d92b221acec1c7c1484?tpId=82&&tqId=29825&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
select * from employees
where not exists(
    select emp_no from dept_emp
    where dept_emp.emp_no = employees.emp_no);
```


### [获取有奖金的员工相关信息](https://www.nowcoder.com/practice/5cdbf1dcbe8d4c689020b6b2743820bf?tpId=82&&tqId=29827&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
select em.emp_no, em.first_name, em.last_name, b.btype, s.salary, 
    (case b.btype
        when 1 then s.salary * 0.1
        when 2 then s.salary * 0.2
        else s.salary * 0.3 
     end) as bonus
from employees as em inner join emp_bonus as b
on em.emp_no = b.emp_no
inner join salaries as s 
on em.emp_no = s.emp_no 
where s.to_date = '9999-01-01';

```

### [获取Employees中的first_name，查询按照first_name最后两个字母，按照升序进行排列](https://www.nowcoder.com/practice/74d90728827e44e2864cce8b26882105?tpId=82&&tqId=29820&rp=1&ru=/ta/sql&qru=/ta/sql/question-ranking)

```sql
SELECT first_name FROM employees ORDER BY substr(first_name,-2);

```


## 知识点
### [MySQL中exists与in的使用](https://www.cnblogs.com/beijingstruggle/p/5885137.html)
### [MySQL case when 用法](https://www.cnblogs.com/chenduzizhong/p/9590741.html)
### [MySQL substr() 用法](https://blog.csdn.net/weixin_43196158/article/details/93754738)


