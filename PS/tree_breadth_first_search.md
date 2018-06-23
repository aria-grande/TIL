# Problem
https://www.hackerrank.com/challenges/tree-level-order-traversal/problem<br/>

트리의 루트 노드가 주어지면, level order로 traverse 및 출력하는 메소드를 작성하라.

## Solution
Queue를 사용해서, 루트 노드를 enqueue.
dequeue 한 노드의 children을 left, right 순서로 enqueue.
이 로직을 queue가 빌 때까지 하면 된다.

```java
void bfs(Node root) {
  StringBuilder sb = new StringBuilder();
  Queue<Node> queue = new LinkedList<Node>();
  queue.add(root);
  while(!queue.isEmpty()) {
    Node node = queue.poll();
    sb.append(node.data);
    sb.append(" ");
    if(node.left != null) {
      queue.add(node.left);
    }
    if(node.right != null) {
      queue.add(node.right);
    }
  }
  System.out.println(sb.toString().trim());
}
```

Time complexity: O(n)<br/>
Space complexity: O(n)
