# Problem
A non-empty array A consisting of N integers is given.

The leader of this array is the value that occurs in more than half of the elements of A.

An equi leader is an index S such that 0 ≤ S < N − 1 and two sequences A[0], A[1], ..., A[S] and A[S + 1], A[S + 2], ..., A[N − 1] have leaders of the same value.

For example, given array A such that:

    A[0] = 4
    A[1] = 3
    A[2] = 4
    A[3] = 4
    A[4] = 4
    A[5] = 2
we can find two equi leaders:

0, because sequences: (4) and (3, 4, 4, 4, 2) have the same leader, whose value is 4.
2, because sequences: (4, 3, 4) and (4, 4, 2) have the same leader, whose value is 4.
The goal is to count the number of equi leaders.

Write a function:

class Solution { public int solution(int[] A); }

that, given a non-empty array A consisting of N integers, returns the number of equi leaders.

For example, given:

    A[0] = 4
    A[1] = 3
    A[2] = 4
    A[3] = 4
    A[4] = 4
    A[5] = 2
the function should return 2, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
each element of array A is an integer within the range [−1,000,000,000..1,000,000,000].

# Solution

```java
final int NO_EXIST = Integer.MIN_VALUE;
public int solution(int[] A) {
    int equiLeadersCount = 0;

    Map<Integer, Integer> counters = new HashMap<>();
    for(int num : A) {
        counters.put(num, counters.getOrDefault(num, 0) + 1);
    }
    Map<Integer, Integer> equiLeftCounters = new HashMap<>();
    // 처음 두 개만 나누고 그 이후로 leader값 각 저장.
    for(int i = 0; i < A.length - 1; ++i) {
        int num = A[i];
        counters.put(num, counters.get(num) - 1);
        equiLeftCounters.put(num, equiLeftCounters.getOrDefault(num, 0) + 1);
        int left = equiLeftCounters.get(num);
        int right = counters.get(num);
        if(isEquiLeader(equiLeftCounters, i + 1, counters, A.length - i - 1)) {
            equiLeadersCount++;
        }
    }
    return equiLeadersCount;
}

private boolean isEquiLeader(Map<Integer, Integer> left, final int LEFT_LEN, Map<Integer, Integer> right, final int RIGHT_LEN) {
    int leftLeader = getLeader(left, LEFT_LEN);
    int rightLeader = getLeader(right, RIGHT_LEN);
    return leftLeader == rightLeader && leftLeader != NO_EXIST;
}

private int getLeader(Map<Integer, Integer> map, final int LEN) {
    final int TARGET_LEN = (LEN % 2 == 0) ? LEN / 2 : (int) Math.ceil((double) LEN / 2) - 1;
    for(int num : map.keySet()) {
        if(map.get(num) > TARGET_LEN) {
            return num;
        }
    }
    return NO_EXIST;
}
```

Time complexity: O(N^2)

Space complexity: O(N)

# Report
- https://app.codility.com/demo/results/training8J3DZJ-NPV/

ㄴ 타임아웃난다. 더 나은 솔루션을 찾아야 ㅠ
