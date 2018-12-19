# Problem
https://leetcode.com/problems/two-sum-iii-data-structure-design/

# Solution

```java
class TwoSum {
    Map<Integer, Integer> nums;
    /** Initialize your data structure here. */
    public TwoSum() {
        nums = new HashMap<>();
    }
    
    /** Add the number to an internal data structure.. */
    public void add(int number) {
        nums.put(number, nums.getOrDefault(number, 0) + 1);
    }
    
    /** Find if there exists any pair of numbers which sum is equal to the value. */
    public boolean find(int value) {
        for(int num : nums.keySet()) {
            if(nums.containsKey(value - num)) {
                if(num * 2 == value && nums.get(num) < 2) {
                    continue;
                } else {
                    return true;
                }
            }
        }
        return false;
    }
}
```
