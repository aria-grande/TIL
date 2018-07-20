# Problem

https://www.hackerrank.com/challenges/circular-array-rotation/problem

# Solution
index 문제다.

```java
int[] circularArrayRotation(int[] a, final int K, int[] queries) {
    final int A = a.length;
    int[] result = new int[queries.length];
    for(int i = 0; i < queries.length; ++i) {
        int idx = (queries[i] - K) % A;
        if (idx < 0) {
            result[i] = a[A + idx];
        } else {
            result[i] = a[idx];
        }
    }
    return result;
}
```

쿼리의 갯수를 N개라 할 때,<br/>
Time complexity: O(N)<br/>
Space complexity: O(N)<br/>
