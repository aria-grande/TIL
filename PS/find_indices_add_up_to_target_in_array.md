# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/546/
```
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
```

# Solution1

```java
public int[] twoSum(int[] nums, int target) {
  for(int i1 = 0; i1 < nums.length; ++i1) {
    int newTarget = target - nums[i1];
    for(int i2 = i1 + 1; i2 < nums.length; ++i2) {
      if(nums[i2] == newTarget) {
        return new int[] {i1, i2};
      }
    }
  }
  return null;
}
```

Time complexity: O(n^2)

Space complexity: O(1)

# Solution2
공간을 써서 시간을 줄여보자.

```java
public int[] twoSum(int[] nums, int target) {
  Map<Integer, Integer> visited = new HashMap<Integer, Integer>();
  for(int i1 = 0; i1 < nums.length; ++i1) {
    int newTarget = target - nums[i1];
    if(visited.containsKey(newTarget)) {
      return new int[] {i1, visited.get(newTarget)};
    }
    visited.put(nums[i1], i1);
  }
  return null;
}
```

Time complexity: O(n)

Space complexity: O(n)
