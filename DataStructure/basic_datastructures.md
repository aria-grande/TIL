# 자료 구조의 비교
자주 사용하는 기본적인 자료구조의 개념을 정리하교 비교해보자.

## Data structures
- [Array](#array)
- Stack
- Queue
- Singly Linked List
- Doubly Linked List
- Hash Table
- Tree
- Binary Tre
- Binary Search Tree
- B-Tree


## Array
```
여러 데이터를 연속된 메모리 공간 안에 담는 자료구조로, 인덱스와 인덱스에 대응하는 데이터로 이루어져있다.
고정 길이로 생성되는 static array, 유동적인 길이를 가질 수 있는 dynamic array가 있다.
일반적으로 사용되는 것은 static array이다.

배열은 길이와 배열의 시작 주소를 가지고 있으며, 시작주소 + (data type size) * (index) 를 통해 타겟을 찾아가므로 
indexing은 O(1)의 시간 복잡도를 가진다.

int[] array = new int[5];

0x0000 0x0004 0x0008 0x000C 0x00010 0x00011
  2      3       1     4      100     52
```

### Dynamic array
크기를 resizing 할 수 있느 배열이며,<br/>
insert시 array가 다 차가면, 더 큰 사이즈의 배열을 생성 후, 기존 array에 있던 데이터 카피 및 재할당 한다.<br/>
Static array와 비교했을 때, 리사이징이 가능한 점. 하지만 리사이징을 하는데 드는 cost도 고려해야 하기 때문에, insert시 시간 복잡도는 증가하게 된다.
