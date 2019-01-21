# ES6 Features

## Destructing assignment

### Array
```js
const [first, second] = [1, 2]
console.log(first) // 1
```

```js
const [first, , third] = [1, 2, 3]
console.log(third) // 3
```

### Object
```js
const {name, age} = {name: 'aria', age: 10}
console.log(name) // 'aria'
```

## Rest Parameter
parameter name 앞에 `...`을 붙여주면 가변 arguments가 배열 형태로 parameter name에 지정됨.
```js
function f(a, b, ...args) {
  console.log(args);
}

f(1,2,3,4,5,6)  // [3,4,5,6]
```

## Spread Operator
Iterable object(배열, 문자열)을 함수 호출할 때 쪼개서 넣어준다.
```js
function getFirstChar(str) {
  return str
}

var str = "abcde"
console.log(getFirstChar(...str)) // "a"
console.log(getFirstChar(str))    // "abcde"
```
인자를 받는 곳에서 쪼개서 받지 않으면 쪼개진 글자 중 `str`에는 맨 처음 글자만 가지게 된다.

쪼개서 보낸걸 다 받아보자.
```js
function split(...str) {
  return str
}
console.log(split(...str))      // ["a", "b", "c", "d", "e"]
console.log(split(str))         // ["abcde"]
```

array를 flatten할 때 쓰이기도 한다.
```js
var missedNums = [3, 4]
var numbers = [1, 2]

numbers.push(missedNums)        // [1, 2, [3, 4]]
numbers.push(...missedNums)     // [1, 2, [3, 4], 3, 4]
```

## Regex

### Grouped captures

```js
let reDate = /(?<year>[0-9]{4})-(?<month>[0-9]{1,2})-(?<day>[0-9]{1,2})/
let match = reDate.exec('2019-1-21')
match.groups        // { year: "2019", month: "1", day: "21" }
const { year, month, day } = match.groups
console.log(year)   // 2019
```

### [Language detection](http://exploringjs.com/es2018-es2019/ch_regexp-unicode-property-escapes.html)

```js
let koRegex = /\p{Script=Hangul}/u

koRegex.test('안녕')      // true
koRegex.test('안녕hello') // true
koRegex.test('hello')    // false
```
지원하는 언어 스펙은 [여기](https://tc39.github.io/proposal-regexp-unicode-property-escapes/#sec-static-semantics-unicodematchproperty-p)서 참고 가능.
