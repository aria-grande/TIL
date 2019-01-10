# Problem
https://leetcode.com/problems/shortest-word-distance/

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

Example:
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].
```
Input: word1 = “coding”, word2 = “practice”
Output: 3
Input: word1 = "makes", word2 = "coding"
Output: 1
```
Note:
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

# Solution
루프 한 번만에 답을 구할 수 있다. 두 단어는 항상 배열 안에 존재하므로, 
한 번 루프를 돌면서 word1 혹은 word2에 해당하는 index가 나올 때마다 저장하고, distance 계산 및 minimum 업데이트를 해주면 된다.

```java
class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        int min = words.length;
        int i1 = -1, i2 = -1;
        for(int i = 0; i < words.length; ++i) {
            String word = words[i];
            if(word.equals(word1)) {
                i1 = i;
            }
            else if(word.equals(word2)) {
                i2 = i;
            }
            if(i1 != -1 && i2 != -1) {
                min = Math.min(min, Math.abs(i2 - i1));
            }
        }
        return min;
    }
}
```

Time complexity: O(N)

Space complexity: O(1)
