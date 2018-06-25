# Problem
```
Binary tree가 주어지면, 루트 노드를 기준으로 좌우 반전하는 메소드를 작성하세오.
이 문제는 구글이 Homebrew 창시자에게 낸 문제로 유명합니다.
```

# Solution
```java
void reverse(Node node) {
  if(node == null) {
    return ;
  }
  
  Node tmp = node.right;
  node.right = node.left;
  node.left = tmp;
  
  reverse(node.left);
  reverse(node.right);
}
```
BT의 노드 갯수가 N개라 할 때,<br/>
Time complexity: O(N)<br/>
Space complexity: O(1)<br/>
