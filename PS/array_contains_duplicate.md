# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/578/
```
Given an array of integers, find if the array contains any duplicates.
```

# Solution 1

```
public boolean containsDuplicate(int[] nums) {
    if(nums == null || nums.length < 2) {
        return false;
    }

    Arrays.sort(nums);
    int prev = nums[0];
    for(int i = 1; i < nums.length; ++i) {
        if(prev == nums[i]) {
            return true;
        }
        prev = nums[i];
    }
    return false;
}
```
Time complexity: O(n log n)

Space complexity: O(1)


# Solution 2
```
public boolean containsDuplicate(int[] nums) {
    if(nums == null || nums.length < 2) {
        return false;
    }
    
    Set<Integer> set = new HashSet<Integer>();
    for(int n : nums) {
      if (set.contains(n)) {
        return true;
      }
      set.add(n);
    }
    return false;
 
}
```
Time complexity: O(n)

Space complexity: O(n)


