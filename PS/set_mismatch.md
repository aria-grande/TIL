# Problem
https://leetcode.com/problems/set-mismatch/
```
The set S originally contains numbers from 1 to n. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array nums representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

Example 1:
Input: nums = [1,2,2,4]
Output: [2,3]

Note:
The given array size will in the range [2, 10000].
The given array's numbers won't have any order.
```

# Solution
```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        final int N = nums.length;
        boolean[] found = new boolean[N];
        int duplicated = 0;
        int sum = 0;
        for(int num : nums) {
            if(found[num - 1]) {
                duplicated = num;
            }
            found[num - 1] = true;
            sum += num;
        }
        int loss = N*(N+1)/2 - sum + duplicated;
        return new int[]{ duplicated, loss };
    }
}
```

Time complexity: O(N)

Space complexity: O(N)
