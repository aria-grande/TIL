# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/881
```
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.
```

# Solution

```java
int firstUniqChar(String s) {
    char[] chars = s.toCharArray();
    int[] counts = new int[26];
    for(char c : chars) {
        counts[c - 'a']++;
    }

    for(int i = 0; i < chars.length; ++i) {
        if(counts[chars[i] - 'a'] == 1) {
            return i;
        }
    }
    return -1;
}
```
Time complexity: O(n)

Space complexity: O(1)
