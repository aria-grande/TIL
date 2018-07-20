# Problem
```
정수 배열 arr이 있습니다. arr 안의 각 원소의 값은 다음 원소의 인덱스입니다.
이렇게 서로 이어지는 원소들의 배열이 있을때, arr[0]부터 시작하여 모든 원소를 들린 다음 다시 arr[0]로 도착할 수 있는지 찾으시오.
단, 시간복잡도는 O(n), 공간복잡도는 O(1) 이어야 합니다.

Input: [1, 2, 4, 0, 3]
Output: True
// 1 -> 2 -> 4 -> 3 -> 0 -> 1

Input: [1, 4, 5, 0, 3, 2]
Output: False
// 1 -> 4 -> 3 -> 0 -> 1
// arr[2], arr[5]를 들리지 않았습니다.

Input: [1, 2, 2, 0]
Output: False
// 1 -> 2 -> 2 -> 2 -> …
// arr[0]로 돌아오지 못합니다.
```

# Solution
특정 index를 방문 후 방문 했음을 알리기 위해 -1(가능하지 않은 인덱스)로 바꿔준다.<br/>
array를 iterate하면서 이미 방문한 인덱스에 또 도달했을 경우(cycle) iterate는 그만 돌아도 되므로 중단한다.<br/>
이 때, 재방문 한 index가 0이라면 이야기가 달라진다.<br/>
true를 리턴할 조건은 cycle이 존재하면서, 그 안에 첫 번째 원소가 있을 경우이기 때문이다.<br/>

```java
boolean rotatble(int[] arr) {
    boolean returnToFirst = false;
    int curIdx = 0;
    for(int count = 0; count < arr.length; ++count) {
        if(arr[curIdx] == -1) {
            break;
        }
        int oldIdx = curIdx;
        curIdx = arr[curIdx];
        arr[oldIdx] = -1;
        if(arr[0] == -1 && curIdx == 0) {
            returnToFirst = true;
        }
    }

    return returnToFirst && Arrays.stream(arr)
            .filter(x -> x != -1)
            .count() == 0;
}
```
