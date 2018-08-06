# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/559/

```
Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
You may assume the integer does not contain any leading zero, except the number 0 itself.
```

# Solution

```java
 public int[] plusOne(int[] digits) {
    final int LAST = digits.length - 1;

    digits[LAST] += 1;
    for(int i = LAST; i >= 1; --i) {
      int digit = digits[i];
      if(digit >= 10) {
        digits[i - 1] += 1;
        digits[i] = digit - 10;
      }
    }

    if(digits[0] < 10) {
      return digits;
    }

    int[] newDigits = new int[digits.length + 1];
    newDigits[0] = 1;
    newDigits[1] = digits[0] - 10;
    for(int i = 2; i < newDigits.length; ++i) {
      newDigits[i] = digits[i - 1];
    }
    return newDigits;
}
```

Time complexity: O(n)

Space complexity: O(n)
