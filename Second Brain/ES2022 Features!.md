# .at() method on built-in indexables

> .at method on built-in indexables [📕](https://github.com/tc39/proposal-relative-indexing-method).

```js
const cart = ['🍎', '🍌', '🍍'];

// first element
cart.at(0); // '🍎'

// last element
cart.at(-1); // '🍍'

// out of bounds
cart.at(-100); // undefined 
cart.at(100); // undefined 
```

```js
const int8 = new Int8Array([0, 10, 42, -10]);

// first element 
int8.at(0); // 0

// last element
int8.at(-1); // -10

// out of bounds
int8.at(-100) // undefined 
int8.at(100) // undefined
```

```js
const sentence = 'This is a sample sentence'

// first element 
sentence.at(0); // 'T'

// last element
sentence.at(-1); // 'e'

// out of bounds
sentence.at(-100) // undefined
sentence.at(100) // undefined
```

# RegExp Match Indices

> additional information about the start and end indices of captured substrings [📕](https://github.com/tc39/proposal-regexp-match-indices)

```js
/(?<xs>x+)(?<ys>y+)/.exec('xxxyyxx');
/*[
  'xxxyy',
  'xxx',
  'yy',
  index: 0,
  input: 'xxxyyxx',
  groups: [Object: null prototype] { xs: 'xxx', ys: 'yy' }
]*/
```

```js
let input = "abcd";
let match = /b(c)/.exec(input);
let indices = match.indices;

// `indices` has the same length as match
indices.length === match.length

// The first element of `indices` contains the start/end indices of the match
indices[0]; // [1, 3];
input.slice(indices[0][0], indices[0][1]); // same as match[0]

// The second element of `indices` contains the start/end indices of the first capture
indices[1]; // [2, 3];
input.slice(indices[1][0], indices[1][1]); // same as match[1]);
```

# Object.hasOwn

> Object.hasOwn [📕](https://github.com/tc39/proposal-accessible-object-hasownproperty)

```js
let books = {}
books.prop = 'exists';

// `hasOwn` will only return true for direct properties:
Object.hasOwn(books, 'prop');             // returns true
Object.hasOwn(books, 'toString');         // returns false
Object.hasOwn(books, 'hasOwnProperty');   // returns false

// The `in` operator will return true for direct or inherited properties:
'prop' in books;                          // returns true
'toString' in books;                      // returns true
'hasOwnProperty' in books;                // returns true
```

# Error cause

> cause property indicating the cause of an error. [📕](https://github.com/tc39/proposal-error-cause)

```js
const actual = new Error('a better error!', { cause: 'Error cause' });

actual instanceof Error; // true
actual.cause; // 'Error cause'
```

```js
try {
  maybeWorks();
} catch (err) {
  throw new Error('maybeWorks failed!', { cause: err });
}
```

# Top-Level await

> await outside of async functions in modules [📕](https://github.com/tc39/proposal-top-level-await)

```js
// say this is index.mjs

// fails
await Promise.resolve('🍎');
// → SyntaxError: await is only valid in async function

// fix with wrapping
(async function() {
  await Promise.resolve('🍎');
  // → 🎉
}());

// to top-level await
await Promise.resolve('🍎') // '🍎'
```

```js
const i18n = await import(`./content-${language}.mjs`);
```

# Class field declarations

> Orthogonally-informed combination of public and private fields. [📕](https://github.com/tc39/proposal-class-fields)

```js
class SampleClass {
    /*
      instead of:
      constructor() { this.publicID = 42; }
    */
    publicID = 42; // public field

    /*
      instead of:
      static get staticPublicField() { return -1 }
    */
    static staticPublicField = -1;

    // static private field
    static #staticPrivateField = 'private';

    //private methods
    #privateMethod() {}

    // static block
    static {
      // executed when the class is created
    }
}
```

# ergonomic brand checks for private fields

> Brand checks without exceptions. [📕](https://github.com/tc39/proposal-private-fields-in-in)

```js
class C {
  #brand;

  #method() {}

  get #getter() {}

  static isC(obj) {
    // in keyword to check
    return #brand in obj && #method in obj && #getter in obj;
  }
}
```