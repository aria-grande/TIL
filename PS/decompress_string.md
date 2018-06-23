# Problem
```
For a given string consists of `count[compressed string]`, return decompressed string.

For example,
'2[abc]' -> 'abcabc'
'abc' -> 'abc'
'ab2[c]d2[e]' -> 'abccdee'
```

# Solution
문자가 숫자로 시작하면, [] 내의 부분을 n번 append한다.

```java
String decompress(char[] compressed, int sp, int ep) {
  StringBuilder sb = new StringBuilder();
  
  for(int i = sp; i <= ep; ++i) {
    char c = compressed[i];
    if(Character.isDigit(c)) {
      int n = Character.getNumericValue(c);
      int newEp = getClosedParenthesis(compressed, i + 1, ep);
      String decompressed = decompress(compressed, i + 2, newEp);
      for(int j = 0; j < n; ++j) {
        sb.append(decompressed);
      }
      i = newEp;
    }
    else if('a' <= c && c <= 'z') {
      sb.append(c);
    }
  }
  return sb.toString();
}

int getClosedParenthesis(char[] str, int sp, int ep) {
  int cnt = 0;
  for(int i = sp; i <= ep; ++i) {
    if(str[i] == '[') {
      cnt++;
    }
    if(str[i] == ']') {
      cnt--;
      if(cnt == 0) {
        return i;
      }
    }
  }
  return -1;
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
