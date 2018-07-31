# Problem
https://www.facebook.com/hackercup/problem/180494849326631/

# Solution
시작과 끝의 파이프 유형은 1개만 허용 되며, column 단위로 쪼개보면 문제의 키가 보인다.<br/>
blocking 되어 있는 셀의 경우의 수를 따져 각 컬럼에 대해 끝까지 도달하기 위한 방법의 가짓 수를 곱해나가면 된다.
```java
import java.util.Arrays;
import java.util.List;
import java.util.Scanner;

public class LetItFlow {

    private static final String BLOCKED = "#";
    private static final List<String> IMPOSSIBLES = Arrays.asList(".#.", "##.", "#.#", ".##", "###");
    private static final List<String> ONLY_ONE_WAY = Arrays.asList("#..", "..#");

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        final int T = s.nextInt();
        for(int t = 1; t <= T; ++t) {
            final int N = s.nextInt();
            String[][] pipe = new String[3][N];
            for(int r = 0; r < pipe.length; ++r) {
                pipe[r] = s.next().split("");
            }

            System.out.println(String.format("Case #%d: %d", t, getNumberOfPipeInstalled(pipe, N)));
        }
        s.close();
    }

    private static int getNumberOfPipeInstalled(String[][] pipe, final int N) {
        String startEndPoint = pipe[0][0] + pipe[1][0] + pipe[1][N - 1] + pipe[2][N - 1];
        if(N % 2 == 1 || startEndPoint.contains(BLOCKED)) {
            return 0;
        }

        final int MOD = 1000000007;
        int result = 1;
        for(int col = 1; col < N - 1; col += 2) {
            String v1 = getVertical(pipe, col);
            String v2 = getVertical(pipe, col + 1);

            int num1 = getNumberOfVertical(v1);
            int num2 = getNumberOfVertical(v2);
            int ways = num1 * num2;
            if(ways == 0 || (ways == 1 && !v1.equals(v2))) { /* 실수했던 포인트 참고 */
                return 0;
            }
            else if(ways == 4) {
                result = (result * 2) % MOD;
            }
        }
        return result % MOD;
    }

    private static String getVertical(String[][] pipe, int col) {
        return String.format("%s%s%s", pipe[0][col], pipe[1][col], pipe[2][col]);
    }

    private static int getNumberOfVertical(String vertical) {
        if(IMPOSSIBLES.contains(vertical)) {
            return 0;
        }
        if (ONLY_ONE_WAY.contains(vertical)) {
            return 1;
        }
        return 2;
    }
}
```

Time complexity: O(T*N)<br/>
Space complexity: O(T*N)

## 실수했던 포인트
col = 0, col = N - 1을 제외하고 iterate를 할 때,<br/>
```
(Case 1)   (Case 2)
  . .        # .
  . .        . .
  # #        . #
두 경우 모두, num1 = 1, num 2 = 2
```
**(ways = num1 * num2) == 1이면 무조건 0을 리턴하도록 했는데 Case1과 Case2를 구분해야 한다.**<br/>
Case1은 가짓수가 1이고, Case2는 더이상 진전할 수 없으므로 0을 리턴해야 하기 때문이다.<br/>
