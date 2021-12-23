### Question

Table: ```Employee```


| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |

id is the primary key column for this table.
Each row of this table contains information about the salary of an employee.
 

Write an SQL query to report the nth highest salary from the Employee table. If there is no nth highest salary, the query should report null.

The query result format is in the following example.


### Answer

```sql
CREATE FUNCTION getNthHighestSalary(N INT) RETURNS INT 
BEGIN
    SET N = N-1;
    RETURN (
        SELECT DISTINCT
                Salary AS NthHighestSalary
            FROM
                Employee
            ORDER BY Salary DESC
            LIMIT N , 1  # LIMIT N-1,1 表示从N-1开始算的第一行, 不建议用OFFSET
    );
  
END;
```
