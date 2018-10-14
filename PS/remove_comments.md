# Problem
https://leetcode.com/problems/remove-comments/description/
```
Remove the comments from the source code.

The string // denotes a line comment, which represents that it and rest of the characters to the right of it in the same line should be ignored.
The string /* denotes a block comment, which represents that all characters until the next (non-overlapping) occurrence of */ should be ignored.
(Here, occurrences happen in reading order: line by line from left to right.) To be clear, the string /*/ does not yet end the block comment, as the ending would be overlapping the beginning.

The first effective comment takes precedence over others: 
if the string // occurs in a block comment, it is ignored. 
Similarly, if the string /* occurs in a line or block comment, it is also ignored.
If a certain line of code is empty after removing comments, 
you must not output that line: each string in the answer list will be non-empty.
There will be no control characters, single quote, or double quote characters. 
For example, source = "string s = "/* Not a comment. */";" will not be a test case. 
(Also, nothing else such as defines or macros will interfere with the comments.)
It is guaranteed that every open block comment will eventually be closed, 
so /* outside of a line or block comment always starts a new comment.
```

# Solution
주의해야 할 점
1. blockComment가 시작되었다면, 그 중간에 //가 나타나도 무시해야 한다. 즉, "/* // */ab"는 "ab"가 되어야 한다는 것.
2. lineComment가 blockComment보다 먼저 시작되었다면, 그 라인의 끝까지 나타나는 /*는 무시해야 한다. 즉, ["ab // /*", "*/cd"]는 ["ab ", "*/cd"]가 되어야 한다.
3. 매 라인마다 lineCommented는 false여야 한다.
4. blockComment가 시작되었고, 중간에 "*/"가 나타나면 blockComment가 종료된 것이다.

```java
public List<String> removeComments(String[] source) {
  List<String> output = new ArrayList<String>();

  boolean blockCommented = false;
  StringBuilder sb = new StringBuilder();
  for(String line : source) {
    if(!blockCommented) {
        sb = new StringBuilder();    
    }

    char[] chars = line.toCharArray();
    for(int i = 0; i < chars.length; ++i) {
      if(i == chars.length - 1) {
        if (!blockCommented) {
          sb.append(chars[i]);    
        }
      }
      else if(!blockCommented && chars[i] == '/' && chars[i + 1] == '/') {
        break;
      }
      else if(!blockCommented && chars[i] == '/' && chars[i + 1] == '*') {
        blockCommented = true;
        i++;
      }
      else if(blockCommented && chars[i] == '*' && chars[i + 1] == '/') {
        blockCommented = false;
        i++;
      }
      else if(!blockCommented) {
        sb.append(chars[i]);
      }
    }

    String commentRemovedLine = sb.toString();
    if(!blockCommented && commentRemovedLine.length() > 0) {
      output.add(commentRemovedLine);
    }
  }
  return output;
}
```

Time complexity: O(N)

Space complexity: O(N)
