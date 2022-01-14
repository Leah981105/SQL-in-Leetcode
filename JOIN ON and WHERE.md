#### JOIN ON 和 WHERE 的区别

 - 条件写在where里,先join再筛选, 可能会筛选掉原来有的行
- 条件写在join on 里, 先筛选再join, left join 的时候可以保留左边的table所有内容, 不匹配的设为null. 
用于需要保留left table所有内容, 且right table内容同时要做筛选的时候

```sql
select user_id buyer_id,
    join_date,
    count(distinct order_id) orders_in_2019
from Users u
left join Orders o on u.user_id = o.buyer_id and year(order_date)='2019'
# year(order_date)='2019' 本来可以写在where, 但是因为需要保留left table的所有内容
#放在where就会先join然后再筛掉, 如果放在on就是先筛掉再join, 会设为null
group by user_id
order by user_id
```
