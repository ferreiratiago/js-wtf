# Statements
JavaScript `statements` perform actions but do not produce any value.

## WTF
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

### Why?
According to the specification, the `default` expression can be placed anywhere in the `switch` block. However, if we place it anywhere except in the last position (as shown in the example above) we will get some weird behaviour.

In this case, for our `42` example the engine will go to all switch cases, skipping the `default`, and it will not find a match. At this point it will invoke the `default` clause and log `foo`. But because we didn't add a `break` statement after the `default` it will execute the following `case`s until it reaches a `break`. Therefore it will log `bar`.

### Further Reading
[Kyle Simpsons - What the... JavaScript? YouTube Video](https://www.youtube.com/watch?v=2pL28CcEijU)

## WTF
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

### Why?
This happens because the result of evaluating the `finally` block is a `return`. Meaning that the result is the `return` completion of the expression followed (i.e. the expression `3`).

However, by doing this, the result of the `try` block is overridden by the result of the `finally` block. Therefore explaining why our final result when executing `foo`  is `3`.

### Further Reading
* [ECMAScript® 2015 Language Specification - The try Statement ] (https://www.ecma-international.org/ecma-262/6.0/index.html#sec-try-statement)
