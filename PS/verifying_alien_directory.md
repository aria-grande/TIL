# Problem
https://leetcode.com/problems/verifying-an-alien-dictionary/

# Solution

```java
public boolean isAlienSorted(String[] words, String order) {
    int[] alphabetNums = new int[26];

    int i = 1;
    for(char alphabet : order.toCharArray()) {
        alphabetNums[alphabet - 'a'] = i++;
    }

    double prevWordNum = 0;
    for (String word : words) {
        double base = Math.pow(26, 20);
        double wordNum = 0;
        for (char alphabet : word.toCharArray()) {
            int num = alphabetNums[alphabet - 'a'];
            wordNum += num * base;
            base /= 26;
        }
        if (prevWordNum > wordNum) {
            return false;
        }
        prevWordNum = wordNum;
    }

    return true;
}
```

Time complexity: O(length of words * length of word)

Space complexity: O(1)
