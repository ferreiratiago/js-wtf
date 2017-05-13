# IIFE
`IIFE` (Immediately-Invoked Function Expression) is the Javascript way to create an execution context and execute it immediately.

By creating a function a new execution context is created and all variables and functions only live there, meaning that they cannot be access from the outside.

## WTF
```js
function () { console.log('Hello World') }();       // SyntaxError: Unexpected token (
```

### Why?
When the parser encounters the `function` keyword in the global scope or inside another function it treats it as a `function declaration` and not as a `function expression`.

The `SyntaxError` exception is because the function declaration requires a name and the parser got our `(` after the `function` keyword instead of the name.

In order to treat it as a `function expression` we need to explicitly tell the parser.

```js
(function () { console.log('Hello World') })();     // 'Hello World'
```

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
* [Stackoverflow - gion_13](http://stackoverflow.com/a/8228308)

## WTF
```js
function foo() { console.log('Hello World') }();  // SyntaxError: Unexpected token )
```

### Why?
Although we have overcome the first `SyntaxError` and our function declaration being completely valid, we still can't execute it by putting parens (parentheses, `()`). The `SyntaxError` is now for a different reason.

We usually place parens after an expression in order to indicate that the expression is a function and we want to executed. However, this is not true when placed after a statement. In this case they work as a grouping operator, which is useful to control the precedence of evaluation.

The `SyntaxError` comes because a grouping operator needs to contain an expression.

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)

## WTF
```js
!function () { console.log('Hello World') }();  // Hello World
```

### Why?
The big difference here is that we are dealing with `function expressions`.

When our parser reaches our unitary operator `!` it expects an expression after it.

Because we have a `function expression` followed by parens our function would be executed (thereby logging `Hello World`) and the result used for the unitary operator `!`.

Although we don't need to wrap our function inside parens (this is because our parser is already expecting an expression), it's still a good idea to use them. Such parens will typically indicate that the function expression is to be executed immediately. Also, it is a good convention.

However, please do remember that this approach makes the code less readable.

#### ~ WTF
```js
var foo = function () { return 'Hello World' }();

true && function () { console.log('Hello World') }();
0, function () { console.log('Hello World') }();

+function () { console.log('Hello World') }();
-function () { console.log('Hello World') }();
*function () { console.log('Hello World') }();
~function () { console.log('Hello World') }();
```

### Further Reading
* [Ben Alman - IIFE](http://benalman.com/news/2010/11/immediately-invoked-function-expression/)
* [Wikipedia - Immediately-invoked function expression](https://en.wikipedia.org/wiki/Immediately-invoked_function_expression)
