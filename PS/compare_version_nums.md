# Problem
https://leetcode.com/problems/compare-version-numbers/

# Solution
```java
class Solution {
    public int compareVersion(String version1, String version2) {
        int n1 = 0, n2 = 0;
        String[] c1 = version1.split("\\.");
        String[] c2 = version2.split("\\.");
        for(String c0 : c1) {
            n1 = n1 * 10 + Integer.parseInt(c0);
        }
        for(String c : c2) {
            n2 = n2 * 10 + Integer.parseInt(c);
        }
        int diff = c1.length - c2.length;
        if(diff > 0){
            n2 *= Math.pow(10, diff);
        }
        else if(diff < 0){
            n1 *= Math.pow(10, -diff);
        }
        if(n1 == n2) {
            return 0;
        }
        return n1 > n2 ? 1 : -1;
    }
}
```
