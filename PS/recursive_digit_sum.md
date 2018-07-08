# Problem
https://www.hackerrank.com/challenges/recursive-digit-sum/copy-from/77487942?h_l=playlist&slugs%5B%5D=interview&slugs%5B%5D=interview-preparation-kit&slugs%5B%5D=recursion-backtracking
```
We define super digit of an integer x using the following rules:

Given an integer, we need to find the super digit of the integer.
- If x has only 1 digit, then its super digit is x.
- Otherwise, the super digit of x is equal to the super digit of the sum of the digits of x.

For given string n represents of an integer and k which is the times to concatenate n to make p, 
get the super digit of it.
```

# Solution
```
n = 9875, k = 4인 경우를 생각해보자.
superDigit(9875, 4) = superDigit(9+8+7+5+9+8+7+5+9+8+7+5) = superDigit((9+8+7+5)*4) = superDigit(2*4) = 8
```
이 문제는 결국 n을 k번 반복시키면서 각 자릿수를 summation 하는 것인데,
summation 값이 10보다 커지면 바로 superDigit화를 해서 sum값이 항상 한 자리 수로 유지해야 한다.


```java
int superDigit(String n, int k) {
    int sum = 0;
    for(char c : n.toCharArray()) {
        sum += Character.getNumericValue(c);
        if(sum >= 10) {
            sum = (sum / 10) + (sum % 10);
        }
    }
    sum *= k;
    while(sum >= 10) {
        sum = (sum / 10) + (sum % 10);
    }
    return sum;
}
```

Time complexity: O(N + K)<br/>
Space complexity: O(1)
