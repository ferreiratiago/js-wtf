# TDZ (Temporary Dead Zone)
[Fabrício S. Matté](https://twitter.com/Ult_Combo) does a great work explaining what [Temporary Dead Zones](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified) are.

*"One of the main differences between the old `var` and the new `let`/`const` declarations (besides their `scope`) is that the latter are constrained by the `Temporal Dead Zone` semantics, meaning they will throw a `ReferenceError` when accessed (read/write) before being initialized, instead of returning `undefined` as a `var`-declared variable would."* - Fabrício S. Matté

## WTF
```js
(function(a = b, b) {

}(undefined, 1));   // ReferenceError
```

### Why?
We are using the new ES6 syntax of `default parameters` for our function.

However, because default parameters are evaluated from left to right this means that when the engine reaches the expression `a = b`, it tries to read `b` but this is not initialized. Although `b` exists, it is uninitialized and that throws an  `ReferenceError` exception due to TDZ semantics.

In fact, the same happens if we try to initialize `a` with itself.
```js
(function(a = a) {

}());   // ReferenceError
```

### Further Reading
* [JS Rocks - Temporal Dead Zone (TDZ) Demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)
* [PonyFoo - Temporal Dead Zone (TDZ) in Depth](https://ponyfoo.com/articles/es6-let-const-and-temporal-dead-zone-in-depth)

## WTF
```js
let b = 1;

(function(a = b, b) {
    console.log(a, b);
}(undefined, 2));   // ReferenceError
```

### Why?
"That is because default parameters are evaluated in an intermediate scope which exists between the parent and inner scope of the given function. The `a` and `b` parameters are bindings of this (intermediate) scope and are initialized from left to right, hence when `a`'s initializer tries to read `b`, the `b` identifier resolves to the b binding in the current scope (the intermediate scope) which is uninitialized at that point and thus throws a ReferenceError due to the TDZ semantics." (*Source: Fabrício S. Matté
[Temporal Dead Zone (TDZ) Demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)*).

### Further Reading
* [JS Rocks - Temporal Dead Zone (TDZ) Demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)
* [Wes Bos - Temporal Dead Zone](https://wesbos.com/temporal-dead-zone/)

## WTF
```js
{
    typeof a;   // undefined
    typeof b;   // ReferenceError

    let b;
}
```

### Why?
TDZ only happen with the new ES6 `let` and `const` variables declaration.

Because of this `typeof a` will return `undefined` due to the fact that `var`iable `a` is not defined. As for `typeof b`, the exception `ReferenceError` is thrown because `b` is defined but not initialized. This reference to the variable `b` before it's initialization falls into `b` TDZ.

Usually we could use `typeof` to make sure a variables existed and had a value. As with ES6 `let` and `const` we need to be aware of this TDZ semantics.

### Further Reading
* [JS Rocks - Temporal Dead Zone (TDZ) Demystified](http://jsrocks.org/2015/01/temporal-dead-zone-tdz-demystified)
