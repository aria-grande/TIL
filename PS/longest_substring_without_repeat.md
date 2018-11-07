
# Problem
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/
```
Given a string, find the length of the longest substring without repeating characters.
```

# Solution
- 영소문자만 취급하면 안된다. 어떠한 character라도 들어올 수 있다!
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        char[] chars = s.toCharArray();
        int maxLength = 0;
        for(int i = 0; i < chars.length; ++i) {
            maxLength = Math.max(maxLength, getLength(chars, i));
        }
        return maxLength;
    }

    private int getLength(char[] chars, int sp) {
        int len = 0;
        Set<Character> appeared = new HashSet<>();
        for(int i = sp; i < chars.length; ++i) {
            char c = chars[i];
            if(appeared.contains(c)) {
                return len;
            }
            else {
                appeared.add(c);
                len++;
            }
        }
        return len;
    }
}
```
Time complexity: O(N^2)

Space complexity: O(N)

# Solution 2 (Better)
- 출현했던 character와 (길이 계산의 시작 점으로 쓰일)그 다음 index 값을 넣은 Map을 이용해보자!

```java 
class Solution {
    public int lengthOfLongestSubstring(String s) {
        char[] chars = s.toCharArray();
        int maxLen = 0;
        Map<Character, Integer> appearedIndex = new HashMap<>();
        for(int ep = 0, sp = 0; ep < chars.length; ++ep) {
            char ec = chars[ep];
            
            sp = Math.max(sp, appearedIndex.getOrDefault(ec, 0));
            maxLen = Math.max(maxLen, ep - sp + 1);
            appearedIndex.put(ec, ep + 1);
        }
        
        return maxLen;
    }
}
```
Time complexity: O(N)

Space complexity: O(N)
