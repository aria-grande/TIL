# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/567/
```
Given an array nums, write a function to move all 0's to the end of it 
while maintaining the relative order of the non-zero elements.
```

# Solution
index pointer를 p1, p2로 둔다. p1은 0을 찾는 역할, p2는 p1보다 크며 0이 아닌 첫번째 원소를 찾는다.
```java
public void moveZeroes(int[] nums) {
    int si = 0;
    for(int i = 0; i < nums.length && si < nums.length; ++i) {
        if(nums[i] != 0) {
            continue;
        }
        for(si = i + 1; si < nums.length; ++si) {
            if(nums[si] != 0) {
                swap(nums, i, si);
                break;
            }
        }
    }
}

private void swap(int[] nums, int i1, int i2) {
    int tmp = nums[i1];
    nums[i1] = nums[i2];
    nums[i2] = tmp;
}
```

Time complexity: O(n)

Space complexity: O(1)
