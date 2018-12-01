# Problem
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. 
```
Example:

Input: n = 10
Output: 12
Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
```
Note:  

1 is typically treated as an ugly number.

n does not exceed 1690.

# Solution
결국 ugly numbers는 2, 3, 5의 조합이다.
Brute-force하게 풀면 정수를 하나씩 증가시켜 가며 그의 factors가 2, 3, 5로만 구성되어있을 경우 출력하는 것인데, n이 1690이 되면 time limit exceeded가 발생한다.

```java
public int nthUglyNumber(int n) {
    int[] uglyNums = new int[n + 1];
    int i2 = 0, i3 = 0, i5 = 0;
    int n2 = 2, n3 = 3, n5 = 5;
    uglyNums[0] = 1;
    for(int i = 1; i < n; i++) {
        int cur = Math.min(Math.min(n2, n3), n5);
        uglyNums[i] = cur;    
        if(cur == n2) {
            n2 = uglyNums[i2++] * 2;
        }
        else if(cur == n3) {
            n3 = uglyNums[i3++] * 3;
        }
        else if(cur == n5) {
            n5 = uglyNums[i5++] * 5;
        }
    }
    return uglyNums[n - 1];
}
```

Time complexity: O(N)

Space complexity: O(N)
