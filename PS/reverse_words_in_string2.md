# Problem
https://leetcode.com/explore/interview/card/amazon/76/array-and-strings/522

https://leetcode.com/problems/reverse-words-in-a-string-ii/

# Solution
```java
class Solution {
    public void reverseWords(char[] str) {
        int sp = 0, ep = str.length - 1;
        while(sp < ep) {
            swap(str, sp++, ep--);
        }
        int p = 0;
        while(p < str.length) {
            int l = p, r = p;
            while(r < str.length && str[r] != ' ') {
                r++;
            }
            p = r + 1;
            r--;
            
            while(l < r) {
                swap(str, l++, r--);
            }
        }
    }
    
    private void swap(char[] str, int p1, int p2) {
        char tmp = str[p1];
        str[p1] = str[p2];
        str[p2] = tmp;
    }
}
```

Runtime: 3ms

Time complexity: O(N)

Space complexity: O(1)
