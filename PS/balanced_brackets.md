# Problem
https://www.hackerrank.com/challenges/balanced-brackets/problem

# Solution

```java
    static String isBalanced(String s) {
        Stack<Character> stack = new Stack<Character>();
        for(char c : s.toCharArray()) {
            if(c == '(' || c == '{'|| c =='[') {
                stack.push(c);
            } else if (stack.isEmpty()) {
                return "NO";
            } else {
                char poped = stack.pop();
                if(poped == '(' && c != ')' || poped == '{' && c != '}'|| poped =='[' && c != ']' ) {
                    return "NO";
                }
            }
        }
        return stack.isEmpty() ? "YES" : "NO";
    }
```

Time complexity: O(n)<br/>
Space complexity: O(n)
