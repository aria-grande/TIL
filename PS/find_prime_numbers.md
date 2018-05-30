# Problem
입력된 숫자 n까지에 대해, 존재하는 모든 소수(prime number)를 출력하라.

# Solution

Sieve of Eratosthenes 알고리즘을 이용한다.
소수를 찾고, 그의 배수를 모두 지워나가면 된다.
boolean array를 이용: index는 number를 의미하고, 값은 prime 여부를 판단.

```java
void getPrimeNumbersUntil(int n) {
  boolean[] isPrime = new boolean[n+1]; // if n = 3, array should be 0..3
  Arrays.fill(isPrime, true);
  
  for(int i = 2; i <= Math.sqrt(n); ++i) {
    if (isPrime[i]) {
      // 여기서 j = i*i를 하는 이유는, 2, 3, 4, 5, 6, 7, 8, 9를 테스트 해보면 알 수 있다.
      // i=2일때, 4,6,8을 지우고
      // i=3일때, 3,6,9가 아닌 3,9만 지워도 되기 때문이다.
      // 6을 두 번 지울필요가 없다.
      for(int j = i*i; j <= n; j += i) {
        isPrime[j] = false;
      }
    }
  }
  
  for(int k = 2; k <= n; ++k) {
    if (isPrime[k]) {
      System.out.print(k + ",");
    }
  }
}
```

| 복잡도 | Big-O |
|:----:|:------:|
|시간 | O(n*log*log n)|
|공간 | O(n)|


<hr/>

## 참고 링크
- [Sieve of Eratosthenes](https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes#cite_note-intro-8)
