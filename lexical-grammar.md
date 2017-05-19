# Lexical Grammar
*"A `lexical grammar` is a formal grammar defining the syntax of tokens. The lexical grammar lays down the rules governing how a character sequence is divided up into subsequences of characters, each part of which represents an individual token."* - [Wikipedia](https://en.wikipedia.org/wiki/Lexical_grammar)

## WTF
```js
function foo() {
    return
        'Hello World';
}

foo()   // undefined
```

### Why?
This happens by [automatic semicolon insertion (ASI)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Automatic_semicolon_insertion) when *the offending token is separated from the previous token by at least one `LineTerminator`*.

In this case, our engine will add a semicolon after the offending token `return`.

```js
function foo() {
    return;                 // <- notice the semicolon
        'Hello World';
}
```

Now, when executing `foo`, our return value is `undefined` instead of `Hello World`.

The same rule of automatic semicolon insertion is valid for the statements `continue`, `break`, `throw`, `yield` expression and `arrow functions`.

## Further Reading
* [ECMAScript® 2016 Language Specification - Rules of Automatic Semicolon Insertion](https://www.ecma-international.org/ecma-262/7.0/index.html#sec-rules-of-automatic-semicolon-insertion)
* [MDN - Automatic Semicolon Insertion](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Automatic_semicolon_insertion)
* [MDN - return](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/return)
