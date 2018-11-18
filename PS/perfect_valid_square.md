# Problem
https://leetcode.com/problems/valid-perfect-square/
```
Given a positive integer num, 
write a function which returns True if num is a perfect square else False.
```

# Solution(Brute-force)
```java 
public boolean isPerfectSquare(int num) {
    if(num == 1) {
        return true;
    }
    for(int i = 1; i <= num / 2; ++i) {
        if(i * i == num) {
            return true;
        }
    }
    return false;
}
``` 
Time complexity: O(N)

Space complexity: O(1)

# Solution(Better)
[Newton's method](https://en.wikipedia.org/wiki/Newton%27s_method)를 참고하면 해결의 실마리가 보인다.
```java
 public boolean isPerfectSquare(int num) {
    if(num == 1) {
        return true;
    }
    long l = num / 2;
    while(l * l > num) {
        l = (l + num / l) / 2;
    }
    return l * l == num;
}
```
Time complexity: O(log N)~O(1)

Space complexity: O(1)
