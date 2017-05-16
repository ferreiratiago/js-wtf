# String
The `String` global object is a constructor for strings, or a sequence of characters.

## WTF
```js
String(-0)      // '0'
Number('-0')    // -0
```

### Why?
The only reason for this is ECMAScript Team's decision.

The team has decided to lie to the user when stringifying `-0` because most people don't know what a `-0` is it for.

### Further Reading
* [ECMAScript® 2015 Language Specification - ToString Applied to the Number Type](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tostring-applied-to-the-number-type)
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)

## WTF
```js
String(null)        // 'null'
String([null])      //  ''

String(undefined)    // 'undefined'
String([undefined])  //  ''
```

### Why?
By [definition](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tostring) when converting `null` or `undefined` into a string we get the `'null'` and `'undefined'` string respectively.

On the other hand, when converting an object into a string Javascript tries to convert it to an non-Object type. For array it tries to convert it to a string, which is done by executing the method `.toString`. By definition `toString` applies the string conversion to all array elements and [joins](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/join) them into one string. However, if an element is `undefined` or `null`, it is converted to the empty string.

### Further Reading
* [ECMAScript® 2015 Language Specification - ToString](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tostring)
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)

## WTF
```js
var s = Symbol('Hello World')   // Symbol(Hello World)

String(s)   // 'Symbol(Hello World)'
s + ''      // TypeError: Cannot convert a Symbol value to a string
```

### Why?
The reason for this is that ECMAScript Team has decided that `Symbol`s can be explicitly coerce but not implicitly coerce.

For that reason `String(s)` work perfectly and prints out the string `'Symbol(Hello World)'` but the expression `s + ''` throws an error.

### Further Reading
* [ECMAScript® 2015 Language Specification - ToString](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tostring)

## WTF
```js
parseInt('15')              // 15
parseInt('15 and more')     // 15
parseInt('more and 15')     // NaN
```

### Why?
By definition `parseInt` function converts its first argument to a string, parses it, and then returns an integer or `NaN`.

The problem here are the characters that do not represent a valid number in the specified `radix` (by default is `10`). In our first `15` example, both `1` and `5` are valid numbers on base `10`, therefore the execution of `parseInt` works smoothly and the integer `15` is returned.

However, "if `parseInt` encounters a character that is not a numeral in the specified radix, it ignores it and all succeeding characters and returns the integer value parsed up to that point." This explains why our last example resolves into `NaN`, meaning that when the engine encounters the first character that is not a numeral, i.e. `m`, there's no integer value parsed until then.

### Further Reading
* [MDN - parseInt](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

## WTF
```js
(!+[]+[]+![]).length    // 9
```

### Why?
This is just a JS trick that involves some [`precedence`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) and [`coercion`](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html).

To understand this we need to break it down:
* The first operation to happen is the logical NOT `!` on the unary plus `+[]`, i.e. `!+[]`.
    * Our unary operation `+[]` evaluates the operand `[]` and converts it to a number, which results into `0`. This `0` is actually the conversion of the empty array `[]` into the string `''` and then into the number `0`.
    * Next, our logical NOT `!` will negate the truthy of `0`, which is first converted to the boolean `false`.
    * In short, `!+[]` > `!+''` > `!+0` > `!0` > `!false` > `true`.
* At this stage our expression is translated into `(true+[]+![]).length`, and the follow operation to take place is `true+[]`.
    * This time our `+` operator works as a concatenation operator evaluating first the first operand `true`. By specification `true` is converted into the string `'true'`.
    * We now evaluate our second operand `[]`, which translates into the empty string `''`.
    * In short, `true+[]` > `'true'+[]` > `'true'+''` > `'true'`.
* Our expression is now `('true'+![]).length`. The now move forward with `'true'+![]`.
    * Our first operand `'true'` is ready to be concatenated.
    * Our second operand `![]` needs to be evaluated and converted to a string. Therefore, `!` negates the truthy of `[]`, which [by definition](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) is `false`, resulting into the string `false`.
    * In short, `'true'+![]` > `'true'+false` > `'true'+'false'` > `'truefalse'`.
* With our final expression being `('truefalse').length` is easy to understand our result of `9`.

### Further Reading
* [MDN - Truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)
* [Charlieharvey - javascript The Weird Parts](https://charlieharvey.org.uk/page/javascript_the_weird_parts)
