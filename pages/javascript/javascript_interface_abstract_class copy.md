---
title: Interface and Abstract Class
sidebar: mydoc_sidebar
permalink: javascript_interface_abstract_class.html
folder: javascript
---

### Interface

    - An interface is a **contract** that defines the properties and what the object that implements it can do.

    - An interface does **not exist at runtime**. So it is not possible to make an introspection. (instanceOf does not work)

    - Promote **loose coupling**

### Abstract Class

    - A class is both a contract and the implementation of a factory. An abstract class is also an implementation but incomplete.

    - An abstract class exists at runtime even if it has only abstract methods. (then **instanceof can be used**)

    - An abstract class with abstract methods cannot be instantiated directly

    - Strongly couple classes together

### Difference between Interface and Abstract Class

    - We should always reach out for interfaces first and resort to the usage of an abstract classes when we want to **inject** functionality to a similar classes