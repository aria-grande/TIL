# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-hard/116/array-and-strings/832/

```
Given an unsorted integer array, find the smallest missing positive integer.
```

# Solution
minimum positive integer이므로 배열의 길이가 N일때, 답은 1~N 사이 혹은 N+1이다.

```java
public int firstMissingPositive(int[] nums) {
    boolean[] mins = new boolean[nums.length];
    for(int n : nums) {
        if(n > 0 && n <= nums.length) {
            mins[n - 1] = true;               
        }
    }
    for(int i = 0; i < mins.length; ++i) {
        if(!mins[i]) {
            return i + 1;
        }            
    }
    return mins.length + 1;
}
```

Time complexity: O(N)
Space complexity: O(N)
