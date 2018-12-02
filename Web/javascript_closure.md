# 클로저(Closure)
클로저는 함수의 생성 시점의 스코프에 있는 모든 변수의 집합이다. 클로저 안에 정의된 함수는 만들어진 환경을 기억한다.
```js
function sum(x) {
  return function(y) {
    return x + y;
  }
}
var add2 = sum(2);      // x is 2
var add5 = sum(5);      // x is 5
console.log(add2(10));  // y is 10, returns 12
console.log(add5(10));  // y is 10, returns 15
```

## 클로저는 언제 유용할까?
```js
// WHAT WILL RETURN?
function count() {
  var i = 0;
  for(i = 0; i < 5; i++) {
    setTimeout(function() {
      console.log(i);
    }, 1000);
  }
}
count();
```
‘5, 5, 5, 5, 5’가 리턴될 것이다. 실제로는 for문이 다섯 번 돈 후에야 setTimeout 함수가 실행되고 그땐 이미 i는 5가 되어있기 때문이다.

그럼 1, 2, 3, 4, 5를 출력하기 위해서는 어떻게 해야할까?

이럴 때 필요한 것이 ‘내부 함수를 둘러싼 외부함수를 기억하고 있는다’는 클로저이다.
```js
function count() {
  var i = 0;
  for(i = 0; i < 5; i++) {
    (function(i) {                 // ← closure
      setTimeout(function() {
        console.log(i);
      }, 1000);
    })(i);
  }
}
```

### 모듈 패턴(Module Pattern)
클로저를 이용하여 프라이빗 메소드를 흉내내는 것이 가능하다. 프라이빗 함수와 변수에 접근하는 퍼블릭 함수를 정의하기 위해 클로저를 사용할 수도 있다.
```js
var counter = (function() {
  var privateCounter = 0;
  return {
    increment: function() {
      privateCounter += 1;
    },
    decrement: function() {
      privateCounter -= 1;
    },
    value: function() {
      return privateCounter;
    }
  };
});

var counter1 = counter();
var counter2 = counter();
console.log(counter1.value());                  // returns 0

counter1.increment();
counter2.decrement();
console.log(counter1.value(), counter2.value());  // returns 1, -1
```
각 클로저들이 고유한 문법적 환경을 가졌지만 여기서 우리는 `counter.increment`, `counter.decrement`, `counter.value` 세 함수에 의해 공유되는 하나의 어휘적 환경을 만든다.

## 클로저가 항상 좋은 것은 아니다.

클로저는 공유해야 할 환경(변수)이 없다면 굳이 사용하지 않아도 된다. 불필요한 클로저는 처리 속도와 메모리 소비 측면에서 스크립트 성능에 부정적인 영향을 미칠 것이다.

예를 들어, 새로운 객체/클래스를 생성할 때, 메소드는 일반적으로 객체 생성자에 정의되기 보다는 객체의 프로토타입에 연결되어야 한다. 
그 이유는 생성자가 호출 될 때마다 메서드가 다시 할당되기 때문이다.
```js
function User(name, age) {
  this.name = name.toString();
  this.age = parseInt(age);
  this.getName = function() {
    return this.name;
  }
  this.getAge = function() {
    return this.age;
  }
}
```
위 코드는 클로저의 이점을 이용하지 않고 있다. 따라서 프로토타입으로 뺄 수 있겠다.
```js
function User(name, age) {
  this.name = name.toString();
  this.age = parseInt(age);
}
User.prototype.getName = function() {
  return this.name;
};
User.prototype.getAge = function() {
  return this.age;
};
```

https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8를 정독해보자!

