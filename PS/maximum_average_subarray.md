# Problem
```
Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value.
And you need to output the maximum average value.
```
https://leetcode.com/problems/maximum-average-subarray-i/description/

# Solution
```java
public double findMaxAverage(int[] nums, int k) {
    double sum = 0.0;
    for(int i = 0; i < k; ++i) {
        sum += nums[i];
    }
    double maxSum = sum;
    for(int sp = 0; sp < nums.length - k; ++sp) {
        sum += nums[sp + k];
        sum -= nums[sp];
        maxSum = Math.max(sum, maxSum);
    }
    return maxSum / k;
}
````

Time complexity: O(n)

Space complexity: O(1)
