### [获取select * from employees对应的执行计划](https://www.nowcoder.com/practice/18f30bb19fd34abebcf7e6397c7fb5d8)

```sql
EXPLAIN SELECT * FROM employees;
```

### [将employees表的所有员工的last_name和first_name拼接起来作为Name](https://www.nowcoder.com/practice/18f30bb19fd34abebcf7e6397c7fb5d8)

```sql
SELECT em.last_name || ' ' || em.first_name AS Name
FROM employees em;
```

### [创建一个actor表，包含如下列信息(注：sqlite获取系统默认时间是datetime('now','localtime'))](https://www.nowcoder.com/practice/18f30bb19fd34abebcf7e6397c7fb5d8)

```sql
CREATE TABLE IF NOT EXISTS actor (
actor_id smallint(5) NOT NULL PRIMARY KEY,
first_name varchar(45) NOT NULL,
last_name varchar(45) NOT NULL,
last_update timestamp NOT NULL DEFAULT (datetime('now','localtime')));
```

### [对于表actor批量插入如下数据(不能有2条insert语句哦!))](https://www.nowcoder.com/practice/51c12cea6a97468da149c04b7ecf362e)

```sql
INSERT INTO actor VALUES (1, 'PENELOPE', 'GUINESS', '2006-02-15 12:34:33'),
                         (2, 'NICK', 'WAHLBERG', '2006-02-15 12:34:33');
```

### [创建一个actor_name表，并且将actor表中的所有first_name以及last_name导入该表](https://www.nowcoder.com/practice/881385f388cf4fe98b2ed9f8897846df)

####[sqlite语法]
```sql
CREATE TABLE actor_name AS
SELECT first_name,last_name FROM actor;
```

```sql
create table if not exists actor_name (
    first_name varchar(45) not null,
    last_name varchar(45) not null
);
insert into actor_name select first_name,last_name from actor;
```

### [针对actor表创建视图actor_name_view](https://www.nowcoder.com/practice/b9db784b5e3d488cbd30bd78fdb2a862)

```sql
CREATE VIEW actor_name_view AS
SELECT first_name AS first_name_v, last_name AS last_name_v
FROM actor;
```

### [查询emp_no为10005, 使用强制索引](https://www.nowcoder.com/practice/f9fa9dc1a1fc4130b08e26c22c7a1e5f)

####[sqlite语法]
```sql
SELECT *
FROM salaries
INDEXED BY idx_emp_no
WHERE emp_no = '10005';
```

####[mysql语法]
```sql
SELECT * FROM salaries
FORCE INDEX (idx_emp_no)
WHERE emp_no = 10005;
```

### [新增加一列名字为create_date, 类型为datetime, NOT NULL，默认值为'0000-00-00 00:00:00'](https://www.nowcoder.com/practice/119f04716d284cb7a19fba65dd876b03)

```sql
ALTER TABLE actor
ADD COLUMN create_date datetime NOT NULL DEFAULT ('0000-00-00 00:00:00');
```

### [构造一个触发器audit_log，在向employees_test表中插入一条数据的时候，触发插入相关的数据到audit中](https://www.nowcoder.com/practice/7e920bb2e1e74c4e83750f5c16033e2e)

```sql
CREATE TRIGGER audit_log
AFTER INSERT ON employees_test
BEGIN
    INSERT INTO audit VALUES(NEW.ID,NEW.NAME);
END;
```
