# Problem
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

# Solution

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue maxHeap = new PriorityQueue<Integer>((o1, o2) -> o1 - o2);  
    for(int num : nums) {
        maxHeap.add(num);
        if(maxHeap.size() > k) {
            maxHeap.poll();
        }
    }
    return (int) maxHeap.poll();
}
```
Suppose N is the length of nums,

Time complexity: O(Nlogk)

Space complexity: O(k)

https://leetcode.com/submissions/detail/206248191/
