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



# How Javascript works behind the scenes

Our code --> Javascript Engine(Parser --Abstract Syntax Tree--> Conversion to Machine Code --> Code Runs)

## Execution Contexts and the Execution Stack

- Execution Context: A box, a container, or a wrapper which stores variables in which a piece of our code is evaluated and executed

  - (DEFAULT) Global Execution Context

    - Code that is not inside any function
    - Associated with the global object
    - In the browser, that's the `window` object.

  - New Execution Contexts: `first()`, `second()`, `third()`에 대해 각 새로운 execution context가 execution stack에 push되며, 메소드가 끝나면 각각 pop된다.

    ```js
    function first() {
        var a = 'hello';
        second();
    }
    function second() {
        var b = 'hi';
        thrid();
    }
    function thrid() {
        var c = 'hey!';
    	return c;
    }
    first();
    ```

### Execution Context Object

- Variable Object(VO): contains function arguments, function declarations
- Scope chain: contains the current variable objects as well as the variable objects of all its parents.
- `this` variable.

#### How it works?

##### 1. Creation phase

1. Creation of the VO

   - The `argument` object is created, containing all the arguments that were passed into the function.

   - Code is scanned for **function declarations**: for each function, a property is created in the VO, **pointing to the funciton**. *Only function declarations will be hoisted. [Function expression](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/function) and [Function constructor](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Function) will not be hoisted!*

   - Code is scanned for **variable declarations**: for each variable, a property is created in the VO, and set to `undefined`.

   -  Called **HOISTING!!**

     ```js
     /* Original code */
     function first() {
         console.log(name);
         var name = "aria";
         console.log(name);
     }
     /* Hoisted code */
     function first() {
         var name;
         console.log(name);
         name = "aria";
         console.log(name);
     }
     ```

2. Creation of the scope chain

3. Determine value of the `this` variable

##### 2. Execution phase

The code of the function that generated the current execution context is ran line by line.