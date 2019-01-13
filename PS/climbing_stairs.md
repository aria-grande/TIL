# Problem
https://leetcode.com/problems/climbing-stairs/

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

# Solution1
자세히 생각해보면 이것은 피보나치와 똑같다. n 개의 계단을 올라가기 위한 방법은 (1 계단 올라가고 n - 1 개를 올라가기 위한 방법) + (2계단 올라가고 n - 2 개를 올라가기 위한 방법) 으로

`ways(n) = ways(n - 1) + ways(n - 2) (n > 2)` 이다.

```java
public int climbStairs(int n) {
    if(n <= 2) {
        return n;
    }
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```

Time complexity: O(2^N)

Space complexity: O(N)

# Solution 2
이를 memoization 해서 풀 수도 있겠다.

```java
public int climbStairs(int n) {
    if(n <= 2) {
        return n;
    }
    int[] ways = new int[n];
    ways[0] = 1;
    ways[1] = 2;
    for(int i = 2; i < n; ++i) {
        ways[i] = ways[i - 1] + ways[i - 2];
    }
    return ways[n - 1];
}
```

Time complexity: O(N)

Space complexity: O(N)

# Solution 3
결국 원하는 것은 ways(n) 값만 알면 되므로, ways(1) 부터 ways(n)까지 전부를 memo할 필요는 없고, 가장 last 두 개만 기억하고 있 된다.

```java
public int climbStairs(int n) {
    if(n <= 2) {
        return n;
    }
    int first = 1;
    int second = 2;
    int result = first + second;
    for(int i = 3; i < n; ++i) {
        first = second;
        second = result;
        result = first + second;
    }
    return result;
}
```

Time complexity: O(N)

Space complexity: O(1)
