# Problem
https://www.hackerrank.com/challenges/drawing-book/problem
```
책은 1부터 n 페이지까지 구성되어 있고, 넘버링은 오른쪽 페이지부터 시작한다.
미션은 p 쪽을 펼치는 것이다. 앞에서부터 혹은 뒤에서부터 펼쳐볼 수 있다고 할 때, 가장 적게 펼쳐 p 페이지에 접근할 때, 펼쳐보는 횟수를 구하여라.
```

# Solution
페이지의 구성은 아래 두 가지 경우가 있을 수 있다.
```
n이 짝수: [ , 1] - [2, 3] -... - [n, ]
n이 홀수: [ , 1] - [2, 3] -... - [n - 1, n]
```
앞에서 쪽수를 넘기는 것과 뒤에서부터 넘기는 것에 대한 카운트를 구한 후, 그 minimum 값을 리턴하면 된다.

```java
int pageCount(int n, int p) {
    int pagesFromBehind = (n % 2 == 0) ? n - p + 1 : n - p;
    return Math.min(p, pagesFromBehind) / 2;
}
```

Time complexity: O(1)<br/>
Space complexity: O(1)
