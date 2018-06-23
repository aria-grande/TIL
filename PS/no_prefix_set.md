# Problem
https://www.hackerrank.com/challenges/no-prefix-set/problem
```
N개의 string이 주어질 때, 어느 하나라도 다른 string의 prefix가 아니라면 'GOOD SET'을 출력하고,
하나라도 prefix인게 존재한다면 'BAD SET'과 bad set을 만든 첫 번째 string도 같이 출력하라.
```

## Test cases
```
2
a
abc
```
```
2
abc
a
```
```
2
ab
ac
```

# Solution
customized Trie를 이용하여 해결할 수 있다.

```java
# TrieNode

class TrieNode {
  int count;
  int childrenCount;
  TrieNode[] children;
  
  public TrieNode() {
    this.count = 0;
    this.childrenCount = 0;
    this.children = new TrieNode[26];
  }
  
  public void insertIfNoPrefix(char[] chars) {
    TrieNode cur = this;
    for(int i = 0; i < chars.length; ++i) {
      int idx = chars[i] - 'a';
      if(cur.children[idx] == null) {
        cur.children[idx] = new TrieNode();
      }
      cur.children[idx].count++;
      cur.childrenCount++;
       
      cur = cur.children[idx];
      int diff = cur.count - cur.childrenCount;
      if (cur.count > 1 && ((i == chars.length - 1 && diff >= 1) || diff >= 2)) {
        return false;
      }
    }
    return true;
  }
}
```

```java
void printGoodOrBadPrefixSet(String[] queries) {
    TrieNode root = new TrieNode();
    for(String query : queries) {
        boolean inserted = root.insertIfNoPrefix(query.toCharArray());
        if (!inserted) {
            System.out.println("BAD SET\n" + query);
            return ;
        }
    }
    System.out.println("GOOD SET");
}
```

query의 갯수가 N개고 각 쿼리의 길이가 M일때, <br/>
Time complexity: O(N*M) <br/>
Space complexity: O(N*M)
