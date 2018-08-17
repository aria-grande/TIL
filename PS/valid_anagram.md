# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/882/
```
Given two strings s and t , write a function to determine if t is an anagram of s.
```

# Solution
```java
boolean isAnagram(String s, String t) {
    int[] count = new int[26];
    for(char a : s.toCharArray()) {
        count[a - 'a']++;
    }
    for(char b : t.toCharArray()) {
        count[b - 'a']--;
    }
    return Arrays.stream(count).filter(x -> x != 0).count() == 0;
}
```

s의 길이를 N, t의 길이를 M이라 할 때,<br/>
Time complexity: O(N + M)<br/>
Space complexity: O(1)
