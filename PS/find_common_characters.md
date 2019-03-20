# Problem
https://leetcode.com/problems/find-common-characters/
```
Given an array A of strings made only from lowercase letters, return a list of all characters that show up in all strings within the list (including duplicates).  For example, if a character occurs 3 times in all strings but not 4 times, you need to include that character three times in the final answer.

You may return the answer in any order.
```

# Solution

```java
public List<String> commonChars(String[] A) {
    int[] counts = new int[26];
    Arrays.fill(counts, Integer.MAX_VALUE);

    for(String str : A) {
        int[] sc = new int[26];
        for(char c : str.toCharArray()) {
            sc[c - 'a']++;
        }
        for(int i = 0; i < 26; ++i) {
            counts[i] = Math.min(counts[i], sc[i]);
        }
    }

    List<String> common = new ArrayList<>();
    for(int i = 0; i < 26; ++i) {
        while(--counts[i] >= 0) {
            common.add(String.valueOf((char)('a' + i)));
        }    
    }
    return common;
}
```

When the size of words is N and the length of each word is M,

TIME COMPLEXITY: O(N*M)

SPACE COPMLEXITY: O(N)
