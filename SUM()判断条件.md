`SUM()`可以用来计算满足条件的TRUE的个数


### Question A
Table: `Product`
```
+--------------+---------+
| Column Name  | Type    |
+--------------+---------+
| product_id   | int     |
| product_name | varchar |
| unit_price   | int     |
+--------------+---------+
product_id is the primary key of this table.
Each row of this table indicates the name and the price of each product.
```
Table: `Sales`
```
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| seller_id   | int     |
| product_id  | int     |
| buyer_id    | int     |
| sale_date   | date    |
| quantity    | int     |
| price       | int     |
+-------------+---------+
This table has no primary key, it can have repeated rows.
product_id is a foreign key to the Product table.
Each row of this table contains some information about one sale.
 ```

Write an SQL query that reports the buyers who have bought S8 but not iPhone. Note that S8 and iPhone are products present in the Product table.

Return the result table in any order.

The query result format is in the following example.

### Answer A

```sql
select s.buyer_id 
from sales as s left join product as p 
on s.product_id=p.product_id
group by buyer_id
having sum(p.product_name='S8')>0 and sum(p.product_name='iPhone')=0 #sum(=) 判断符合条件的次数
```


### Question B

Table 同上

Write an SQL query that reports the products that were only sold in the spring of 2019. That is, between 2019-01-01 and 2019-03-31 inclusive.

Return the result table in any order.

The query result format is in the following example.



### Answer B

```sql
select p.product_id,
    product_name
from Sales s 
inner join Product p on p.product_id = s.product_id
group by p.product_id
having sum(sale_date not between '2019-01-01' and '2019-03-31') = 0  # sum()是组内boolean求和
#将product_id 分组后, 同一组内的date进行判断, 判断后求和, 计算出TRUE的个数, 是纵向相加, 所以必须同时满足都不在范围外才行
```


##### 可以用sum()+条件, 计算比例, 例如点击率, 转化率

```sql
select ad_id,
ifnull(round(sum(action="Clicked")/sum(action<>"Ignored")*100,2),0.00) as ctr
from ads
group by ad_id
order by ctr desc,ad_id 
```
