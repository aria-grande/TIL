# Problem
https://www.facebook.com/hackercup/problem/175329729852444/

# Solution

```java
public class Interception {
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        final int TestCases = s.nextInt();
        for(int caseN = 1; caseN <= TestCases; ++caseN) {
            int N = s.nextInt();
            for(int i = 0; i <= N; ++i) {
                s.nextInt();
            }
            int result = (N % 2 == 0) ? 0 : 1;
            System.out.println(String.format("Case #%d: %d", caseN, result));
            if(result == 1) {
                System.out.println("0.0");
            }

        }
        s.close();
    }
}
```

Time complexity: O(1)<br/>
Space complexity: O(1)
