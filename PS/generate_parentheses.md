# Problem
https://leetcode.com/problems/generate-parentheses/description/

```
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

# Solution
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> combinations = new ArrayList<String>();
        generate(combinations, "(", n, 1, 0);
        
        return combinations;
    }
    
    private void generate(List<String> combinations, String str, final int maxCount, int openCount, int closeCount) {
        if(openCount > maxCount || closeCount > maxCount || closeCount > openCount) {
            return ;
        }
        if(closeCount == maxCount) {
            combinations.add(str);
            return ;
        }
        if(openCount < maxCount) {
            generate(combinations, str + "(", n, openCount + 1, closeCount);
        }
        if(closeCount < maxCount) {
            generate(combinations, str + ")", n, openCount, closeCount + 1);
        }
    }
}
```

시간복잡도와 공간복잡도는 어떻게 될까요?
