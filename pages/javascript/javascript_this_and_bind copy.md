---
title: This and Bind
sidebar: mydoc_sidebar
permalink: javascript_this_and_bind.html
folder: javascript
---

## **This** is determined at the time of the call not defined. It's context sensitive.
## When we use **this** , there is a clash between Object oriented programming and functional programming.  
To prevent this we need to use **bind**
```java
const dog = {
    sound: 'woof',
    talk: function() {
        console.log(this.sound);
    }
}

dog.talk()  // woof
const talkFunction = dog.talk;
talkFunction()  // undefined

// To prevent this, we use bind !!!
const boundFunction = talkFunction.bind(dog);
boundFunction();    // woof
```