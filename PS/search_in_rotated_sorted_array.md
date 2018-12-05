# Problem
https://leetcode.com/problems/search-in-rotated-sorted-array/
``` 
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).
``` 

# Solution
```java
public int search(int[] nums, int target) {
    int sp = 0, ep = nums.length - 1;
    while(sp <= ep) {
        int mid = (sp + ep) / 2;
        if(nums[mid] == target) {
            return mid;
        }
        if(nums[sp] == target) {
            return sp;
        }
        if(nums[ep] == target) {
            return ep;
        }
        if(nums[sp] < nums[mid] && nums[mid] > nums[ep]) { // pivot is on right
            if(nums[sp] < target && target < nums[mid]) {
                ep = mid - 1;
            } else {
                sp = mid + 1;
            }
        }
        else {  // pivot is in left
            if(nums[mid] < target && target < nums[ep]) {
                sp = mid + 1;
            } else {
                ep = mid - 1;
            }
        }    
    }
    return -1;
}
```
Time complexity: O(log N)
Space complexity: O(1)
