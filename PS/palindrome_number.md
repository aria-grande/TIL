# Problem
https://leetcode.com/problems/palindrome-number/

# Solution
string에 담아 문자열의 시작과 끝의 양 포인터를 이용하여 palindrome인지 판단하는 방법.
```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) {
            return false;
        }
        char[] num = String.valueOf(x).toCharArray();
        int sp = 0, ep = num.length - 1;
        while(sp < ep) {
            if(num[sp] != num[ep]) {
                return false;
            }
            sp++;
            ep--;
        }
        return true;
    }
}
```
Time complexity: O(N)

Space complexity: O(N)

로직 개선할 것이 보인다. 내일 계속.
