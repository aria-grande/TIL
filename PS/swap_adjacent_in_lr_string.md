# Problem
https://leetcode.com/problems/swap-adjacent-in-lr-string/
```
In a string composed of 'L', 'R', and 'X' characters, like "RXXLRXRXL", 
a move consists of either replacing one occurrence of "XL" with "LX", 
or replacing one occurrence of "RX" with "XR". 

Given the starting string start and the ending string end, 
return True if and only if there exists a sequence of moves to transform one string to the other.
```

# Solution
"XL" -> "LX", "RX" -> "XR"의 패턴을 곰곰이 생각해보면, L은 왼쪽으로 움직일 수 있고, R은 오른쪽으로 움직일 수 있다는 것을 알 수 있다.
start, end를 각각 순회하면서 "X"가 나오면 무시하고 L이 찾아지는 포인트와 R이 찾아지는 포인트를 비교함으로써 이 문제를 쉽게 풀 수 있다

```java
public boolean canTransform(String start, String end) {
  char[] starts = start.toCharArray();
  char[] ends = end.toCharArray();
  final int LEN = starts.length;
  
  int sp = 0, ep = 0;
  while(sp < LEN && ep < LEN) {
    while(sp < LEN && starts[sp] == 'X') {
      sp++;
    }
    while(ep < LEN && ends[ep] == 'X') {
      ep++;
    }
    if(sp == LEN || ep == LEN) {
      return sp == ep;
    }
    char sc = starts[sp];
    if(sc != ends[ep] || (sc == 'L' && sp < ep) || (sc == 'R' && sp > ep)) {
      return false;
    }
    sp++;
    ep++;
  }
  return true;
}
```

Time complexity: O(N)

Space complexity: O(N)
