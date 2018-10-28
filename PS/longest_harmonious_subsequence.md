# Problem
https://leetcode.com/problems/longest-harmonious-subsequence/description/
```
We define a harmonious array is an array where the difference between its maximum value and its minimum value is exactly 1.
Now, given an integer array, you need to find the length of its longest harmonious subsequence among all its possible subsequences.
```

# Solution1
- Brute-force way
```java
public int findLHS(int[] nums) {
  int maxLen = 0;
  for(int i = 0; i < nums.length; ++i) {
    int newLen = getLengthWithStandard(nums, i + 1, nums[i]);
    maxLen = Math.max(maxLen, newLen);
  }
  return maxLen;
}

private int getLengthWithStandard(int[] nums, int startIdx, int standard) {
  int plusLen = 1;
  int minusLen = 1;
  boolean plusAppeared = false;
  boolean minusAppeared = false;
  for(int j = startIdx; j < nums.length; ++j) {
    int diff = nums[j] - standard;
    if(diff == 0) {
      plusLen++;
      minusLen++;
    }
    else if(diff == 1) {
      plusAppeared = true;
      plusLen++;
    }
    else if (diff == -1) {
      minusAppeared = true;
      minusLen++;
    }
  }
  plusLen = plusAppeared ? plusLen : 0;
  minusLen = minusAppeared ? minusLen : 0;
  return Math.max(plusLen, minusLen);
}
```

Time complexity: O(N^2)

Space complexity: O(1)

# Solution2(Much Better)
- Using Hashmap!
- Hashmap을 이용하여, 기준값보다 1이 작고 큰 count들을 get해가며 길이를 계산하면 순서를 유지한채(subsequence) 길이를 계산할 수 있다.

```java
public int findLHS(int[] nums) {
    int maxLen = 0;
    Map<Integer, Integer> counts = new HashMap<>();
    for(int num : nums) {
      int newCount = counts.getOrDefault(num, 0) + 1;
      counts.put(num, newCount);
      if(counts.containsKey(num - 1)) {
        maxLen = Math.max(maxLen, newCount + counts.get(num - 1));
      }
      if(counts.containsKey(num + 1)) {
        maxLen = Math.max(maxLen, newCount + counts.get(num + 1));
      }
    }
    return maxLen;
}
```

Time complexity: O(N)

Space complexity: O(N)
