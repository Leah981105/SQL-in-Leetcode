
### The SQL ALL Operator
The `ALL` operator:

returns a boolean value as a result
returns TRUE if `ALL` of the subquery values meet the condition
is used with `SELECT`, `WHERE` and `HAVING` statements
ALL means that the condition will be true only if the operation is true for all values in the range. 

```sql
SELECT ALL column_name(s)
FROM table_name
WHERE condition;
```

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name operator ALL
  (SELECT column_name
  FROM table_name
  WHERE condition);
```

### Question

Table: `Project`

```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| project_id  | int     |
| employee_id | int     |
+-------------+---------+
(project_id, employee_id) is the primary key of this table.
employee_id is a foreign key to Employee table.
Each row of this table indicates that the employee with employee_id is working on the project with project_id.
```
Write an SQL query that reports all the projects that have the most employees.

Return the result table in any order.

The query result format is in the following example.


### Answer

```sql
select project_id
from project
group by project_id
having count(*) >= all #全部的值, 而不是返回单一值; 不用 all 是不行的, subquery在判断的时候必须返回单一值
(select count(*) num
from project
group by project_id)
```



