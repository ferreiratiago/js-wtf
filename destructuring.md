# Destructuring
`Destructuring` assignment allow us to assign properties of arrays or objects to variables.

## WTF
```js
function foo(x = {y: 10}, {y = 20} = {}) {
    console.log(x.y, y);
}

foo();                  // 10 20
foo({y: 30}, {y: 40});  // 30 40
foo({}, {});            // undefined 20
```

### Why?
The inconsistency is on the last line with `foo({}, {})`'s result of `undefined 20`.

As for the first argument the value of `{}` is able to override the default value of `{y: 10}`. Because our passed object `{}` does not have a value for `y`, `x.y` will log `undefined`.

On the other side, the provided value of `{}` as the second argument is only able to override the default value assign to `{y = 20}`. Through destructuring we are able to declare `y` even when the provided argument is an empty object (as in this case). This means, that for the second argument we are not able to override the destructuring `{y = 20}`. We will always have our variable `y` declared.

The inconsistency comes when we expect the same behaviour for our first argument `x = {y: 10}`.

### Further Reading
* [ExploringJS - Destructuring](http://exploringjs.com/es6/ch_destructuring.html)
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
