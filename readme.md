# [array-merge-by-key](https://www.npmjs.com/package/array-merge-by-key)

[![npm](https://img.shields.io/npm/v/array-merge-by-key.svg)](https://www.npmjs.com/package/array-merge-by-key)
[![License](https://img.shields.io/github/license/zitros/array-merge-by-key.svg)](LICENSE)
[![Build Status](https://travis-ci.org/ZitRos/array-merge-by-key.svg?branch=master)](https://travis-ci.org/ZitRos/array-merge-by-key)

Effectively merge arrays of objects into a single array by merging objects with the same key 
(property). Also use this module to merge objects with the same property value in one array. 

This is a micro module, which includes light and well-tested code.

Example
-------

```javascript
import mergeByKey from "array-merge-by-key";

const array1 = [
    { id: "100500", any: 11, other: "UA", props: "1-1" },
    { id: "100501", any: 22, other: "US", props: "5-9" }, // same id
    { id: "100502", any: 33, other: "EN", props: "1-4" }
];

const array2 = [
    { id: "100501", any: 22, other: "US", props: "9-9" }, // same id
    { id: "100503", any: 44, other: "AU", props: "7-4" }
];

// const arrayN = [...]

const result = mergeByKey("id", array1, array2);

// result is [
//  { id: "100500", any: 11, other: "UA", props: "1-1" },
//  { id: "100501", any: 22, other: "US", props: "9-9" }, // merged
//  { id: "100502", any: 33, other: "EN", props: "1-4" },
//  { id: "100503", any: 44, other: "AU", props: "7-4" }
// ]
```

Usage
-----

Module `array-merge-by-key` exports function `mergeByKey(key, array1, array2, ...)` by default.
Module uses `Object.assign` to merge two objects having the same key (property) value. The 
assignment is performed *from right to left*, which means that the most right passed array will have 
priority over previous ones. The comparison of key values is strict (`===` operator). The order of 
elements in resulting array is the same as they appear in arguments, from *left to right*, from the 
first to the last element of arrays. Objects that do not have a key (property) will never be merged 
with others and will have the same memory reference. The new (merged) objects does not mutate old 
ones. The new array does not mutate any of passed arrays.

Objects having the same key values in the same array also merge. For example:

```javascript
mergeByKey("id", [{ id: 1, test: "54" }, { id: 1, test: "76" }])
//  Results with [{ id: 1, test: "76" }]
```

Licence
-------

[MIT](LICENSE) © [Nikita Savchenko](https://nikita.tk)
