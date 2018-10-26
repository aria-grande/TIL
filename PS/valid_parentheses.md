# Problem
https://leetcode.com/problems/valid-parentheses/description/

```
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.
```

# Solution
```java
class Solution {
    final char SO = '(';
    final char SC = ')';
    final char MO = '{';
    final char MC = '}';
    final char LO = '[';
    final char LC = ']';
    
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for(char c : s.toCharArray()) {
            if(isOpened(c)) {
                stack.push(c);
            }
            else if(isClosed(c)) {
                if(stack.isEmpty()) {
                    return false;
                }
                char poped = stack.pop();
                if(!isMatched(poped, c)) {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
    
    private boolean isOpened(char c) {
        return c == SO || c == MO || c == LO;
    }
    private boolean isClosed(char c) {
        return c == SC || c == MC || c == LC;
    }
    private boolean isMatched(char opened, char closed) {
        return opened == SO && closed == SC || opened == MO && closed == MC || opened == LO && closed == LC;
    }
}
```

Time complexity: O(N)

Spacee complexity: O(N)
