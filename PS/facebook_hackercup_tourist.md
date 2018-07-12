# Problem
https://www.facebook.com/hackercup/problem/1632703893518337/

# Solution
```java
public class Tourist {
    static void whereToVisit(String[] attractions, final int A, final int K, final long V) {
        int sp = (int)((K * (V - 1)) % A);
        int ep = (sp + (K - 1)) % A;

        if(sp <= ep) {
            for(int i = sp; i <= ep; ++i) {
                System.out.print(attractions[i] + " ");
            }
        }
        else {
            for(int idx = 0; idx <= ep; ++idx) {
                System.out.print(attractions[idx] + " ");
            }
            for(int idx2 = sp; idx2 < A; ++idx2) {
                System.out.print(attractions[idx2] + " ");
            }
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        final int TestCases = s.nextInt();
        for(int caseN = 1; caseN <= TestCases; ++caseN) {
            int A = s.nextInt();
            int K = s.nextInt();
            long V = s.nextLong();
            String[] attractions = new String[A];
            for(int i = 0; i < A; ++i) {
                attractions[i] = s.next();
            }

            System.out.print(String.format("Case #%d: ", caseN));
            whereToVisit(attractions, A, K, V);
        }
        s.close();
    }
}
```

Time complexity: O(K)<br/>
Space complexity: O(1)
