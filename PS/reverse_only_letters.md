# Problem
https://leetcode.com/problems/reverse-only-letters
```
Given a string S, return the "reversed" string where all characters that are not a letter stay in the same place, 
and all letters reverse their positions.
```

# Solution
문자열의 처음과 끝에서 시작하는 두 개의 포인터를 두고, 각 포인터가 문자열을 가르킬때에만 swapping을 하면 끝!

```java
class Solution {
    public String reverseOnlyLetters(String S) {
        char[] chars = S.toCharArray();
        int sp = 0, ep = chars.length - 1;
        while(sp < ep) {
            while(sp < ep && !Character.isLetter(chars[sp])) { sp++; }
            while(sp < ep && !Character.isLetter(chars[ep])) { ep--; }
            swap(chars, sp++, ep--);
        }
        return String.valueOf(chars);
    }
    
    private void swap(char[] chars, int i, int j) {
        char tmp = chars[i];
        chars[i] = chars[j];
        chars[j] = tmp;
    }
}
```
Time complexity: O(N)

Space complexity: O(N)

**Runtime: 4 ms, faster than 99.33% of Java online submissions for Reverse Only Letters.**


