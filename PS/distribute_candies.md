# Problem

https://leetcode.com/problems/distribute-candies/

Given an integer array with even length, where different numbers in this array represent different kinds of candies. Each number means one candy of the corresponding kind. You need to distribute these candies equally in number to brother and sister. Return the maximum number of kinds of candies the sister could gain.

# Solution1

```java
class Solution {
    public int distributeCandies(int[] candies) {
        Set<Integer> sisters = new HashSet<>();
        for(int candy : candies) {
            sisters.add(candy);
        }
        return Math.min(candies.length / 2, sisters.size());
    }
}
```
Time complexity: O(N)

Space complexity: O(N)


# Solution 2

```java
class Solution {
    public int distributeCandies(int[] candies) {
        Arrays.sort(candies);
        int max = 0;
        int prev = Integer.MIN_VALUE;
        for(int candy : candies) {
            if(candy != prev) {
                max++;
                prev = candy;
            }
        }
        return Math.min(candies.length / 2, max);
    }
}
```
Time complexity: O(nlogn)

Space complexity: O(1)

# Solution 3

```java
class Solution {
    public int distributeCandies(int[] candies) {
        boolean[] sisters = new boolean[200001];
        int max = 0;
        for(int candy : candies) {
            if(!sisters[candy + 100000]) {
                sisters[candy + 100000] = true;
                max++;
            }
        }
        return Math.min(candies.length / 2, max);
    }
}
```

Time complexity: O(N)

Space complexity: O(1)
