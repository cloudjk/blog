---
title: Introduction
sidebar: mydoc_sidebar
permalink: javascript_introduction.html
folder: javascript
---

![Copy](/assets/img/posts/shallow_deep_cp.png)

## 1. Shallow Copy

1) Assgin array to new array !!! This does not copy an array !!!

```java
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const assignedArr = arr
console.log(JSON.stringify(assignedArr))
arr[0] = {aa: 10}
console.log(JSON.stringify(assingedArr))    // assigned array chanages when the elements in orginal array changes !!! 
```

2) The spread operator (...)

```java
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = [...arr]
```

3) slice()

```java
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = arr.slice()
```

4) Object.assign(target, source) : copies all enumerable properties from source objects to a target object. Returns target object.

```java
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = []
Object.assign(shallowCopy, arr)
```

5) Array.from

```java
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = Array.from(arr)
```
## 2. Deep Copy

1) lodash _.cloneDeep()

```java
const originalArray = [
    37, 
    3700, 
    { 
        hello: "world" 
    }
]
const deepCopy = _.cloneDeep(originalArray)
```

2) custom funciton

```java
const originalArray = [37, 3700, { hello: "world" }]
const deepCopyFunction = (inObj) => {
    let outObj, val, key

    if (typeof inObj !== 'object' || inObj === null) {
        return inObj
    }

    outObj = Array.isArray(inObj) ? [] : {}

    for ( key in inObj ) {
        val = inObj[key]
        outObj[key] = deepCopyFunction(val)
    }

    return outObj
}
const deepCopy = deepCopyFunction(originalArray)
```

3) JSON.parse/stringify

**Do not use this when there is one of date, functions, undefined, Infinity, [NaN], RegExps, Maps, Sets, Blobs, FileLists, ImageDatas,
sparse Arrays, Type Arrays or other complex types withing your object in the object you want to deep copy**

```java
const originalArray = [37, 3700, { hello: "world" }]
const deepCopy = JSON.parse(JSON.stringify(originalArray));
```

4) rfdc (Really Fast Deep Clone)

**400% faster than lodash cloneDeep**

```java
const clone = require('rfdc')() // Returns the deep copy function
clone({a: 37, b: {c: 3700}})
```

## 3. Performance

1) When it comes to shallow copy, use "slice" which is the fastest.
2) In Deep copy, use "custom function" or "rfdc" and avoid using JSON.parse.
