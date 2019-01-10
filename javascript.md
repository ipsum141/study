# Some notable features of JavaScript.


## Variable.

There are three types of variable: `var`, `let` and `const`.

`var` is accessable from everywhere in same and inner scope:

```js
var a = "Hello, world!";

(function foo() {
    console.log(a);     // "Hello, world!";
})();
```

```js
console.log(a);         // "Hello, world!";

var a = "Hello, world!";
```

When JavaScript gets executed, `var` declaration is concepturally "moved" to the top of its scope. so you
can reference it everywhere in same and inner scope.

This behavior is called **'hoisting'**.

`let` and `const` are accessable only after declaration:

```js
console.log(a, b);      // error.

let a = "Hello, ";
const b = "world!";
```

Unlike `var`, `let` and `const` are not hoisted.

and `const` is constant.

When you try to use undeclared variable, that variable get automatically
declared in global scope in `var`.

```js
(function foo() {
    a = "Hello, world!";
    console.log(a);         // "Hello, world!"
})();

(function bar() {
    console.log(a);         // "Hello, world!"
                            // you can use 'a' here because 'a' is declared in global scope.
})();
```


## Data Types.

JavaScript has following data types.

+ `string`
+ `number`
+ `boolean`
+ `null` and `undefined`
+ `object`
+ `symbol`

```js
// Result of 'typeof' is string.
var a;
typeof a;                   // "undefined"

a = "Hello, world!";
typeof a;                   // "string"

a = 42;
typeof a;                   // "number"

a = true;
typeof a;                   // "boolean"

a = null;
typeof a;                   // "object" -- wtf? bug.

a = undefined;
typeof a;                   // "undefined"

a = { b: "c" };
typeof a;                   // "object"
```

**Bug/feature:** `typeof null` is `"object"`. not `"null"`.

This is a long-standing bug in JS, but one that is likely never going to be fixed.
Too much code on the Web relies on the bug and thus fixing it would cause a lot more bugs!

### Object.

The `object` type refers to a compound value where you can set properties (named locations) that
each hold their own values of **any type**.

```js
var obj = {
    a: "Hello, world!",
    b: "42",
    c: true,
};

obj.a;              // "Hello, world!"
obj.b;              // 42
obj.c;              // true

obj["a"];           // "Hello, world!"
obj["b"];           // 42
obj["c"];           // true
```

Properties can either be accessed with dot notation (i.e., obj.a) or bracket notation (i.e., obj["a"]).

**Bracket notation** is useful if you want to access a property/key using variable, such as:

```js
var obj = {
    a: "hello world",
    b: 42,
};

var b = "a";

obj[b];			    // "hello world"
obj["b"];		    // 42
```

### Array.

An array is an `object` that holds **value of any type** in numerically indexed position. For example:

```js
var arr = [
    "hello world",
    42,
    true
];

arr[0];			// "hello world"
arr[1];			// 42
arr[2];			// true
arr.length;		// 3

typeof arr;		// "object"
```

### Function.

Function is also subtype of `object`.

```js
function foo() {
    return 42;
}

foo.bar = "Hello, world!";

typeof foo;         // "function"
typeof foo();       // "number"
typeof foo.bar;     // "string"
```

There is another method to declare function:

```js
const foo = () => {
    return 42;
};

foo.bar = "hello world";

typeof foo;         // "function"
typeof foo();       // "number"
typeof foo.bar;     // "string"
```

This is called **arrow function**.

Albeit `function` is subtype of `object`, `typeof function` returns `"function"`. 
because unlike others, `function` is callable. so `function` is treated separately.

### Built-in Type Methods.

There are many built-in methods. for example:

```js
var a = "hello world";
var b = 3.14159;

a.length;           // 11
a.toUpperCase();    // "HELLO WORLD"
b.toFixed(4);       // "3.1416"
```

The "how" behind being able to call a.toUpperCase() is more complicated than just that method existing on the value.

Briefly, there is a String (capital S) object wrapper form, typically called a "native," that pairs with the primitive string type;
it's this object wrapper that defines the toUpperCase() method on its prototype.

When you use a primitive value like "hello world" as an object by referencing a property or method (e.g., a.toUpperCase() 
in the previous snippet), JS automatically "boxes" the value to its object wrapper counterpart (hidden under the covers).

A string value can be wrapped by a String object, a number can be wrapped by a Number object, and a boolean can be wrapped by a 
Boolean object. For the most part, you don't need to worry about or directly use these object wrapper forms of the values 
-- prefer the primitive value forms in practically all cases and JavaScript will take care of the rest for you.


## Coercion.

When you try to do something between different data types, JavaScript
automatically convert one to another data type so that two data types are same.
this behavior is called **implicit coercion**.

```js
    var a = "42";

    var b = a * 1;

    console.log(a, b);      // "42", 42
```

Or you can change one data type to another explicitly on your own.
this is called **explicit coercion**.

```js
var a = "42";

var b = Number(a);

console.log(a, b);          // "42", 42
```


## Comparing Values.

### Truthy & Falsy.

**"Falsy"** are data types that becomes `false` when it's coerced to `boolean`.

**"Truty"** are data types that becomes `true` when it's coerced to `boolean`.

The specific list of "falsy" values in JavaScript is as follows:

+ `""` (empty string)
+ `0`, `-0`, `NaN` (invalid `number`)
+ `null`, `undefined`
+ `false`

Any value that's not on this "falsy" list is "truthy".

### Equality.

There are four equality operators: `==`, `===`, `!=`, and `!==`.

Difference between `==` and `===` is that `==` checks for equality with coercion allowed, 
and `===` checks for equality without coercion allowed.

```js
var a = "42";
var b = 42;

a == b;			    // true
a === b;		    // false
```

The != non-equality form pairs with ==, and the !== form pairs with ===. 
All the rules and observations hold symmetrically for these non-equality comparisons.

You should take special note of the == and === comparison rules if you're comparing two non-primitive values,
like objects (including function and array). Because those values are actually held by reference, 
both == and === comparisons will simply check whether the references match, not anything about the underlying values.

For example, arrays are by default coerced to strings by simply joining all the values with commas (,) in between. 
You might think that two arrays with the same contents would be == equal, but they're not:

```js
var a = [1,2,3];
var b = [1,2,3];
var c = "1,2,3";

a == c;		// true
b == c;		// true
a == b;		// false
```

### Inequality.

<!-- TODO -->


## Strict mode.


## Code block.


## `this`.


## Closures.


## Asynchronous and Callback.
