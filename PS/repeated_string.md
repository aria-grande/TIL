# Problem
https://www.hackerrank.com/challenges/repeated-string/problem

```
Lilah has a string, s, of lowercase English letters that she repeated infinitely many times.

Given an integer, n, find and print the number of letter a's in the first n letters of Lilah's infinite string.
```

# Solution

```java
long repeatedString(String s, long n) {
    char[] chars = s.toCharArray();
    int aCount = getACount(chars, chars.length);
    int subACount = getACount(chars, (int) (n % chars.length));

    return aCount * (n / chars.length) + subACount;
}

private int getACount(char[] chars, int until) {
    int cnt = 0;
    for(int i = 0; i < until; ++i) {
        if(chars[i] == 'a') {
            cnt++;
        }
    }
    return cnt;
}
```

Time complexity: O(len(s))<br/>
Space complexity: O(len(s))
