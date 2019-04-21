# Problem
https://leetcode.com/problems/hamming-distance/description/

# Solution
```java
public int hammingDistance(int x, int y) {
    int xor = x ^ y;
    int len = 0;       
    while(xor >= 1) {
        if(xor % 2== 1) {
            len++;
        }
        xor = xor >> 1;
    }
    return len;
}
```

Time complexity: O(ln max(x, y))

Space complexity: O(1)
