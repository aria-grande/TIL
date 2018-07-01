# Problem
https://www.hackerrank.com/challenges/pairs/problem

```
You will be given an array of integers and a target value.
Determine the number of pairs of array elements that have a difference equal to a target value.
```

# Solution
sorted array에서 equal difference를 찾아내는 것이 수월하며 이 때 시간 복잡도는 O(n)이다.<br/>
하지만 given array는 unsorted이므로, sort 하는데 O(nlogn)을 소요한다.<br/>

sorted integer array이기 때문에, array의 각 원소를 iterate하는 standard와 
standard + k 값을 충족할 값을 찾기 위해 array를 iterate 하는 pointer인 comparePointer를 이용할 수 있겠다.<br/>
standard + k 값을 충족하는 값이 나왔을 경우, comparePointer는 해당 인덱스의 다음을 가리키면 되며, sorted array를 한 번 탐색하면 끝나게 된다.

```java
int pairs(int k, int[] arr) {
  Arrays.sort(arr);
  
  int pairCnt = 0;
  int comparePointer = 1;
  for(int standard : arr) {
    for(int i = comparePointer; i < arr.length - 1; ++i) {
      if(standard + k == arr[i]) {
        comparePointer = i + 1;
        pairCnt++;
        break;
      }
    }
  }
  return pairCnt;
}
```

Time complexity: O(nlogn)<br/>
Space complexity: O(1)
