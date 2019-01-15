# Problem
https://leetcode.com/problems/house-robber/

```
You are a professional robber planning to rob houses along a street. 
Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected 
and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, 
determine the maximum amount of money you can rob tonight without alerting the police.
```

# Solution
웬만한 솔루션으로는 TLE가 발생한다. DP로 풀었었으나 TLE 발생!

현재 집을 털 때와 털지 않았을 때 값들을 가지고 있으면서 max 값을 업데이트 하는 방식으로 접근하면 된다.

```java
public class Solution {
    public int rob(int[] nums) {
        int rob = 0;    // money when rob current house
        int notRob = 0; // money when not rob current house
        for(int n : nums) {
            int curRob = notRob + n; // when decided to rob current house
            notRob = Math.max(notRob, rob); // get max between robbing before house and not robbing before house
            rob = curRob;
        }
        return Math.max(rob, notRob);
    }
}
```

Time complexity: O(N)

Space complexity: O(1)
