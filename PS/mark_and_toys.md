# Problem
https://www.hackerrank.com/challenges/mark-and-toys/problem

```
Mark가 사고 싶어 하는 장난감들의 가격이 int[] 형태로 주어지고, 쓸 수 있는 예산이 k로 주어집니다.
예산 내에서 가장 많이 살 수 있는 갯수를 출력하시오.
```

# Solution
가장 저렴한 것들 부터 구입할 때, 가장 많이 살 수 있다.

```java
int maximumToys(int[] prices, int k) {
    Arrays.sort(prices);
    int cnt = 0;
    int sum = 0;
    for(int price : prices) {
        if (sum + price > k) {
          break;
        }
        sum += price;
        cnt++;
    }
    return cnt;
}
```

Time complexity: O(nlogn)<br/>
Space complexity: O(1)
