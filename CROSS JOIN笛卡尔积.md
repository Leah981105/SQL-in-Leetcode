#### CROSS JOIN 笛卡尔积

![image](https://user-images.githubusercontent.com/89485280/149686159-883d75ca-2579-415b-b846-b84e6a0b529d.png)

```
Input: 
Students table:
+------------+--------------+
| student_id | student_name |
+------------+--------------+
| 1          | Alice        |
| 2          | Bob          |
| 13         | John         |
| 6          | Alex         |
+------------+--------------+
Subjects table:
+--------------+
| subject_name |
+--------------+
| Math         |
| Physics      |
| Programming  |


```

```sql
SELECT a.student_id, a.student_name, b.subject_name, COUNT(e.subject_name) AS attended_exams
FROM Students a CROSS JOIN Subjects b  #笛卡尔积
```


```
Output: 
+------------+--------------+--------------+
| student_id | student_name | subject_name |
+------------+--------------+--------------+
| 1          | Alice        | Math         | 
| 1          | Alice        | Physics      | 
| 1          | Alice        | Programming  | 
| 2          | Bob          | Math         | 
| 2          | Bob          | Physics      | 
| 2          | Bob          | Programming  | 
| 6          | Alex         | Math         | 
| 6          | Alex         | Physics      | 
| 6          | Alex         | Programming  | 
| 13         | John         | Math         |
| 13         | John         | Physics      | 
| 13         | John         | Programming  | 
+------------+--------------+--------------+

```
