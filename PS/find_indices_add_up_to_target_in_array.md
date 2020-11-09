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


<hr/>

## Following Problem - 1
Given an array of integers, return **indices of the pairs** that add up to a specific target N.

- Array is not ordered
- There can be multiple pairs, or no-pair
- All elements in the array are distinct


### Solution
```java
List<Integer[]> getIndices(int[] arr, final int N) {
  List<Integer[]> pairs = new ArrayList<>();
  Map<Integer, Integer> indexMap = new HashMap<>();
  for(int i = 0; i < arr.length; ++i) {
    indexMap.put(arr[i], i);
  }
  Arrays.sort(arr);

  int lp = 0, rp = arr.length - 1;
  while(lp < rp) {
    int left = arr[lp];
    int right = arr[rp];
    int sum = left + right;
    if (sum == N) {
      pairs.add(new Integer[]{ indexMap.get(left), indexMap.get(right) });
      lp++;
      rp--;
    }
    else if (sum < N) {
      lp++;
    }
    else {
      rp--;
    }
  }

  return pairs;
}
```
Time complexity: O(N * logN)

Space complexity: O(N)

## Following Problem - 2
What if there can be same integer in the array?

indexMap can have multiple index values.

### Solution
```java


```
