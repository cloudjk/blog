---
title: SOLID Principles
sidebar: mydoc_sidebar
permalink: javascript_solid_principle.html
folder: javascript
---

### 1. Single Responsibility Principle

> Every method/class should handle a single responsibility

- 
  ```javascript
  -- The Challenge
  class Statistics {
    public computeSalesStatistics() {
      // ...
    }
    public generateReport() {
      // ...
    }
  }

  -- Solution
  class Statistics {
    public computeSalesStatistics() {
      // ...
    }
  }

  class ReportGenerator {
    public generateReport() {
      // ...
    }
  }
  ```

### 2. Open/Close Principle

  - Open to extension, Closed for modification. The idea is that a class, once implemented, should be closed any further modification, If any functionality is needed, it can be added later using extension features such as inheritance. This is primarily done so as to not break existing code as well as unit tests. It also results in a modular code.

  - 
    ```javascript
    -- The Challenge
    class Rectangle {
      public width: number;
      public height: number;
      constructor(width: number, height: number) {
        this.width = width;
        this.height = height;
      }
    }

    class Circle {
      public radius: number;
      constructor(radius: number) {
        this.radius = radius;
      }
    }

    function calculateAreasOfMultipleShapes(
      shapes: Array<Rectangle | Circle>
    ) {
      return shapes.reduce(
        (calculatedArea, shape) => {
          if (shape instanceof Rectangle) {
            return calculatedArea + shape.width * shape.height;
          }
          if (shape instanceof Circle) {
            return calculatedArea + shape.radius * Math.PI;
          }
        },
        0
      );
    }

    main();

    -- Solution
    interface Shape {
      getArea(): number;
    }

    class Rectangle implements Shape {
      public width: number;
      public height: number;
      constructor(width: number, height: number) {
        this.width = width;
        this.height = height;
      }
      public getArea() {
        return this.width * this.height;
      }
    }

    class Circle implements Shape {
      public radius: number;
      constructor(radius: number) {
        this.radius = radius;
      }
      public getArea() {
        return this.radius * Math.PI;
      }
    }

    function calculateAreasOfMultipleShapes(shapes: Shape[]) {
      return shapes.reduce(
        (calculatedArea, shape) => {
          return calculatedArea + shape.getArea();
        },
        0
      );
    }
    ```

### 3. Liskov Substitution Principle

  - Each derived class must replace its parent without affecting parent's behavior (Should not break code which means that return type should be equal)
  - 
    ```javascript
    -- The Challenge
    class Rectangle {
      constructor(private _width: number, private _height: number) {}

      public area() : number {
        return this._height * this._width;
      }
    }

    interface Shape {
      area() : number;
    }

    class Rectangle implements Shape {
      constructor(private _width: number, private _height: number) {}

      public area() : number {
        return this._height * this._width;
      }
    }

    class Square implements Shape {
      constructor(private _height: number) {}

      public area() : number {
        return Math.pow(this._height, 2);
      }
    }
    ```

### 4. Interface Segregation Principle

  - Instead of a generalized interface for a class, it is better to user separate segregated interfaces with smaller functionalities.
  - 
    ```javascript
    -- The Challenge
    interface Bird {
      fly(): void;
      walk(): void;
    }

    class Nightingale implements Bird {
      public fly() {
        /// ...
      }
      public walk() {
        /// ...
      }
    }

    class Kiwi implements Bird {
      public fly() {
        throw new Error('Unfortunately, Kiwi can not fly!');
      }
      public walk() {
        /// ...
      }
    }

    -- Solution
    interface CanWalk {
      walk(): void;
    }

    interface CanFly {
      fly(): void;
    }

    class Nightingale implements CanFly, CanWalk {
      public fly() {
        /// ...
      }
      public walk() {
        /// ...
      }
    }

    class Kiwi implements CanWalk {
      public walk() {
        /// ...
      }
    }
    ```

### 5. Dependency Inversion Principle

  - High-level classes shouldn't depend on low-level class. Both should depend on abstractions. Abstractions shouldn't depend on details. Details should depend on abstractions.

  - This principle states that a class should not depend on another class, but instead on an abstraction of that class. It allows loose-coupling and more reusability.

  - 
    ```javascript
    -- The Challenge
    class MemoryStorage {
      private storage: any[];

      constructor() {
        this.storage = [];
      }

      public insert(record: any): void {
        this.storage.push(record);
      }
    }

    class PostService {
      private db = new MemoryStorage();

      createPost(title: string) {
        this.db.insert(title);
      }
    }

    -- Solution
    interface DatabaseStorage {
      insert(record: any): void;
    }

    class MemoryStorage implements DatabaseStorage {
      private storage: any[];

      constructor() {
        this.storage = [];
      }

      public insert(record: any): void {
        this.storage.push(record);
      }
    }

    class PostService {
      private db: DatabaseStorage;

      constructor(db: DatabaseStorage) {
        this.db = db;
      }

      createPost(title: string) {
        this.db.insert(title);
      }
    }
    ```

### 6. Ref Site
  - [SOLID](https://medium.com/@alejandromarr/solid-principles-using-typescript-c475031efcd3)