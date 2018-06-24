# Problem
https://www.hackerrank.com/challenges/climbing-the-leaderboard/problem

# Solution
1. 주어진 scores에서 중복된 점수를 제거하여 새로운 board를 만들고, index + 1을 rank 순서로 사용한다.
2. board는 descending order이고, alice's scores는 ascending order이므로, board의 끝부터 비교해나가면 된다.
3. 그 다음 alice score의 ranking을 찾을 때는 이전 랭킹의 값을 활용할 수 있다.

```java
int[] climbingLeaderboard(int[] scores, int[] alice) {
    final int BOARD_LEN = scores.length;
    int[] board = new int[BOARD_LEN];
    int borderLastIndex = 0;
    int prev = -1;
    for(int s : scores) {
        if(prev != s) {
            board[borderLastIndex++] = s;
            prev = s;
        }
    }
    
    final int ALICE_LEN = alice.length;
    int[] ranks = new int[ALICE_LEN];
    int startIndex = borderLastIndex - 1;
    for(int i = 0; i < ALICE_LEN; ++i) {
        int rank = getRank(alice[i], startIndex, board);
        ranks[i] = rank + 1;
        sp = rank;
    }
    return ranks;
}

private int getRank(int score, int sp, int[] board) {
    for(int i = sp; i >= 0; --i) {
        if(score == board[i]) {
            return i;
        }
        else if(score < board[i]) {
            return i + 1;
        }
    }
    return 0;
}
```
`scores`의 length를 N, `alice`의 length를 M이라 할 때,<br/>
Time complexity: O(N+M)<br/>
Space complexity: O(N+M)
