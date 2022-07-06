# 626. Exchange Seats
https://leetcode.cn/problems/exchange-seats/  
Table: Seat

| Column Name | Type    |
|-------------|---------|
| id          | int     |
| name        | varchar |

id is the primary key column for this table.   
Each row of this table indicates the name and the ID of a student.   
id is a continuous increment.   
 
Write an SQL query to swap the seat id of every two consecutive students. If the number of students is odd, the id of the last student is not swapped.   
Return the result table ordered by id in ascending order.   
The query result format is in the following example.   
 
Example 1:  
Input:   
Seat table:   

| id | student |
|-------------|---------|
| 1  | Abbot   |
| 2  | Doris   |
| 3  | Emerson |
| 4  | Green   |
| 5  | Jeames  |

Output: 

| id | student |
|-------------|---------|
| 1  | Doris   |
| 2  | Abbot   |
| 3  | Green   |
| 4  | Emerson |
| 5  | Jeames  |

Explanation:    
Note that if the number of students is odd, there is no need to change the last one's seat.

``` sql
# Write your MySQL query statement below
SELECT
    s.id,
    CASE
        WHEN MOD(s.id, 2) = 0 THEN (SELECT student FROM Seat s1 WHERE s1.id = s.id - 1)          
        WHEN MOD(s.id, 2) = 1 AND s.id = (SELECT MAX(id) FROM Seat) THEN student
        ELSE (SELECT student FROM Seat s2 WHERE s2.id = s.id + 1)
    END
    AS student
FROM Seat s
```
