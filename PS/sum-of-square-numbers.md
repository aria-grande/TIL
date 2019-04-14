# Problem
https://leetcode.com/problems/sum-of-square-numbers/
```
Given a non-negative integer c, your task is to decide whether there're two integers a and b such that a^2 + b^2 = c.
```

# Solution
```java
import java.lang.Math;

class Solution {
    public boolean judgeSquareSum(int c) {
        for(int a = 1; a <= (int) Math.sqrt(c); ++a) {
            double b = Math.sqrt(c - a * a);
            if((int) b == b) {
                return true;
            }
        }
        return false;
    }
}
```

Time complexity: O(c^(1/2) * log(c)) // log(c) is for finding square root of (c - a^2) in the worst case.

Space complexity: O(1)
