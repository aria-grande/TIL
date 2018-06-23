# Problem
https://www.hackerrank.com/challenges/birthday-cake-candles/problem

# Solution
max 값의 count를 리턴하면 되는 간단한 문제.

```java
int birthdayCakeCandles(int[] ar) {
    int max = 0;
    int cnt = 0;
    for(int e : ar) {
        if (e == max) {
            cnt++;
        }
        else if (e > max) {
            max = e;
            cnt = 1;
        }
    }
    return cnt;
}
```

Time complexity: O(n)<br/>
Space complexity: O(1)
