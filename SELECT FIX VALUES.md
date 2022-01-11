
#### 当我们需要设定每一个id都有固定的三个值在column2的时候

```sql
select distinct spend_date, "desktop" as platform from Spending
union
select distinct spend_date, "mobile" as platform from Spending
union
select distinct spend_date, "both" as platform from Spending 

```

```sql
Output: 
+------------+----------+--------------+-------------+
| spend_date | platform | total_amount | total_users |
+------------+----------+--------------+-------------+
| 2019-07-01 | desktop  | 100          | 1           |
| 2019-07-01 | mobile   | 100          | 1           |
| 2019-07-01 | both     | 200          | 1           |
| 2019-07-02 | desktop  | 100          | 1           |
| 2019-07-02 | mobile   | 100          | 1           |
| 2019-07-02 | both     | 0            | 0           |
+------------+----------+--------------+-------------+ 


```
