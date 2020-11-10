# Problem
https://leetcode.com/problems/permutation-in-string/

# Solution
```java
public boolean checkInclusion(String s1, String s2) {
  final int s1Size = s1.length();
  final int s2Size = s2.length();

  if (s1Size > s2Size) {
      return false;
  }

  char[] s1Chars = s1.toCharArray();
  char[] s2Chars = s2.toCharArray();

  int[] s1Count = new int[26];
  int[] s2SubCount = new int[26];
  for (int i = 0; i < s1Size; ++i) {
      s1Count[a - 'a']++;
      s2SubCount[s2Chars[i] - 'a']++;
  }

  for (int i = 0; i < s2Size - s1Size; ++i) {
      if (equals(s1Count, s2SubCount)) {
          return true;
      }
      s2SubCount[s2Chars[i] - 'a']--;
      s2SubCount[s2Chars[i + s1Size] - 'a']++;
  }
  return equals(s1Count, s2SubCount);
}

private boolean equals(int[] arr1, int[] arr2) {
  for (int i = 0; i < arr1.length; ++i) {
      if (arr1[i] != arr2[i]) {
          return false;
      }
  }
  return true;
}
```

Time complexity: O(26 * s2Size + s1Size)

Space complexity: O(s1Size + s2Size)
