# Problem

# Solution
컨셉: 누적 + 빚 + 갚기
- buy1을 첫번째 주식을 사면서 빚지게 되는 가격,
- sell1은 첫번째 주식을 팔면서 취하게 되는 총 이득(+일수도, -일수도)
- buy2는 두번째 주식을 사면서 누적으로 빚지게 되는 가격(sell1 - buy2)
- sell2는 두번째 주식을 팔면서 취하게 되는 총 이득.

```java
public int maxProfit(int[] prices) {
    int buy1 = Integer.MIN_VALUE, buy2 = Integer.MIN_VALUE;
    int sell1 = 0, sell2 = 0;
    for(int price : prices) {
        buy1 = Math.max(buy1, -price);
        sell1 = Math.max(sell1, price + buy1);
        buy2 = Math.max(buy2, sell1 - price);
        sell2 = Math.max(sell2, price + buy2);
    }
    return sell2;
}
```

Time complexity: O(N)

Space complexity: O(1)
