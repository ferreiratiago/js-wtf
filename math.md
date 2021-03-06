# Math
`Math` is a built-in object that has properties and methods for mathematical purposes.

## WTF
```js
Math.max() > Math.min()   // false
```

### Why?
`Math.max()` returns `-Infinity` when no arguments are provided, i.e. the smallest possible value. By having `-Infinity` as the base of comparison, `Math.max()` will always return the correct result when only a single value is provided.

Following the same idea, `Math.min()` returns `Infinity` when no arguments are provided, i.e. the highest possible value.

Therefore, when comparing `Math.max() > Math.min()` we are actually comparing `-Infinity > Infinity`, which is `false`.

### Further Reading
[Stackoverflow - T.J. Crowder answer](http://stackoverflow.com/a/5101991)
[ECMAScript® 2015 Language Specification - ToNumber](https://www.ecma-international.org/ecma-262/6.0/index.html#sec-tonumber)
