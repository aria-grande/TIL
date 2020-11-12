# Problem
https://leetcode.com/problems/unique-binary-search-trees/


# Solution

```java
public int numTrees(int n) {
    if (n < 2) {
        return n;
    }
    int[] nums = new int[n + 1];
    nums[0] = 1;
    nums[1] = 1;
    nums[2] = 2;

    for(int i = 3; i <= n; ++i) {
        int num = 0;
        for(int k = 0; k < i; ++k) {
            num += nums[k]*nums[i - 1 - k];
        }

        nums[i] = num;
    }

    return nums[n];
}
```

Time complexity: O(N)

Space complexity: O(N)
