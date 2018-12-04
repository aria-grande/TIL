# Problem
https://leetcode.com/problems/friend-requests-ii-who-has-the-most-friends/

# Solution
```SQL
SELECt a.id as id, count(*) as num
FROM (
  (SELECT requester_id as id FROM request_accepted) UNION ALL 
  (select accepter_id as id from request_accepted)
) a 
GROUP BY a.id
ORDER BY num DESC
LIMIT 1;
```
