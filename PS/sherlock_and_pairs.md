# Problem
https://www.hackerrank.com/challenges/sherlock-and-pairs/problem

# Solution
1. array를 정렬
2. 값이 동일한 원소가 n 개일 때, 해당 원소로 만들 수 있는 pair count는 순열에 해당하며, `nP2 = n * (n - 1)`이다.
3. constraints를 보면 배열의 사이즈인 N은 최대 10^5이므로, pair count의 최댓 값은 10^10에 근접하다. integer의 범위를 넘을 수 있으므로 long type으로 취급.

```java
long getPairCount(int[] arr) {
  final int LEN = arr.length;
  Arrays.sort(arr);
  
  long count = 0;
  for(int i = 0; i < LEN;) {
    int j = i;
    while(j < LEN && arr[j] == arr[i]) {
      j++;
    }
    count += (long) (j - i) * (j - i - 1);
    i = j;
  }
  
  return count;
}
```

Time complexity: O(nlogn)<br/>
Space complexity: O(1)

## 이 때,
계속 3 개의 테스트 케이스만 통과하고 large N에 대한 테스트 케이스는 실패했다.

로직에 문제가 있나 하여 계속 살펴보았으나,

결국 타입 컨버전에 문제가 있었다. 선언만 long으로 해두고, 실제 값은 int 형태로만 넣어주고 있었던 것.

자바는 기본적으로 숫자는 int로 취급하고 있으므로, long 형이라고 명시적으로 선언해주거나(`0L, 1L..`), type convert(`(long) 123`)를 해줘야 한다.
