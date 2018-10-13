# Problem
https://leetcode.com/problems/strobogrammatic-number/
```
A strobogrammatic number is a number that looks the same when rotated 180 degrees (looked at upside down).

Write a function to determine if a number is strobogrammatic. The number is represented as a string.

Example 1:
Input:  "69"
Output: true

Example 2:
Input:  "88"
Output: true

Example 3:
Input:  "962"
Output: false
```

# Solution
180도 돌렸을 때, 6은 9가 되고, 9는 6이 된다. 1은 1이되며, 8과 0도 자기 자신이 된다.
2, 3, 4, 6, 7이 포함되어 있다면 input string은 절대 strobogrammatic number가 될 수 없다.
180도 돌렸을 때와 0도일 때 같으려면 input string의 절반을 잘라 앞/뒤에서부터 비교해 나가야 한다.
앞/뒤 원소의 각 pair가 strobogrammatic number가 될 수 있는지 판별하면 된다.

```java
Map<Integer, Integer> map = new HashMap<Integer, Integer>() {
  {
    put(0, 0);
    put(1, 1);
    put(6, 9);
    put(8, 8);
    put(9, 6);
  }
};
public boolean isStrobogrammatic(String num) {
  char[] nums = num.toCharArray();
  for(int sp = 0, ep = nums.length - 1; sp <= ep; ++sp, --ep) {
    int sn = Character.getNumericValue(nums[sp]);
    int en = Character.getNumericValue(nums[ep]);
    if(!map.containsKey(sn) || map.get(sn) != en) {
      return false;
    }
  }
  return true;
}
```

Time complexity: O(N)

Space complexity: O(N)
