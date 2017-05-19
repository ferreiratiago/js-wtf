# Immediately-Invoked Function Expression
Immediately-Invoked Function Expression (`IIFE`) is the JavaScript way to create an execution context and execute it immediately.

By creating a function, a new execution context is created and all variables and functions only live there, meaning that they cannot be access from the outside.

## WTF
```js
function () { console.log('Hello World') }()       // SyntaxError: Unexpected token (
```

### Why?
When the parser encounters the `function` keyword in the global scope or inside another function it treats it as a `function declaration` and not as a `function expression`.

The `SyntaxError` exception is because the function declaration requires a `name` and the parser gets our `(` after the `function` keyword instead.

To treat it as a `function expression` we need to explicitly tell the parser, e.g.
```js
(function () { console.log('Hello World') })()     // 'Hello World'
```

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
* [Stackoverflow - gion_13](http://stackoverflow.com/a/8228308)

## WTF
```js
function foo() { console.log('Hello World') }()  // SyntaxError: Unexpected token )
```

### Why?
Although our function declaration is valid, we can't execute it by adding parens (i.e. `()`).

We usually place parens after an expression in order to indicate that an expression is a function and we want to execute it. However, this is not true when placed after a statement. In this case parens work as a grouping operator, which is useful to control precedence.

The `SyntaxError` comes because a grouping operator needs to contain an expression.

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)

## WTF
```js
!function () { console.log('Hello World') }()  // Hello World
```

### Why?
We are now dealing with a `function expression`.

When our parser reaches our unary operator `!` it expects an expression after it.

Because we have a `function expression` followed by parens our function would be executed (thereby logging `Hello World`) and the result used for the unary operator `!`.

Although we don't need to wrap our function inside parens (this is because our parser is already expecting an expression), it's still a good idea to use them. Such parens will typically indicate that the function expression is to be executed immediately. Also, it is a good convention.

#### +WTF
```js
var foo = function () { /* code */ }()

true && function () { /* code */ }()
0, function () { /* code */ }()

+function () { /* code */ }()
-function () { /* code */ }()
*function () { /* code */ }()
~function () { /* code */ }()
```

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
* [Wikipedia - Immediately-invoked function expression](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
