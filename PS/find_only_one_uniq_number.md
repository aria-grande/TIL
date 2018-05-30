# Problem
1차원 배열에 숫자가 2개씩 중복해서 들어가있고 딱 1개만 혼자 들어가 있을 때 그 하나 있는 숫자를 찾으시오.


# Solution

Map을 활용한다. key는 배열의 숫자, value는 출현 빈도수를 저장하여
value가 1인 key를 리턴한다.

```java
int findOnlyOneUniqNum(int[] arr) {
  Map<Integer, Integer> board = new HashMap<Integer, Integer>();
  for(int num : arr) {
    int count = board.containsKey(num) ? board.get(num) : 0;
    board.put(num, ++count);
  }
  
  for(Map.Entry<Integer, Integer> elem : board.entrySet()) {
    if (elem.getValue() == 1) {
      return elem.getKey();
    }
  }
  
  return Integer.MIN_VALUE;
}
```

Time Complexity: O(n)
Space Complexity: O(n)
