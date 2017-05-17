# Operators
`Operators` allow us to perform operations on pieces of data.

## WTF
```js
[] + {}     // '[object Object]'
{} + []     // 0
```

### Why?
The `+` operator being commutative is only true for numbers.

In this example the `+` operator is being used in two distinct contexts.

For the expression `[] + {}` `+` behaves as an operator to append multiple strings, mainly `[]` and `{}`. Through `Coercion` both operands are converted to string using the static methods `.toString`, which results into `[].toString() + ({}).toString()`. This last one translates into `'' + [object Object]` that explains the final result of `'[object Object]'`.

On last expression `{} + []` the first operant is a pair of curly brackets (i.e. an empty block). This empty blocks means that we don't to anything, therefore we more forward with our execution.

When reaching the `+` operator it behaves an unary operator because it only has the one operant `[]`. Through `Coercion` `[]` translates into `0` and we end up with the final result of `0`.

### Further Reading
* [ECMAScript® 2015 Language Specification - Unary plus (+)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators#Unary_plus)

## WTF
```js
true + true === 2   // true
true - true === 0   // true
true === 1          // false
```

### Why?
Here the `+` operator performs a numeric addition.

Because none of the operands is a string, both are converted into numbers. [By definition](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tonumber) the boolean `true` is converted into the number `1` and the boolean `false` into the number `0`.

Therefore, the expression `true + true` is translated into `1 + 1` that returns `2`.

### Further Reading
* [The Addition operator](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-applying-the-additive-operators-to-numbers)

## WTF
```js
0.1 + 0.2 === 0.3   // false
```

### Why?
This is not a problem to be fair.

**This is because computers can only natively store integers and therefore need some way to represent decimal numbers. This representation comes with some degree of inaccuracy. - [Source](http://0.30000000000000004.com/)** That's why we get the problem described above.

In detail, the values `0.1` and `0.2` translate into the fractional values of `1/10` and `1/5` which are both repeating numbers on a binary representation. When we do math on repeating decimals, we end up with leftovers which carry over when converting our base 2 result into a base 10 number.

Btw, the value result for `0.1 + 0.2` is actually `0.30000000000000004`.

### Further Reading
* [JavaScript.com - Numbers](https://www.javascript.com/learn/javascript/numbers)
* [Floating Point Math](http://0.30000000000000004.com/)

## WTF
```js
1 < 2 < 3   // true
3 > 2 > 1   // false
```

### Why?
The reason for this is `Coercion`, which says that when the operands of an operator are different types, one of them is converted into the other's type.

On the first expression `1 < 2 < 3` we will first solve `1 < 2`, which is `true` and then implicitly `true < 3`. In this case `true` is converted into `1` because of coercion and the final expression is `1 < 3`, which is `true`.

As for the second expression `3 > 2 > 1`, we will end up with `true > 1` (`true` as the result from `3 > 2`), and because `true` is converted into `1` the expression `true > 1` is equal to `false`.

### Further Reading
* [MDN - Comparison operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Less_than_operator)
* [Kyle Simpsons - What the... JavaScript? YouTube Video](https://www.youtube.com/watch?v=2pL28CcEijU)

## WTF
```js
'5' + 3     // '53'
'5' - 3     // 2
```

### Why?
By specification the addition operator either performs string concatenation or numeric addition. When one of the operands is a string, the engine converts the other operand to a string and returns the concatenation of both operands. In this case, because our left operand `'5'` is a string the final result is the concatenation of `'5'` and `String(3)`, i.e. `'53'`.

On the other hand, the `-` operator performs subtraction on two operands of numeric type. When an operator is not of the type `Number` the engine will convert it into a number. For that reason the string `'5'` is converted into the number `5` to which is subtracted `3`. The final result is the number `2`.

## Further Reading
* [You Don't Know JS: Types & Grammar by Kyle Simpson](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html)
* [Kyle Simpsons - What the... JavaScript? YouTube Video](https://www.youtube.com/watch?v=2pL28CcEijU)
