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

Our first argument `{}` is able to override the default value of `{y: 10}`. `x.y` logs `undefined`.

However, our second argument `{}` is not able to override our variable `y` and not having it declared.

The inconsistency comes because the syntax is quite similar but the behaviour varies depending on the way we do destructuring.

### Further Reading
* [ExploringJS - Destructuring](http://exploringjs.com/es6/ch_destructuring.html)
* [Kyle Simpsons - What the... JavaScript? (YouTube)](https://www.youtube.com/watch?v=2pL28CcEijU)
