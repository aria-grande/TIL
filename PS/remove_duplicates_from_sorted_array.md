# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/727

# Solution

```java
public int removeDuplicates(int[] nums) {
    if(nums.length < 2) {
        return nums.length;
    }
    boolean duplicationFound = false;
    for(int i = 0; i < nums.length - 1; ++i) {
        if(nums[i] == nums[i + 1]) {
            duplicationFound = true;
        }
    }
    if(!duplicationFound) {
        return nums.length;
    }


    int li = 0;
    int pi = 0;
    for(int ci = 1; ci < nums.length; ++ci) {
        int prev = nums[pi];
        int cur = nums[ci];
        int last = nums[li];
        // System.out.println("prev=" + prev +"("+pi+"),cur = " + cur+ "("+ci+"), last = " + last+"("+li+")");
        if(prev != cur && pi != ci && pi != li && cur > last) {
            int tmp = nums[pi];
            nums[pi] = nums[ci];
            nums[ci] = tmp;
            pi++;
            li++;
        }
        else if(prev > last) {
            pi++;
            li++;
        }
        else if(pi == li || prev == last) {
            if(pi == li && prev == last && prev != cur) {
                li++;
            }
            pi++;
        }
    }

    return li + 1;
}
```

Time complexity: O(n)

Space complexity: O(1)
