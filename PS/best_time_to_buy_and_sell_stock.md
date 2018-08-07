# Problem
https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/564/

```
Say you have an array for which the ith element is the price of a given stock on day i.
Design an algorithm to find the maximum profit. 
You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).
Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).
```

# Solution
buy: 매입가<br/>
cur: 현재가<br/>
next: 다음날가격

다음날 가격이 현재가보다 떨어질 경우, 매도를 하고,<br/>
현재가가 매입하려는 가격보다 적다면 매입을 한다.

```java
public int maxProfit(int[] prices) {
    int max = 0;
    int purchasePrice = Integer.MAX_VALUE;
    for(int ci = 0; ci < prices.length; ++ci) {
        int cur = prices[ci];
        int next = (ci == prices.length - 1) ? cur - 1 : prices[ci + 1];
        if (cur < purchasePrice) {
            prev = cur;
        }
        else if (cur > next) {
            max += cur - purchasePrice;
            purchasePrice = next;
        }
    }
    return max;
}

```

Time complexity: O(N)

Space complexity: O(1)


# Better Solution
다시 잘 생각해보자. 꼭 '매도 시점'과 '매수 시점'이 기록되어야 하는 것은 아니니,
배열의 increasing 부분을 모두 더하면 된다. So simple!

```java
public int maxProfit(int[] prices) {
    int max = 0;
    for(int i = 0; i < prices.length - 1; ++i) {
      if (prices[i] < prices[i + 1]) {
        max += prices[i + 1] - prices[i];
      }
    }
    return max;
}
```
Time complexity: O(N)

Space complexity: O(1)
