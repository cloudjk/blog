---
title: Object Literals
sidebar: mydoc_sidebar
permalink: javascript_object_literals.html
folder: javascript
---

### Object Literals
#### 1. same name property value can be removed
#### 2. returned object can be assigned to a variable
#### 3. function property's colon and function can be removed

```java
const getName = (fname, sname) => {
  const objName = {
    fname,
    sname,
    fullname: function() { // ==> fullname() {
      return fname.concat(' ', sname);
    }
  }
  return objName;
}

const name = getName('Sharon', 'Stone');
console.log(name.fname);
console.log(name.sname);
console.log(name.fullname());
```

#### 4. object key can be substituted by variable
```java
const key = "last name";
const obj = {
  "firstName" :'Chandler',
  [key]: 'Bing'
}

console.log(obj);
```