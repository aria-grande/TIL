# Problem
https://www.hackerrank.com/challenges/kangaroo/problem

# Solution
방정식 문제이다. 

캥거루1의 start point가 x1이고 점프 속력은 v1, 캥거루 2의 start point가 x2, 점프 속력을 v2라고 하자.<br/>
n번 점프 했을 때 만난 다는 가정 하에, 방정식은 아래와 같다.<br/>
```
v1 * n + x1 = v2 * n + x2
(v1 - v2) * n = (x2 - x1)
n = (x2 - x1) / (v1 - v2)
```

v1와 v2가 같은 경우 non division by zero exception이 발생할 수 있거니와, v1 == v2 이고, x1 != x2 라면, 무조건 만날 수 없으므로 바로 리턴해주자.<br/>
n이 0 이상의 정수일 경우 만날 수 있다고 표현 할 수 있다.


```java
boolean canWeMeet(int x1, int v1, int x2, int v2) {
  int startPositionDiff = x2 - x1;
  int speedDiff = v1 - v2;
  if(speedDiff == 0 && startPositionDiff != 0) {
    return false;
  }
  return (startPositionDiff % speedDiff == 0) && (startPositionDiff / speedDiff >= 0);
}
```

Time complexity: O(1)<br/>
Space complexity: O(1)
