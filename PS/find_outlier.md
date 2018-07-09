# Problem
https://www.codewars.com/kata/find-the-parity-outlier

```
You are given an array (which will have a length of at least 3, but could be very large) containing integers. 
The array is either entirely comprised of odd integers or entirely comprised of even integers except for a single integer N. 
Write a method that takes the array as an argument and returns this "outlier" N.
```


# Solution

한 개만 다른 유형이고, 나머지는 같은 유형(짝수 or 홀수)이므로, array의 첫 3개 values만 보고 outlier가 짝수인지 홀수인지 판단할 수 있다.
1, 2, 3 -> outlier: 짝수  `(1 % 2) + (2 % 2) + (3 % 2) = 2`<br/>
1, 3, 5 -> outlier: 짝수  `(1 % 2) + (3 % 2) + (5 % 2) = 3`<br/>
2, 4, 6 -> outlier: 홀수  `(2 % 2) + (4 % 2) + (6 % 2) = 0`<br/>
2, 4, 5 -> outlier: 홀수  `(2 % 2) + (4 % 2) + (5 % 2) = 1`<br/>

처음 3-value의 sum of mod가 0 혹은 1이라면 outlier는 홀수, 2 혹은 3이라면 outlier는 짝수임을 알 수 있다.

```java
int getOutlier(int[] arr) {
  int sum = Arrays.stream(arr).limit(3)
                     .map(x -> Math.abs(x) % 2)
                     .sum();
  int remainder = (sum <= 1) ? 1 : 0;
  
  for(int num : arr) {
    if(Math.abs(num) % 2 == remainder) {
      return num;
    }
  } 
  return 0;  
}
```
