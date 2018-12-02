# Promise
Javascript는 기본적으로 비동기 + 싱글 스레드에서 돌아가는 언어다. 

**비동기는 특정 코드의 연산이 끝날 때까지 결과를 기다리지 않고 다음 코드를 실행하는 것을 의미**한다.(참고 [async and web framework](https://kstreee.github.io/techmemo/async_and_webframework.pdf))

비동기 코드의 실행을 기다렸다가 그다음 동작하도록 하기 위해, 콜백으로도 해결할 수 있다.
```js
var username;
$.get('/user/1', function(response) {
    username = response.user.name;
    console.log(username);	// 2. 응답 내 사용자 이름 출력
});
console.log(username);		// 1. undefined 출력
```

단순한 경우는 ajax로 처리할 수 있다. 하지만 이 뎁스가 꽤 깊어진다면?
```js
$.get('/user/1', function(response) {
  $.get('/user/1/orders', function(response2) {
    $.get('/user/1/payments', function(response3) {
      // ...
    });
  });
});
```

콜백 지옥이 탄생할 것이다.

이 콜백 지옥을 해결하기 위해 등장한 것이 Promise 패턴이다.

Promise에는 네 가지 상태가 있다. 
- pending(약속 수행 중)
- fulfilled(약속이 지켜짐)
- rejected(약속이 지켜지지 않음)
- settled(지켜진 것과는 관계 없이 약속 수행 완료)

약속이 지켜졌을 경우에 resolve 처리를 해주면, Promise 선언 뒤 then 함수로 인자들이 전달된다.

약속이 지켜지지 않았을 경우에는 reject 처리를 해주고, Promise 선언 뒤 catch 함수로 인자들이 전달된다.

위의 함수를 리팩토링 해보자.
```js
var promise = function(user_id) {
  return new Promise(function(resolve, reject) {
    $.get(`/users/${user_id}`, function(response) {
      resolve({ user_id: user_id, response: response });
    });
  };
};

promise(1)
.then(function(data) {
  return new Promise(function(resolve, reject) {
    $.get(`/users/${data.user_id}/orders`, function(response) {
      resolve({ user_id: user_id, response: response });
    });
  });
})
.then(function(data) {
  return new Promise(function(resolve, reject) {
    $.get(`/users/${data.user_id}/payments`, function(response) {
      resolve({ user_id: user_id, response: response });
    });
  });
})
.then(function(data) {
    console.log(data);
});
```
콜백 지옥이 사라졌다! 가독성도 높아졌다. ES6 이상에서 지원한다.

## 참고
https://programmingsummaries.tistory.com/325

# async/await
비동기 프로그래밍 언어에서 코드를 동기적으로 동작하게 하기 위한 ES8의 표준 문법이다.

'Promise, then'에 비해 훨씬 직관적이다.

동기로 처리될 함수 선언 앞에는 `async` 키워드를 붙여주고, 
그 함수를 호출하는 곳에서 `await` 키워드를 붙여주면 된다. 
Promise의 `resolve` 로 넘겨준 값을 받아서 `await` 키워드가 선언되어 있는 곳으로 넘겨준다.

예로, 출근하는 시간을 구하는 함수를 작성해보자.
콜백 형태로 구현할 경우 아래와 같다.
```js
(function goWork() {
  var walk = 1000;
  setTimeout(() => {
   console.log("1. walk for " + walk);
    var subway = 2000;
    console.log("2. subway for " + subway);
    setTimeout(() => {
      console.log("3. duration is  " + (walk + subway)); 
    }, subway);
  }, walk);
})();
```

프로미스 형태로 구현할 경우 아래와 같다.
```js
function goWork() {
  return new Promise(resolve => {
    var walk = 1000;
    setTimeout(() => {
      console.log('1. walk for ' + walk);
      resolve(walk);
    }, walk)
  });
}

goWork()
.then(time => 
  new Promise(resolve => { 
    var subway = 2000;
    setTimeout(() => {
      console.log('2. subway for ' + subway);
      resolve(subway + time);
    }, subway)
  }))
.then(time => console.log('3. duration is ' + time));
```

이를 `async`, `await` 으로 바꾸면 아래와 같다.
```js
(async function goWork() {
  var w = await walk();
  var s = await takeSubway();
  console.log("3. duration is " + (w + s));
})();
async function walk() {
  return new Promise(resolve => {
    var walk = 1000;
    setTimeout(() => {
      console.log("1. walk for " + walk);
      resolve(walk);
    }, walk);
  });
}
async function takeSubway() {
  return new Promise(resolve => {
    var subway = 2000;
    setTimeout(() => {
      console.log("2. subway for " + subway);
      resolve(subway);
    }, subway);
  });
}
```
훨씬 직관적이다! 키워드만으로 뭘 하려는 건지 알겠다. 
