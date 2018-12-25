
# Problem
https://leetcode.com/problems/largest-number/
```
Given a list of non negative integers, arrange them such that they form the largest number.
```

# Solution
```java
import java.math.*;
class Solution {
    public String largestNumber(int[] nums) {
        Integer[] nums2 = Arrays.stream( nums ).boxed().toArray( Integer[]::new );
        Arrays.sort(nums2, new Comparator<Integer>() {
           public int compare(Integer o1, Integer o2) {
               String s1 = o1.toString();
               String s2 = o2.toString();
               return new BigInteger((s2 + s1)).subtract(new BigInteger(s1 + s2)).intValue();
           } 
        });
        
        StringBuilder sb = new StringBuilder();
        int first = nums2[0];
        for(int n : nums2) {
            if(first == 0) {
                first = n;
                continue;
            }
            sb.append(n);
        }
        return sb.length() == 0 ? "0" : sb.toString();
    }
}
```
