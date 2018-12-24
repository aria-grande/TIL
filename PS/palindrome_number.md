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

# Better solution
reversed number를 만들면 쉽게 비교할 수 있다.

```java
class Solution {
    public boolean isPalindrome(int x) {
        if(x < 0) {
            return false;
        }
        int origin = x;
        int reversed = 0;
        while(x > 0) {
            reversed *= 10;
            reversed += x % 10;
            x /= 10;
        }
        
        return origin == reversed;
    }
}
```
Time complexity : O(log 10 N)

Space complexity : O(1)
