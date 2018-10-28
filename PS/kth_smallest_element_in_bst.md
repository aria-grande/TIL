# Problem
https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/
```
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note: 
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.
```

# Solution1
BST를 순회하며 minHeap에 넣은 후, k 번째에 있는 원소를 리턴하자!
```java
public int kthSmallest(TreeNode root, int k) {
  Queue<Integer> minHeap = new PriorityQueue<Integer>();
  convertToMinHeap(root, minHeap);
  for(int i = 0; i < k - 1; ++i) {
      minHeap.poll();
  }
  return minHeap.poll();
}

private void convertToMinHeap(TreeNode node, Queue<Integer> minHeap) {
  if(node != null) {
    minHeap.add(node.val);
    convertToMinHeap(node.left, minHeap);
    convertToMinHeap(node.right, minHeap);
  }
}
```
- Time complexity: O(N*logN)
- Space complexity: O(N)

# Solution2 (Better)
주어진 자료구조가 BST인 이유를 생각해보자. BST하면 어떤게 떠오를까? pre-order, in-order, post-order traverse가 떠오른다.

in-order traverse를 하면서 k 번째에 있는 원소를 리턴하면 되지 않을까?
```java
public int kthSmallest(TreeNode root, int k) {
  List<Integer> inOrdered = new ArrayList<Integer>();
  traverseInOrder(root, inOrdered);
  return inOrdered.get(k - 1);
}

private void traverseInOrder(TreeNode node, List<Integer> inOrdered) {
  if(node == null) {
    return;
  }
  traverseInOrder(node.left, inOrdered);
  inOrdered.add(node.val);
  traverseInOrder(node.right, inOrdered);
}
```
- Time complexity: O(N)
- Space complexity: O(N)
