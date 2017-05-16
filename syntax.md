# Syntax
`Syntax` is what allows JavaScript to interpret when a piece of code is syntactically valid or not.

## WTF
```js
function foo() {
    return
        'Hello World';
}

foo()   // undefined
```
### Why?
This happens because  automatically adds a semicolon when *the offending token is separated from the previous token by at least one `LineTerminator`*.

In this case, our engine will add a semicolon after the offending token `return`.

```js
function foo() {
    return;                 // <- notice the semicolon
        'Hello World';
}
```

Now, when executing `foo`, our return value would be `undefined` instead of `Hello World`.

The same rule of automatic semicolon insertion is valid for the statements `continue`, `break`, `throw`, `yield` expression and `arrow functions`.

## Further Reading
* [ECMAScript® 2016 Language Specification - Rules of Automatic Semicolon Insertion](https://www.ecma-international.org/ecma-262/7.0/index.html#sec-rules-of-automatic-semicolon-insertion)
