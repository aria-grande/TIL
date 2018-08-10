# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/674/
```
Given two arrays, write a function to compute their intersection.

Example:
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].

Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.

Follow up:
- What if the given array is already sorted? How would you optimize your algorithm?
- What if nums1's size is small compared to nums2's size? Which algorithm is better?
- What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
```

# Solution
```java
public int[] intersect(int[] nums1, int[] nums2) {
    List<Integer> l = new ArrayList<Integer>();
    Map<Integer, Integer> m = new HashMap<Integer, Integer>();

    for(int n1 : nums1) {
        m.put(n1, m.getOrDefault(n1, 0) + 1);
    }
    for(int n2 : nums2) {
        if(m.containsKey(n2) && m.get(n2) > 0) {
            l.add(n2);
            m.put(n2, m.get(n2) - 1);
        }
    }
    int[] intersect = new int[l.size()];
    int i = 0;
    for(int e : l) {
        intersect[i++] = e;
    }
    return intersect;
}
```
nums1의 길이를 N, nums2의 길이를 M이라 할 때,

Time complexity: O(N+M)

Space complexity: O(N+M)
