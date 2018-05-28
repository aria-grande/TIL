# Problem
Calculate a depth of a given binary tree.

# Solution
재귀를 이용하여 max depth 값을 출력할 것이다.
현재 노드와 depth 값을 들고다닐 것이며, 노드가 null일 경우, 재귀 종료.
그렇지 않다면, children에 대해 재귀 실행.

```java
int getDepth(Node head, int height) {
  if (head == null) {
    return height;
  }
  return Math.max(getDepth(head.left, height + 1), getDepth(head.right, height + 1));
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
