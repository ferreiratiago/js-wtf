# What the f** JavaScript
These are some of the weirdest things brought to us by JavaScript.

* [Number](#number)
* [Math](#math)
* [Operators](#operators)
* [String](#string)
* [Array](#array)
* [Immediately Invoked Function Expression](#immediately-invoked-function-expression)
* [Lexical Grammar](#lexical-grammar)
* [Statements](#statements)
* [Destructuring](#destructuring)
* [Temporary Dead Zones](#temporary-dead-zones)

## [Number](https://github.com/ferreiratiago/js-wtf/blob/master/number.md)
```js
Number('0.')    // 0
Number('.0')    // 0
Number('.')     // NaN
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#wtf)

```js
Number({})      // NaN
Number([])      // 0
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#wtf-1)

```js
Number(undefined)   // NaN
Number(null)        // 0
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#wtf-2)

```js
Number('0O0')       // 0
Number('0X0')       // 0
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#wtf-3)

```js
Number.MAX_VALUE > 0;   //true
Number.MIN_VALUE < 0;   //false
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#wtf-4)

```js
42.toFixed(2)       // SyntaxError: Invalid or unexpected token
42. toFixed(2)      // SyntaxError: Unexpected identifier
42 .toFixed(2)      // '42.00'
42 . toFixed(2)     // '42.00'
42.0.toFixed(2)     // '42.00'
42..toFixed(2)      // '42.00'
(42).toFixed(2)     // '42.00'
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/number.md#why-5)

## [Math](https://github.com/ferreiratiago/js-wtf/blob/master/math.md)
```js
Math.max() > Math.min()   // false
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/math.md#wtf)

## [Operators](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md)
```js
[] + {}     // '[object Object]'
{} + []     // 0
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md#wtf)

```js
true + true === 2   // true
true - true === 0   // true
true === 1          // false
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md#wtf-1)

```js
0.1 + 0.2 === 0.3   // false
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md#wtf-2)

```js
1 < 2 < 3   // true
3 > 2 > 1   // false
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md#wtf-3)

```js
'5' + 3     // '53'
'5' - 3     // 2
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/operators.md#wtf-4)

## [String](https://github.com/ferreiratiago/js-wtf/blob/master/string.md)
```js
String(-0)      // '0'
Number('-0')    // -0
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf)

```js
String(null)        // 'null'
String([null])      //  ''

String(undefined)    // 'undefined'
String([undefined])  //  ''
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf-1)

```js
String({})      // '[object Object]'
String([])      // ''
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf-2)

```js
var s = Symbol('Hello World')   // Symbol(Hello World)

String(s)   // 'Symbol(Hello World)'
s + ''      // TypeError: Cannot convert a Symbol value to a string
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf-3)

```js
parseInt('15')              // 15
parseInt('15 and more')     // 15
parseInt('more and 15')     // NaN
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf-4)

```js
(!+[]+[]+![]).length    // 9
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/string.md#wtf-5)

## [Array](https://github.com/ferreiratiago/js-wtf/blob/master/array.md)
```js
[] == ![]   // true
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/array.md#wtf)

```js
Array.apply(null, Array(3))        // [ undefined, undefined, undefined ]
Array.apply(null, [,,,])           // [ undefined, undefined, undefined ]
Array.apply(null, {length : 3})    // [ undefined, undefined, undefined ]
Array.apply(null, (a,b,c) => {})   // [ undefined, undefined, undefined ]
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/array.md#wtf-1)

```js
[10, 9, 8, 3, 2, 1, 0].sort() // [ 0, 1, 10, 2, 3, 8, 9 ]
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/array.md#wtf-2)

## [Immediately Invoked Function Expression](https://github.com/ferreiratiago/js-wtf/blob/master/iife.md)
```js
function () { console.log('Hello World') }()       // SyntaxError: Unexpected token (
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/iife.md#wtf)

```js
function foo() { console.log('Hello World') }()  // SyntaxError: Unexpected token )
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/iife.md#wtf-1)

```js
!function () { console.log('Hello World') }()  // Hello World
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/iife.md#wtf-2)

## [Lexical Grammar](https://github.com/ferreiratiago/js-wtf/blob/master/lexical-grammar.md)
```js
function foo() {
    return
        'Hello World';
}

foo()   // undefined
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/lexical-grammar.md#lexical-grammar)

## [Statements](https://github.com/ferreiratiago/js-wtf/blob/master/statements.md)
```js
switch (42) {
    default:
        console.log('foo');
    case 10:
    case 20:
        console.log('bar');
        break;
    case 30:
        console.log('zed');
        break;
}
// foo
// bar
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/statements.md#wtf)

```js
function foo() {
    try {
        return 2
    } finally {
        return 3
    }
}

foo()   // 3
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/statements.md#wtf-1)

## [Destructuring](https://github.com/ferreiratiago/js-wtf/blob/master/destructuring.md)
```js
function foo(x = {y: 10}, {y = 20} = {}) {
    console.log(x.y, y);
}

foo();                  // 10 20
foo({y: 30}, {y: 40});  // 30 40
foo({}, {});            // undefined 20
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/destructuring.md#wtf)

## [Temporary Dead Zones](https://github.com/ferreiratiago/js-wtf/blob/master/tdz.md)
```js
(function(a = b, b) {

}(undefined, 1));   // ReferenceError
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/tdz.md#wtf)

```js
let b = 1;

(function(a = b, b) {
    console.log(a, b);
}(undefined, 2));   // ReferenceError
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/tdz.md#wtf-1)

```js
{
    typeof a;   // undefined
    typeof b;   // ReferenceError

    let b;
}
```
[*Why?*](https://github.com/ferreiratiago/js-wtf/blob/master/tdz.md#wtf-2)
