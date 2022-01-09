
#### 当条件中group by的id和max()数值需要一一对应时, 可以采用where (x,y) in subquery


```sql

SELECT student_id, MIN(course_id) AS course_id, grade
FROM Enrollments
WHERE (student_id, grade) IN (SELECT student_id, MAX(grade)
                              FROM Enrollments
                              GROUP BY student_id)
                            # pair in
GROUP BY student_id
ORDER BY student_id
``
