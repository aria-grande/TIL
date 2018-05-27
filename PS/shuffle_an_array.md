# Problem
Write a method shuffles an array consist of numbers.

# Solution
## Shuffle
유한한 sequence 내 elements를 랜덤하게 재정렬 하는 것

### 로직

current element의 index+1부터 sequence의 길이까지의 elements 중 random하게 골라 current element와 swap
두번 째부터 마지막 element까지 위의 로직 수행

```java
void shuffle(int[] arr) {
  final int len = arr.length;
  int[] shuffled = new int[len];
  
  for(int i = 0; i < len - 1; ++i) {
    double random = Math.random(); // 0.0 ~ 1.0(exclusive)
    // minimum range: i + 1
    // range of random: (len - 1) - (i + 1) + 1
    int randIdx = (int)(random * (len - (i + 1)) + (i + 1);
    int tmp = arr[randIdx];
    arr[randIdx] = arr[i];
    arr[i] = tmp;
  }
}
```
| 복잡도  | Big-O |
|-------|-----|
| Time  | O(n)|
| Space | O(1)|


<hr/>

## 참고 링크
- [Fisher-Yates shuffle](https://en.wikipedia.org/wiki/Fisher%E2%80%93Yates_shuffle)
