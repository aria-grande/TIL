# Problem
```
연속되는 문자열을 압축하라.

예) 
AAABBCCDDD -> A3B2C2D3
AABAAB -> A2B1A2B1
```

# Solution
```java
String compress(String input) {
  if(input == null || input.isEmpty()) {
    return input;
  }
  
  StringBuilder sb = new StringBuilder();
  char cur = input.charAt(0);
  int cnt = 0;
  for(char c: input.toCharArray()) {
  if (c == cur) {
      cnt++;
    }
    else {
      sb.append(cur);
      sb.append(cnt);
      cur = c;
      cnt = 1;
    }
  }
  sb.append(cur);
  sb.append(cnt);
  
  return sb.toString();
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
