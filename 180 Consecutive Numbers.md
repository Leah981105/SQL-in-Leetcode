### Question

Table: `Logs`


| Column Name | Type    |
|-------------|---------|
| id          | int     |
| num         | varchar |

id is the primary key for this table.
 

Write an SQL query to find all numbers that appear at least three times consecutively.

Return the result table in any order.

The query result format is in the following example.
Example 1:

Input: 
Logs table:

| id | num |
|----|-----|
| 1  | 1   |
| 2  | 1   |
| 3  | 1   |
| 4  | 2   |
| 5  | 1   |
| 6  | 2   |
| 7  | 2   |

Output: 

| ConsecutiveNums |
|-----------------|
| 1               |

Explanation: 1 is the only number that appears consecutively for at least three times.


### Answer

- 1. 保持Num顺序不变, 用row_number() partition by num order by id计算出每个出现的num组中的子排序
```sql
SELECT Id,Num,
	ROW_NUMBER() over(partition by Num order by Id) as SerialGroup
FROM ContinueNumber

```
![image](https://user-images.githubusercontent.com/89485280/147188620-bf187736-4b1a-48c7-8cdd-4d8ca61155d9.png)



- 2. 可以发现, id-子排序的结果,如果一致,说明是连续出现的num

```sql
SELECT Id,Num,
      row_number() over(order by id) -
      row_number() over(partition by Num order by Id) as SerialNumberSubGroup
FROM ContinueNumber
```

![image](https://user-images.githubusercontent.com/89485280/147188794-7535b6eb-baa9-4954-a4c8-126f550ca17d.png)


- 3. 最后选取count(id)大于等于3次的num, 输出即可, 注意group by num 和 SerialNumberSubGroup, 因为id是distinct的, 可以进行count

```sql
SELECT DISTINCT Num ConsecutiveNums FROM 
	(SELECT Id,Num,
		row_number() over(order by id) -
		ROW_NUMBER() over(partition by Num order by Id) as SerialNumberSubGroup
	FROM Logs) as Sub
GROUP BY Num,SerialNumberSubGroup 
HAVING COUNT(Id) >= 3;
```




