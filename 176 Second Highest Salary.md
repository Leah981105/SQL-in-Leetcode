
### Question

Table: ```Employee```


| Column Name | Type |
|-------------|------|
| id          | int  |
| salary      | int  |


id is the primary key column for this table.
Each row of this table contains information about the salary of an employee.
 

Write an SQL query to report the second highest salary from the Employee table. If there is no second highest salary, **the query should report null**


### Answer

- Solution 1
```sql
SELECT
    (SELECT DISTINCT
            Salary
        FROM
            Employee
        ORDER BY Salary DESC
        LIMIT 1 OFFSET 1) AS SecondHighestSalary  #limit 取第一行, offset一行,如果没有就返回NULL
;
```

- Solution 2
IFNULL()函数
```sql
SELECT
    IFNULL(
      (SELECT DISTINCT Salary
       FROM Employee
       ORDER BY Salary DESC
        LIMIT 1 OFFSET 1),
    NULL) AS SecondHighestSalary

```
