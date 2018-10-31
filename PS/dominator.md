# Problem
An array A consisting of N integers is given. The dominator of array A is the value that occurs in more than half of the elements of A.

For example, consider array A such that
```
 A[0] = 3    A[1] = 4    A[2] =  3
 A[3] = 2    A[4] = 3    A[5] = -1
 A[6] = 3    A[7] = 3
```
The dominator of A is 3 because it occurs in 5 out of 8 elements of A (namely in those with indices 0, 2, 4, 6 and 7) and 5 is more than a half of 8.

Write a function

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers, returns index of any element of array A in which the dominator of A occurs. The function should return −1 if array A does not have a dominator.

For example, given array A such that
```
 A[0] = 3    A[1] = 4    A[2] =  3
 A[3] = 2    A[4] = 3    A[5] = -1
 A[6] = 3    A[7] = 3
```
the function may return 0, 2, 4, 6 or 7, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].
# Solution
- N이 홀수일때와 짝수일 때 **more than half** 의 의미가 달라짐에 유의하자.
```java
public int solution(int[] A) {
    final int LEN = A.length;
    if(A == null || LEN == 0) {
        return -1;
    }
    final int TARGET_LEN = (LEN % 2 == 0) ? LEN / 2 : (int) Math.ceil((double) LEN / 2) - 1;
    Map<Integer, Integer> counter = new HashMap<>();
    for(int i = 0; i < LEN; ++i) {
        int num = A[i];
        counter.put(num, counter.getOrDefault(num, 0) + 1);
        if(counter.get(num) > TARGET_LEN) {
            return i;
        }
    }
    return -1;
}
```

Time complexity: O(N)

Space complexity: O(N)

# Report
- https://app.codility.com/demo/results/training9398RA-EKG/
