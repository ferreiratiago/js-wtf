# Array
`Array` is a global object used to construct the data structure array, which is a high-level list-like objects.

## WTF
```js
[] == ![]   // true
```

### Why?
This happens because of [`Precedence`](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence) and  [`Coercion`](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html).

Due to `Precedence` we first execute the logical NOT `!` on the array `[]`, which negates its [truthy](https://developer.mozilla.org/en/docs/Glossary/Truthy) value. Therefore `![]` results into the boolean `false`.

At this point our expression translates into `[] == false`. Because `[]` is an `Object` and `false` a boolean, both operants get converted into numbers in order perform the comparison (this is because when anything gets compared with an `Object` both operands are first converted to numbers).

Through `Coercion` our expression translates into `0 == 0`, which is `true`.

### Further Reading
* [MDN - Precedence](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)
* [You Don't Know JS - Coercion](https://www.safaribooksonline.com/library/view/you-dont-know/9781491905159/ch04.html)
