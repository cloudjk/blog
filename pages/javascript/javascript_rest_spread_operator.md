---
title: Rest Operator / Spread Operator
sidebar: mydoc_sidebar
permalink: javascript_deep_copy.html
folder: javascript
---

### Rest Operator (Combine!)
- takes variable number of parameters or arguments and put them into an single array
- Specified in the function declaration

```java
  const displayColors = (message, ...colors) => {
    console.log(message);
    for (let i in colors) {
      console.log(colors[i]);
    }
  }
  let message = 'list of colors';
  displayColors(message, 'Red');
  displayColors(message, 'Red', 'Blue');
  displayColors(message, 'Red', 'Blue', 'Green');
}
```

### Speread Operator (Split!)
- takes an array and splits it into the individual elements
- Specified during funciton call

```java
  const displayColors = (message, ...colors) => {
    console.log(message);
    for (let i in colors) {
      console.log(colors[i]);
    }
  }
  let message = 'list of colors';
  const colorArray = ['Red', 'Blue', 'Green'];
  displayColors(message, ...colorArray);
}
```