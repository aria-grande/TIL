# Problem
https://leetcode.com/problems/interleaving-string/
```
Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.
``` 

# Solution
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        char[] c1 = s1.toCharArray();
        char[] c2 = s2.toCharArray();
        char[] c3 = s3.toCharArray();
        if(c1.length + c2.length != c3.length) {
            return false;
        }
        
        return possible(c1, c2, c3, 0, 0, 0);
    }
    
    private boolean possible(char[] c1, char[] c2, char[] c3, int p1, int p2, int p3) {
        if(p1 == c1.length && p2 == c2.length && p3 == c3.length) {
            return true;
        }
        boolean result = false;
        if(p1 < c1.length && c1[p1] == c3[p3]) {
            result = result || possible(c1, c2, c3, p1 + 1, p2, p3 + 1);
        }
        if(p2 < c2.length && c2[p2] == c3[p3]) {
            result = result || possible(c1, c2, c3, p1, p2 + 1, p3 + 1);
        }
        return result;
    }
}
```
N, M, K를 각각 s1, s2, s3의 길이라고 할 때,

Time complexity: O(N+M+K)

Space complexity: O(N+M+K)
