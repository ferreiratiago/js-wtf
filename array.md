# Array
`Array` is a global object used to construct the data structure array, which is a high-level list-like objects.

## WTF
```js
[] == ![]   // true
```

### Why?
This happens because of [`precedence`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) and  [`coercion`](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html).

Due to `precedence` we first execute the logical NOT `!` on the array `[]`, which negates its [truthy](https://developer.mozilla.org/en/docs/Glossary/Truthy) value. Therefore `![]` results into the boolean `false`.

At this point our expression translates into `[] == false`. Because `[]` is an `Object` and `false` a boolean, both operants get converted into numbers in order perform the comparison (this is because when anything gets compared with an `Object` both operands are first converted to numbers).

Through `coercion` our expression translates into `0 == 0`, which is `true`.

### Further Reading
* [MDN - Precedence](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
* [You Don't Know JS - Coercion](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html)

## WTF
```js
Array.apply(null, Array(3))        // [ undefined, undefined, undefined ]
Array.apply(null, [,,,])           // [ undefined, undefined, undefined ]
Array.apply(null, {length : 3})    // [ undefined, undefined, undefined ]
Array.apply(null, (a,b,c) => {})   // [ undefined, undefined, undefined ]
```

### Why?
This happens because since *ECMAScript 5th Edition* we can call `apply` with any kind of object array-like. This means that `apply`'s second argument (i.e. its definition is `fun.apply(thisArg, [argsArray])`) needs to have the property `length` and the integer properties in the range (0...length - 1). For instance, the array `[6,8]` has the property length of `2` and the integer properties from `0..2 - 1`, which are the array indexes (i.e. `0` is `[6,8][0]` and `1` is `[6,8][1]`).

Because all the 4 examples are objects array-like with the property `length`, `apply` will execute the `Array` function with each value from `0...length - 1` as its arguments.

For the example `(a,b,c) => {}` it's `length` is equal to `3` and `apply` will execute `Array` as follows:
```js
var example = (a,b,c) => {}   // 'example.length' is equal to 3.
// Array will be executed with its arguments being the properties' values in the range (0..length - 1), which is (0...2), i.e.
Array(example[0], example[1], example[2]) // [ undefined, undefined, undefined ]
```

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [MDN - Function.prototype.apply()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply)

## WTF
```js
[10, 9, 8, 3, 2, 1, 0].sort() // [ 0, 1, 10, 2, 3, 8, 9 ]
```

### Why?
This is not actually a `WTF` but how `sort()` method works.

According the specification, `sort()` sorts the elements of an array according to the string unicode code points.

Therefore the unicode value for first character of `10` (i.e. `1`) is lower than the unicode value for the character `2`.

```js
'0'.charCodeAt(0)       // 48
'2'.charCodeAt(0)       // 50
'10'.charCodeAt(0)      // 49
```

### Further Reading
* [MDN - Array.prototype.sort()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
