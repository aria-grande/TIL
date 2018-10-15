# Javascript
Javascript is an object-based script language used in front-end and back-end. In front-end, it is used to handle events, motions and etc.

## History
- 1996: Changed from LiveScript to Javascript to attract Java adevelopers.Javascript has almost nothing to do with Java.
- 1997: ES1(ECMAScript1) became the first version of the JavaScript language standard:
  - ECMAScript: The language standard.
  - JavaScript: The language in practice.
- 2009: ES5 was released with lots of new features.
- 2015: ES6/ES2015 was released: **the biggest update to the language ever.**
- 2015: Changed to an **annual release cycle.**
- 2016/2017/... : ES7/ES8/... will release.

# Syntax
## Equality Operators
### Type coersion
With use of `==` operator, it converts types string to integer, or etc.
```js
23 == '23' // returns true

var date = new date();
console.log(date); // Mon Oct 15 2018 08:24:57 GMT+0900 (Korean Standard Time)
date == "Mon Oct 15 2018 08:24:57 GMT+0900 (Korean Standard Time)" // returns true
```
### Equality operators
With use of `===` operator, it does not convert types and compare.
```js
23 === '23' // returns false


var date = new date();
console.log(date); // Mon Oct 15 2018 08:24:57 GMT+0900 (Korean Standard Time)
date === "Mon Oct 15 2018 08:24:57 GMT+0900 (Korean Standard Time)" // returns false
```

# [ES(ECMAScript)](https://ko.wikipedia.org/wiki/ECMA%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8)
- Well supported in all modern browsers.
- No support in order browsers.
- ES6: Can use most features in production with transpiling and polyfilling(converting to ES5).
