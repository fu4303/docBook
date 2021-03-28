---
title: Various Javascript Tips
date: 2020-11-20
permalink: /javascript/tips/index.html
toc: true
comments: 0
eleventyNavigation:
  key: Tips
  order: 30
  parent: Javascript
---

## Table of Contents
- [Unique array in javascript](#Unique-array-in-javascript)
- [Generate a unique global id for elements that need one](#Generate-a-unique-global-id-for-elements-that-need-one)
- [Pre-populate an array in javascript](#Pre-populate-an-array-in-javascript)

### Unique array in javascript

And today's code snippet is about how to get unique values from an array in JavaScript.

I have seen some versions of this snippet before, but the one I like to recommend the most is the use of a [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) object alongside with the [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) in JavaScript.

By default, a `Set` is meant to store unique values and spreading it into an array is enough to give us the desired result.


```ts
const uniqueArray = arr => [...new Set(arr)]

uniqueArray(['ReactJS', 'NextJS', 'NodeJS', 'ReactJS']) // ['ReactJS', 'NextJS', 'NodeJS']

uniqueArray([1, 2, 2, 3, 3, 3, 4, 4, 4, 4]) // [1, 2, 3, 4]
```

- [Table of Contents](#Table-of-Contents)

### Generate a unique global id for elements that need one

Examples:

- Setting `key` property when looping an array in ReactJS (_watchout for potential performance issues if going this path!_).
- Setting `id` attribute to DOM elements.
- Cache response from endpoints that don't provide you with an identifier.

As a [curried function](https://en.wikipedia.org/wiki/Currying), it keeps a local `counter` variable and for every new `uniqueId` generated `counter`'s value is incremented.
An optional `prefix` can also be sent in case you want some extra information alongside with the id.


```js
function createUniqueId() {
  let counter = 0

  return (prefix = '') => {
    if (prefix) {
      return `${prefix}_${++counter}`
    }

    return `${++counter}`
  }
}

const uniqueId = createUniqueId()

console.log(uniqueId()) // 1
console.log(uniqueId()) // 2
console.log(uniqueId()) // 3
console.log(uniqueId('testing')) // testing_4
```

- [Table of Contents](#Table-of-Contents)


### Pre-populate an array in javascript

This is the second post I write about code snippets I find useful (you can check the first one [here](/blog/code-snippets-uniqueid)).
And today's code snippet is how to pre-populate an array in JavaScript.

The `for` loop is probably one of the first choices that comes to mind when dealing with arrays or collections.
But instead, I prefer to create an array with [Array.from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from).

If you've never heard of `Array.from` before, it accepts and array-like or an iteratable object as its first argument so we can map into it.
Once the array is created, `map` gives us each element in the newly created array so we can populate it with, for example, the index of each element.


```ts
function createArray(size: number) {
  return Array.from({ length: size }).map((_, index) => index + 1)
}
```

or using the Array constructor:


```ts
function createArray(size: number) {
  return Array.from(Array(size)).map((_, index) => index + 1)
}
```

- [Table of Contents](#Table-of-Contents)
