# Reactive programming & ReactiveX
Reactive + Functional programming의 개념이 합쳐진 여러 프로그래밍 패러다임 중 하나

## [Reactive programming](https://en.wikipedia.org/wiki/Reactive_programming)
- A declarative programming paradigmconcerned with data streams and the propagation of change
- 특정 이벤트 발생에 반응하여 동작하도록 하는 프로그래밍 패러다임.
- 쉽게 콜백(callback) 혹은 리스너(listener)를 활용하는 방식.

### Example
```
view.setOnClickListener { view ->
 … 
}
```


## [ReactiveX](http://reactivex.io/)
- Reactive programming을 언어 무관하게 사용할 수 있도록 정의한 표준 프로토콜.
- Combination of the best ideas from the [Observer pattern](http://reactivex.io/documentation/observable.html), the Iterator pattern, and functional programming


### 언어별 구현체가 따로 있다.
- [RxJava](https://github.com/ReactiveX/RxJava)
- [RxJS](https://github.com/ReactiveX/rxjs)
- [RxSwift](https://github.com/ReactiveX/RxSwift)
- [RxRuby](https://github.com/ReactiveX/RxRuby)

### Why HOT?
- 기존 리액티브 방식의 한계를 극복한 new paradigm이기 때문이다!

#### 기존 리액티브 방식의 한계?
-  Callback 지옥에 빠지기 쉽다.
- 서로 다른 작업 간에 dependency가 걸리는 순간 로직의 복잡도 증가
- 복잡한 state들을 직접 관리해야 함.

각 깃헙 유저의 팔로워들의 레포를 프린트 하는 코드를 작성해보자.
기존 방식으로 작성시 callback 지옥에 빠지게 된다.
```
users = [‘aria’, ‘latte’]
for user in users:
  getFollowers(user, { resultJson ->
    followers = resultJson.tofollowers()
    for follower in followers:
      getRepos(follower, { resultJson ->
        repos = resultJson.toRepos()
        println(repos)
      })
  })
```

### Characteristics
- 함수형 프로그래밍과 결합되어 pure function 작성 및 chaining 가능.
    - avoid intricate stateful programs, using clean input/output functions over observable streams.
- Concurrency made easy
    - Observables and Schedulers in ReactivreX allow the programmer to abstract away low-level threading, synchronization, and concurrency issues.
- Async error handling
    - Traditional try/catch is powerless for errors in asynchronous computations, but ReactiveX is equipped with proper mechanisms for handling errors.
- 가독성 증가.
- 성능에 초점을 둔 것은 아니므로 때에 따라 느릴 수 있다.

```
users = ['aria', 'latte', 'choco-latte'] 

Observable.fromArray(users) .flatMap { user -> getFollowers(user) } 
.map { resultJson -> resultJson.toFollowers() }
.flatten()
.flatMap { follower -> getRepos(follower) }
.map { resultJson -> resultJson.toRepos() }
.subscribe { repos -> println(repos) } 
```

### When to use Rx?
http://www.introtorx.com/Content/v1.0.10621.0/01_WhyRx.html#WhyRx
