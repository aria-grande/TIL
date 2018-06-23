# Problem
https://www.hackerrank.com/challenges/contacts/problem
```
We're going to make our own Contacts application! The application must perform two types of operations:

add name, where name is a string denoting a contact name. This must store name as a new contact in the application.
find partial, where name is a string denoting a partial name to search the application for. 
It must count the number of contacts starting with partial name and print the count on a new line.
Given n sequential add and find operations, perform each operation in order.
```

# Solution
[Trie](https://en.wikipedia.org/wiki/Trie)를 이용하여 해결 할 수 있다.<br/>
TrieNode 자료구조는 해당 노드가 visited된 count와 26개의 children nodes를 가진다.<br/>
26개인 이유는 input이 a-z로 한정되어있기 때문이며, children은 TrieNode의 배열 타입이다.

```java
class TrieNode {
  int count;
  TrieNode[] children;
  
  public TrieNode() {
    this.count = 0;
    this.children = new TrieNode[26];
  }
  
  public void insert(String s) {
    TrieNode current = this;
    for(char c : s.toCharArray()) {
      int idx = c - 'a';
      if (current.children[idx] == null) {
        current.children[idx] = new TrieNode();
      }
      current = current.children[idx];
      current.count++;
    }
  }
  
  public int find(String s) {
    TrieNode current = this;
    for(char c : s.toCharArray()) {
      int idx = c - 'a';
      if (current.children[idx] == null) {
        return 0;
      }
      current = current.children[idx];
    }
    return current == null ? 0 : current.count;
  }
}
```
```java
/* Solution.java */
static int[] contacts(String[][] queries) {
    List<Integer> result = new LinkedList<Integer>();
    TrieNode root = new TrieNode();
    for(String[] query : queries) {
        String operator = query[0];
        String contact = query[1];
        if ("add".equals(operator)) {
            root.insert(contact);
        } else if ("find".equals(operator)) {
            result.add(root.find(contact));
        }
    }
    return result.stream().mapToInt(i->i).toArray();
}
```
전체 쿼리가 N개이고 각 쿼리의 input인 `contact`의 길이가 M이라고 할 때,<br/>
Time complexity: O(N*M)
Space complexity: O(N*M)
