# PROBLEM
https://leetcode.com/problems/longest-common-prefix/

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

# SOLUTION
```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) {
            return "";
        }
        StringBuilder sb = new StringBuilder();
        final int LEN = getMinLength(strs);
        for(int i = 0; i < LEN; ++i) {
            boolean appeared = true;
            char target = strs[0].charAt(i);
            for(int j = 1; j < strs.length; ++j){
                appeared &= strs[j].charAt(i) == target;
            }
            if(!appeared) {
                break;
            }
            sb.append(target);
        }
        return sb.toString();
    }
    
    private int getMinLength(String[] strs) {
        int len = Integer.MAX_VALUE;
        for(String s : strs){
            len = Math.min(len, s.length());
        }
        return len;
    }
}
```
