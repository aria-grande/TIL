# Problem
A non-empty array A consisting of N integers is given. The product of triplet (P, Q, R) equates to A[P] * A[Q] * A[R] (0 ≤ P < Q < R < N).

For example, array A such that:
```
A =[-3, 1, 2, -2, 5, 6]
```
contains the following example triplets:

(0, 1, 2), product is −3 * 1 * 2 = −6
(1, 2, 4), product is 1 * 2 * 5 = 10
(2, 4, 5), product is 2 * 5 * 6 = 60
Your goal is to find the maximal product of any triplet.

Write a function:

class Solution { public int solution(int[] A); }

that, given a non-empty array A, returns the value of the maximal product of any triplet.

For example, given array A such that:
```
A =[-3, 1, 2, -2, 5, 6]
```
the function should return 60, as the product of triplet (2, 4, 5) is maximal.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [3..100,000];
each element of array A is an integer within the range [−1,000..1,000].

# Solution
오름차순 정렬 후, 

배열 A 내에 음수가 없다면 가장 마지막 3 원소의 곱이 max product이다.

하지만 첫 번째와 두 번째 원소가 음수라면, 둘을 곱했을 때 양수가 되므로 마지막 원소(max 값)와 곱해서 max product가 될 수도 있다.

```java
public int solution(int[] A) {
    final int LEN = A.length;
    Arrays.sort(A);

    int productR = A[LEN - 1] * A[LEN - 2] * A[LEN - 3];
    int productL = A[0] * A[1] * A[LEN - 1];
    return Math.max(productR, productL);        
}
```
Time complexity: O(N*logN)

Space complexity: O(1)

# Report
- https://app.codility.com/demo/results/trainingSUWWXK-AZT/
