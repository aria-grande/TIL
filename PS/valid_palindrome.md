# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/883/
```
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.
```

# Solution

```java
public boolean isPalindrome(String s) {
    char[] cs = s.toCharArray();
    final int LEN = cs.length;
    int sp = 0 ;
    int ep = LEN - 1;
    while(sp <= ep) {
        if(!Character.isLetterOrDigit(cs[sp])) {
            ++sp;
        } else if(!Character.isLetterOrDigit(cs[ep])) {
            --ep;
        } else if(Character.toLowerCase(cs[sp]) != Character.toLowerCase(cs[ep])) {
            return false;
        } else {
            sp++;
            ep--;
        }
    }
    return true;
}
```

Time complexity: O(N)

Space complexity: O(N)
