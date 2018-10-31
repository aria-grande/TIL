# Problem
An array A consisting of N integers is given. A triplet (P, Q, R) is triangular if 0 ≤ P < Q < R < N and:

```
A[P] + A[Q] > A[R],
A[Q] + A[R] > A[P],  
A[R] + A[P] > A[Q].
```
For example, consider array A such that:
```
[10, 2, 5, 1, 8, 20]
```
Triplet (0, 2, 4) is triangular.

Write a function:

`class Solution { public int solution(int[] A); }`

that, given an array A consisting of N integers, returns 1 if there exists a triangular triplet for this array and returns 0 otherwise.

For example, given array A such that:
```
A[0] = 10    A[1] = 2    A[2] = 5
A[3] = 1     A[4] = 8    A[5] = 20
```
the function should return 1, as explained above. Given array A such that:

```
A[0] = 10    A[1] = 2    A[2] = 5
A[3] = 1     A[4] = 8    A[5] = 20
```
the function should return 0.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];

each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

# Solution
```java
public int solution(int[] A) {
    if(A == null || A.length < 3) {
        return 0;
    }
    boolean found = false;
    int pi = 0;
    int qi = 1;
    int ri = 2;
    while(ri < A.length) {
        long P = A[pi];
        long Q = A[qi];
        long R = A[ri];

        if(P + Q <= R) {
            if(P < Q) {
                pi++;
                if(pi == qi) {
                    qi++;
                }
                if(qi == ri) {
                    ri++;
                }
            } else {
                qi++;
                if(qi == ri) {
                    ri++;
                }
            }                 
        } else if (Q + R <= P) {
            if(Q < R) {
                qi++;
                if(qi == ri) {
                    ri++;
                }
            } else {
                ri++;
            }
        } else if (R + P <= Q) {
            if(R < P) {
                ri++;
            } else {
                pi++;
                if(pi == qi) {
                    qi++;
                }
                if (qi == ri) {
                    ri++;
                }
            }
        } else {
            found = true;
            break;
        }
    }
    return found ? 1 : 0;
}
```
Time complexity: O(N*logN)

Space complexity: O(1)

# Solution(Smarter)
- 조건을 다시 생각해보자.
- key point: 0 <= P < Q < R < N 은 신경 쓰지 않아도 될 조건이다.
- 주어진 조건이 삼각형을 만드는 조건이기 때문이다.
- 추후 정리하자

# Report
https://app.codility.com/demo/results/trainingNP4ZJW-PAK/
