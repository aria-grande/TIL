# Problem
https://leetcode.com/problems/find-the-duplicate-number/

# Solution
```java
class Solution {
    public int findDuplicate(int[] nums) {
        int p = 0;
        while(p < nums.length) {
            if(nums[p] == p + 1) {
                p++;
            }
            else {
                int nextP = nums[p] - 1;
                if(nums[nextP] == nextP + 1) {
                    return nextP + 1;
                }
                int tmp = nums[p];
                nums[p] = nums[nextP];
                nums[nextP] = tmp;
            }
        }
        return 0;
    }
}
``` 

Runtime: 1ms

Time complexity: O(N)

Space complexity: O(1)
