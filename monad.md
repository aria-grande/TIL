# 모나드
익명의 함수 왕자의 세미나

## Monad?
**컨텍스트**가 있는 

**연속된 계산**을 

**읽기 쉽게** 만들기 위한 

**순수 함수형** 패턴.

객체지향에서 여러 디자인 패턴이 있듯이 FP(Functional Programming)에서 있는 디자인 패턴 중 하나이다.

## 1. 읽기 쉽게 만들기 위한

복잡한 것을 일반화(추상화)해서 이해하기 쉽게 한다. 축약을 의미할 수도 있다.

'바나나 하나에 바나나 하나를 추가하면 바나나 두개' 보다는 '바나나 1 + 1 = 바나나 2'가 읽기 쉽다.

## 2. 순수 함수형 패턴

### 함수형이 아닌 것

- state-less
- global variables
- NO side effect
- 절차가 필요한(running procedure dependency). 시간에 구애받지 않는

대부분의 언어는 순수하지 않은 기능을 제공하지만 모나드는 순수함을 전제로 한다.


## 3. 연속된 계산

```js
// Original Code
var x = 1;
var y = 2;
var result = x + y;

// Trial 1: 순수 함수형으로 표현해보자.
((x => 
      (y => 
            x + y))
  (1))
      (2)

// Trial 2: 함수를 읽기 쉽게 해보자.
bind(1, x =>
bind(2, y =>
     x + y));

function bind(mv, f) { // mv: monad value
    return f(mv);
}
```

### 모나드 기본 패턴

```js
bind(계산, 계산 결과를 바인딩할 기호 => 
bind(계산, 계산 결과를 바인딩할 기호 => 
     결과));
```

bind는 특별한 일을 하지 않는다. **Identity 모나드**


## 4. 컨텍스트가 있는
연속된 계산 속에 있는 공통 기능

#### 컨텍스트의 예

- Maybe 모나드: 계산 과정 중에 결과가 null인 경우 처리를 하는 컨텍스트

  ```js
  function getNameById(id) {
      if(id == 1) {
          return "WORLD";
      }
      return null;
  }
  
  bind(getNameById(2), x =>
       bind(x.toLowerCase(), y =>
           "Hello" + y));
  // 를 하면 `Uncaught TypeError: Cannot read property 'toLowerCase' of null` 에러가 발생할 것이다.
  // 모나드를 의미하는 bind를 바꿔보자.
  function bind(mv, f){
      if(mv != null) {
          return f(mv);
      }
      return null;
  }
  // 이게 바로 maybe 모나드! fast-fail!
  ```

- Writer 모나드: 계산 과정 중 기록을 할 수 있는 컨텍스트

  ```js
  var result = 
      bind(1,              x=>
      bind(log("x: " + x), _ =>
      bind(2,              y =>
           x + y)));
  // 부수 효과가 없기 때문에 로그는 계산 결과와 함께 받는다.
  
  // bind를 바꿔보자.
  function bind(mv, f) {
      var result = f(mv.value);
      return {
          value: result.value,
          logs: mv.logs.concat(result.logs)
      };
  }
  // 두번 째 라인의 `1.value`는 에러가 나타날 것이다.
  // 코드 구조를 고쳐야 하겠다.
  var result = 
      bind(mreturn(1),     x =>
      bind(log("x: " + x), _ =>
      bind(mreturn(2),     y =>
          x + y)));
  function mreturn(v) {
      return { value: v, logs: [] };
  }
  function log(s) {
      return {
          value: null,
          logs: [s]
      }
  }
  // mreturn과 bind 함수가 writer 모나드의 형태이다.
  ```

- Reader 모나드: 계산 과정 중 어디서든지 값을 참조할 수 있는 컨텍스트. DI가 필요할 경우 많이 사용됨.

  ```js
  var config = { debug: true };
  function calc(x) {
      if(config.debug) {
          console.log("on debugging");
      }
      return x;
  }
  
  // 전역 변수를 참조하고 있으므로 순수하지 않다. 바꿔보자.
  function calc(x, config) {
      if(config.debug) {
          console.log("on debugging");
      }
      return x;
  }
  
  // 얘를 이제 바꿔보자.
  var result =
      bind(mreturn(calc(1)),    x=>
      bind(ask(),          ,    config =>
      bind(mreturn(calc(2)),    y =>
           mreturn(x _ y)
  )));
  result({debug: true}); // result의 결괏값도 function이어야 한다.
  
  function mreturn(v) {
      return function(r) {
          return v;
      };
  }
  function bind(mv, f) {
      return function(r) {
          return f(mv(r))(r);	// r이 필요한 이유는 처음 넘겨줬던 context를 호출해서 실제 필요한 값을 빼낸다.
      }
  }
  ```
  
- State 모나드: 계산 과정 중 읽고 쓸 수 있는 상태가 필요한 컨텍스트

  ```js
  어려워ㅠㅠ
  ```

## 정리

모나드 값 != 일반 값

Container, Boxing, Wrapping, Context이라고 불리기도 한다.


### Scala에서는

```scala
for{
 x <- getValueById(1)
 y <- Some(2)
} yield x + y 
```

이런 식으로 언어 차원에서 조금 지원을 해주고 있음. functional 하게 동작하도록 도와주는 라이브러리들도 있음.

### JS에서는

모나드를 지원해주는 라이브러리들이 있음.

원하는 모나드 타입의 function을 불러다 사용하면 됨.

https://github.com/monet/monet.js/blob/master/docs/MAYBE.md


### 책 추천

- 스칼라로 배우는 함수형 프로그래밍
- 가장 쉬운 하스켈 책
