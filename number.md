# Number
The `Number` JavaScript object is a wrapper object allowing you to work with numerical values.

## WTF
```js
Number('0.')    // 0
Number('.0')    // 0
Number('.')     // NaN
```

### Why?
When converting strings into numbers Javascript is able to understand that a period before or after a numeric value represents a decimal number. That's the reason why the get `0` as the result of the first two expressions.

However, the period by itself represents the character `.`, which can not be converted into a number.

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [ECMAScript® 2015 Language Specification - The Number Constructor](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-number-constructor)

## WTF
```js
Number({})      // NaN
Number([])      // 0
```

### Why?
The reason for this is because when the method `Number` gets an Object as argument it tries to convert it to a non-Object type. In this case it converts both `{}` and `[]` to string values.

```js
String({})      // '[object Object]'
String([])      // ''
```

Because the grammar cannot interpret the string `'[object Object]'` the result is `NaN`. As for the empty string `''` it is converted into `0` [by specification](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tonumber-applied-to-the-string-type).

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [ECMAScript® 2015 Language Specification - The Number Constructor](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-number-constructor)
* [ECMAScript® 2015 Language Specification - The String Constructor](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-string-constructor)

## WTF
```js
Number(undefined)   // NaN
Number(null)        // 0
```

### Why?
As defined by [ToBoolean](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-toboolean) specification both `null` and `undefined` represent the absence of something.

`undefined` is more generic since it's used to represent a variable's value when no other value is assigned. It means that a variable has been declared but has not yet been assigned a value.

`null`, on the other hand, is an assignment value. It can be assigned to a variable as a representation of no value. It's a blank object reference.

Because of this, I came to believe that this is why `undefined` represents a `NaN` when trying to convert to number, meaning no value assigned. And `null` the value `0` meaning a falsy representation of a value.

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [ECMAScript® 2015 Language Specification - ToBoolean](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-toboolean)

## WTF
```js
Number('0O0')       // 0
Number('0X0')       // 0
```

### Why?
There's nothing wrong with the two expressions.

The first is the new ES6 Octal representation, where the middle character is actually the capital letter `O`, not a zero. Not wrong but confusing.

As for the last one is the ES6 Hexadecimal representation.

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [ECMAScript® 2015 Language Specification - ToNumber](http://www.ecma-international.org/ecma-262/6.0/index.html#sec-toboolean)

## WTF
```js
Number.MAX_VALUE > 0;   //true
Number.MIN_VALUE < 0;   //false
```

### Why?
It's easy to understand that `Number.MAX_VALUE` is bigger than `0`, however it's strange that `Number.MIN_VALUE` is not smaller than `0`.

That's because `Number.MIN_VALUE` is not actually the minimum value possible, but the minimum **positive** value possible, which is very very very small (`5e-324` to be specific) but bigger than `0`.

We can safely use `Number.MIN_SAFE_INTEGER`, the smallest integer `n`, i.e. −(2<sup>53</sup>−1).

### Further Reading
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
* [ECMAScript® 2015 Language Specification - Number.MAX_VALUE](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-number.max_value)
* [ECMAScript® 2015 Language Specification - Number.MIN_VALUE](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-number.min_value)

## WTF
```js
42.toFixed(2)       // SyntaxError: Invalid or unexpected token
42. toFixed(2)      // SyntaxError: Unexpected identifier
42 .toFixed(2)      // '42.00'
42 . toFixed(2)     // '42.00'
42.0.toFixed(2)     // '42.00'
42..toFixed(2)      // '42.00'
(42).toFixed(2)     // '42.00'
```

### Why?
Having a period after a number is the way to say that a number is fractional. However this makes the use of static methods inconsistent.

On our first example, `42.toFixed(2)`, because `42.` is a completely valid number it is immediately confronted with `toFixed`, which makes it an invalid expression.

Even a space between `42.` and `toFixed` does not solves the problem. However, a space between `42` and `.toFixed` solves the problem.

Another way to fix this (if we can call it a fix) is to treat our period as part of our number or wrap it inside parens.

### Further Reading
* [MDN - Number.prototype.toFixed()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed)
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
