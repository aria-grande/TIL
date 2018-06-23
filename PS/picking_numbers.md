# Problem
https://www.hackerrank.com/challenges/picking-numbers/problem
```
Given an array of integers, find and print the maximum number of integers you can select from the array such 
that the absolute difference between any two of the chosen integers is less than or equal to 1.

ex) a = [6,4,5,3,1,3] -> [3,3,4] -> output: 3
```

# Solution
1. sort array
2. get lengths using start and end pointers(sp, ep)

```java
int pickingNumbers(int[] arr) {
    Arrays.sort(arr);

    int sp = 0;
    int ep = 0;
    int maxLen = 0;
    final int N = arr.length;
    while(sp <= ep && sp < N && ep < N) {
        if(arr[ep] - arr[sp] > 1) {
            ++sp;
        } else {
            maxLen = Math.max(ep - sp + 1, maxLen);
            ++ep;
        }
    }
    return maxLen;
}
```

Time complexity: O(nlogn)<br/>
Space complexity: O(1)
