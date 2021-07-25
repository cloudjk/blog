---
title: Deep Copy
sidebar: mydoc_sidebar
permalink: javascript_deep_copy.html
folder: javascript
---

{% include image.html file="shallow_deep_cp.png" %}

## Shallow Copy

### 1. Assgin array to new array. This does not copy an array

```javascript
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

### 2. The spread operator (...)

```javascript
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = [...arr]
```

### 3. slice()

```javascript
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = arr.slice()
```

### 4. Object.assign(target, source) : copies all enumerable properties from source objects to a target object. Returns target object.

```javascript
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = []
Object.assign(shallowCopy, arr)
```

### 5. Array.from

```javascript
const arr = [
    {a: 1, b: 2, c: 3},
    {x: 10, y: 11},
    {q: 9}
]
const shallowCopy = Array.from(arr)
```
## Deep Copy

### 1. lodash _.cloneDeep()

```javascript
const originalArray = [
    37, 
    3700, 
    { 
        hello: "world" 
    }
]
const deepCopy = _.cloneDeep(originalArray)
```

### 2. custom funciton

```javascript
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

### 3. JSON.parse/stringify

**Do not use this when there is one of date, functions, undefined, Infinity, [NaN], RegExps, Maps, Sets, Blobs, FileLists, ImageDatas,
sparse Arrays, Type Arrays or other complex types withing your object in the object you want to deep copy**

```javascript
const originalArray = [37, 3700, { hello: "world" }]
const deepCopy = JSON.parse(JSON.stringify(originalArray));
```

### 4. rfdc (Really Fast Deep Clone)

**400% faster than lodash cloneDeep**

```javascript
const clone = require('rfdc')() // Returns the deep copy function
clone({a: 37, b: {c: 3700}})
```

## Performance

### 1. When it comes to shallow copy, use "slice" which is the fastest.
### 2. In Deep copy, use "custom function" or "rfdc" and avoid using JSON.parse.
