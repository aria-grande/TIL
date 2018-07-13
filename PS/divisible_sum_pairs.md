# Problem
https://www.hackerrank.com/challenges/divisible-sum-pairs/problem?h_r=internal-search

# Solution
```java
int divisibleSumPairs(int n, int k, int[] arr) {
  int cnt = 0;
  for(int i = 0; i < n - 1; ++i) {
    for(int j = i + 1; j < n; ++j) {
      if((arr[i] + arr[j]) % k == 0) {
        cnt++;
      }
    }
  }
  return cnt;
}
```

Time complexity: O(n^2)<br/>
Space complexity: O(1)
