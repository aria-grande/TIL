# Problem
https://leetcode.com/problems/second-degree-follower/

```
In facebook, there is a follow table with two columns: followee, follower.
Please write a sql query to get the amount of each follower’s follower if he/she has one.

For example,
+-------------+------------+
| followee    | follower   |
+-------------+------------+
|     A       |     B      |
|     B       |     C      |
|     B       |     D      |
|     D       |     E      |
+-------------+------------+

should output:
+-------------+------------+
| follower    | num        |
+-------------+------------+
|     B       |  2         |
|     D       |  1         |
+-------------+------------+
```

# Solution
```sql
select b.follower as follower, count(distinct a.follower) as num 
from follow a 
inner join follow b on a.followee = b.follower 
group by b.follower;
```
