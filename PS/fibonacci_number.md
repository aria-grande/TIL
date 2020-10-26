# Problem
https://leetcode.com/problems/fibonacci-number/

``` 
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
Given N, calculate F(N).
```

# Solution 1 - simplest solution
```java
public int fib(int N) {
  int fib = 0, next = 1;
  for (int i = 0; i < N; ++i) {
      int tmp = next;
      next += fib;
      fib = tmp;
  }
  return fib;
}
```

No need to memoize every past elements. For an example, to get fib(100), we only need fib(99) and fib(98).

Time complexity: O(N)
Space complexity: O(1)


# Solution 2 - memoization
```java
public int fib(int N) {
    if (N < 2) {
        return N;
    }
    int[] fibs = new int[N + 1];
    fibs[0] = 0;
    fibs[1] = 1;

    for (int i = 2; i <= N; ++i) {
        fibs[i] = fibs[i - 1] + fibs[i -2];
    }
    
    return fibs[N];
}
```
Time complexity: O(N)
Space complexity: O(N)

# Solution 3 - recursion
```java
public int fib(int N) {
  if (N < 2) {
    return N;
  }
  return fib(N - 1) + fib(N - 2);
}
```
Time complexity: O(N)
Space complexity: O(N)

