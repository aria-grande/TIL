# Problem

https://leetcode.com/problems/find-smallest-letter-greater-than-target/

# Solution (Linearly)
```java

```
Time complexity: O(N)

Space complexity: O(1)

# Solution (Better)
Let's use binary search since the given array is sorted.
```java
public char nextGreatestLetter(char[] letters, char target) {
    return getNextGreatest(letters, target, 0, letters.length - 1);
}

private char getNextGreatest(char[] letters, char target, int sp, int ep) {
    int mid = (sp + ep) / 2;
    int compared = letters[mid] - target;
    if(sp == ep) {
        return letters[sp] > target ? letters[sp] : letters[0];
    }
    if(compared <= 0) {
        return getNextGreatest(letters, target, mid + 1, ep);
    }
    if(compared > 0) {
        return getNextGreatest(letters, target, sp, mid);
    }
    return letters[0];
}
```
Time complexity: O(log N)

Space complexity: O(1) (O(N) when considers call stack)

# Solution (Much better)
Let's use binary search not recursively.
```java
public char nextGreatestLetter(char[] letters, char target) {
    int sp = 0, ep = letters.length - 1;
    while(sp <= ep) {
        int mid = (sp + ep) / 2;
        if(sp == ep) {
            return letters[sp] > target ? letters[sp] : letters[0];
        }
        if(letters[mid] <= target) {
            sp = mid + 1;
        }
        else {
            ep = mid;
        }
    }
    return letters[0];
}
```
Time complexity: O(log N)

Space complexity: O(1)
