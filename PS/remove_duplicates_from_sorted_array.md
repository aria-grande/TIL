# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/727

# Solution
`ci`: current index. nums를 iterate하는 index pointer다.

`pi`: prev index. return 값을 의미하며, `nums[0]~nums[prev - 1]`까지는 sorted array without duplication이 된다.

pi가 오른쪽으로 움직이는(`pi++`) 경우
- 맨 처음일 때, sorted이므로 맨 처음은 무조건 유효한 값이라고 판단
- prev_prev < prev 일 때, sorted이므로 유효한 값이라고 판단
- swapping 되거나(swapping은 prev_prev도 current 보다 작고, prev도 current보다 작을 경우)


```java
public int removeDuplicates(int[] nums) {
        boolean duplicationFound = false;
        for(int i = 0; i < nums.length - 1; ++i) {
            if(nums[i] == nums[i + 1]) {
                duplicationFound = true;
                break;
            }
        }
        if(!duplicationFound) {
            return nums.length;
        }
        
        int pi = 0;
        for(int ci = 1; ci < nums.length; ++ci) {
            int prev_prev = nusm[pi - 1];
            int prev = nums[pi];
            int cur = nums[ci];
            if(pi == 0 || prev_prev < prev) {
                pi++;
            }
            else if(prev < cur && prev_prev < cur) {
                nums[pi] = cur;
                nums[ci] = prev;
                pi++;
            }
        }
        return pi;
}
```

Time complexity: O(n)

Space complexity: O(1)
