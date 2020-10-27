# Problem
```
Write a function that takes in an array of integers and returns the length of the longest peak in the array.
A peak is defined as adjacent integers in the array that are strictly increasing until they reach a tip (the highest value in the peak), at which point they become strictly  decreasing. At least three integers are required to form a peak.

For example, the integers 1, 4, 10, 2 form a peak, but the integers 4, 0, 10 don't and neither do the integers 1, 2, 2, 0. Similarly, the integers 1, 2, 3 don't form a peak because there aren't any strictly decreasing integers after the 3.
```

# Solution
```java
public static int longestPeak(int[] array) {
  int maxLength = 0;
  boolean increasing = false, peakPassed = false;
  int sp = -1, ep = -1;

  for (int i = 0; i < array.length - 1; ++i) {
    if (array[i] > array[i + 1]) {
      if (increasing) {
        peakPassed = true;
        increasing = false;
      }

      if (peakPassed) {
        ep = i + 1;
        maxLength = Math.max(maxLength, (ep - sp + 1));
      }
    }
    else if (array[i] < array[i + 1] && !increasing) {
      increasing = true;
      sp = i;
      peakPassed = false;
    }
    else {
      peakPassed = false;
      increasing = false;
    }
  }
  return maxLength;
}
```

Time complexity: O(N), when N is the length of the array

Space complexity: O(1)
