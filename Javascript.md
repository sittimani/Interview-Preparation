# JavaScript and ES6 Concepts

This document provides a summary of essential JavaScript and ES6 concepts that are crucial for technical interviews. 

## JavaScript Basics
- **Variables**: Use `let` and `const` instead of `var` for block scope. `let` is used for variables that may change, while `const` is for constants.
- **Data Types**: Understand the basic data types: `undefined`, `null`, `boolean`, `number`, `string`, `object`, and `symbol`.
- **Type Coercion**: JavaScript automatically converts data types. Understand how type coercion works with `==` (abstract equality) and `===` (strict equality).
- **Primitive data types**: are basic, immutable values stored directly in memory (stack). **Example:** Number, String, Boolean, Undefined, Null, Symbol, BigInt
- **Non-Primitive Data Types**: are reference types, stored in the heap, and mutable.  **Example:** Object, Array, Function, Date, RegExp, Map, Set, WeakMap, WeakSet

## Functions

### Function Declarations and Expressions:
- **Function Declarations**: These are hoisted to the top of their scope, meaning they can be called before they are defined in the code. 
  - **Example**: Function declaration:
    ```javascript
    function greet() {
      console.log('Hello');
    }
    ```
  - **Usage**: Useful for defining functions that need to be accessible throughout a given scope.

- **Function Expressions**: These are not hoisted, so they cannot be called before they are defined.
  - **Example**: Function expression:
    ```javascript
    const greet = function() {
      console.log('Hello');
    };
    ```
  - **Usage**: Often used when functions need to be conditionally defined or passed as arguments.

### Arrow Functions:
- **Syntax**: Provide a shorter, more concise way to write functions, and lexically bind the `this` value.
  - **Example**: Arrow function syntax:
    ```javascript
    const add = (a, b) => a + b;
    // add(4,5)  -> 9
    ```
  - **Key Characteristics**:
    - **Shorter syntax**: Especially for simple functions.
    - **No own `this` context**: `this` is lexically inherited from the parent scope.
    - **Cannot be used as constructors**: Arrow functions do not have their own `this` context.

### Higher-Order Functions:
- **Definition**: Functions that take other functions as arguments or return them as results.
  - **Examples**: `map`, `filter`, `reduce`.
  - **Usage**: Higher-order functions enable more abstract and concise ways of working with data.


## Objects and Arrays

### Object Literals
- **Creation and Modification**: Understand how to create objects using literal syntax and how to access/modify their properties.
  - **Example**: Creating and modifying object properties:
    ```javascript
    const person = {
      name: 'John',
      age: 30
    };
    person.name = 'Jane'; // Modifying property
    person['age'] = 25;   // Another way to modify property
    ```

- **Important Methods**:
  - **`Object.keys`**: Returns an array of a given object's own enumerable property names.
    ```javascript
    const keys = Object.keys(person);
    // ['name', 'age']
    ```
  - **`Object.values`**: Returns an array of a given object's own enumerable property values.
    ```javascript
    const values = Object.values(person);
    // ['Jane', 25]
    ```
  - **`Object.entries`**: Returns an array of a given object's own enumerable property [key, value] pairs.
    ```javascript
    const entries = Object.entries(person);
    // [['name', 'Jane'], ['age', 25]]
    ```
  - **`Object.assign`**: Copies all enumerable own properties from one or more source objects to a target object.
    ```javascript
    const target = {};
    const source = { name: 'Alice' };
    Object.assign(target, source); // target now has { name: 'Alice' }
    ```

- **Making Objects Immutable**:
  - **Object.freeze**: Prevents the modification of existing property attributes and values, and prevents new properties from being added.
    ```javascript
    const frozenObject = Object.freeze(person);
    frozenObject.age = 40; // This will not change the age property
    ```
   -  **Object.seal**
		- **Purpose**: Prevents new properties from being added to an object and marks all existing properties as non-configurable.
		- **Key Points**:
		  - **Non-configurable**: Existing properties cannot be deleted or reconfigured.
		  - **Modifiable values**: Existing properties can still be modified.

	- **Object.preventExtensions**
		- **Purpose**: Prevents new properties from being added to an object.
		- **Key Points**:
		  - **No new properties**: New properties cannot be added.
		  - **Modifiable and deletable values**: Existing properties can be modified or deleted.

### Array Methods
- **Important Methods**: `push`, `pop`, `shift`, `unshift`, `map`, `filter`, `reduce`, `forEach`, and `find`.
  - **`push`**: Adds one or more elements to the end of an array.
    ```javascript
    const arr = [1, 2, 3];
    arr.push(4); // [1, 2, 3, 4]
    ```
  - **`pop`**: Removes the last element from an array.
    ```javascript
    arr.pop();
    // [1, 2, 3]
    ```
  - **`shift`**: Removes the first element from an array.
    ```javascript
    arr.shift();
    // [2, 3]
    ```
  - **`unshift`**: Adds one or more elements to the beginning of an array.
    ```javascript
    arr.unshift(0);
    // [0, 2, 3]
    ```
  - **`map`**: Creates a new array with the results of calling a provided function on every element in the calling array.
    ```javascript
    const doubled = arr.map(x => x * 2);
    // [0, 4, 6]
    ```
  - **`filter`**: Creates a new array with all elements that pass the test implemented by the provided function.
    ```javascript
    const even = arr.filter(x => x % 2 === 0);
    // [0, 2]
    ```
  - **`reduce`**: Executes a reducer function (that you provide) on each element of the array, resulting in a single output value.
    ```javascript
    const sum = arr.reduce((acc, curr) => acc + curr, 0);
    // 5
    ```
  - **`forEach`**: Executes a provided function once for each array element. **Note:** `forEach` cannot be stopped or broken in the middle, unlike a `for` loop.
    ```javascript
    arr.forEach(x => console.log(x));
    // 0, 2, 3
    ```
  - **`find`**: Returns the value of the first element in the provided array that satisfies the provided testing function.
    ```javascript
    const found = arr.find(x => x > 1);
    // 2
    ```

## Prototypes and Inheritance

### Prototype Chain
- **Concept**: Every JavaScript object has a prototype. All objects inherit properties and methods from their prototype.
- **Prototype Chain**: The lookup for properties and methods follows the prototype chain until the property/method is found or the end of the chain is reached.
  - **Example**: Creating prototypes and inheritance.
    ```javascript
    function Person(name) {
      this.name = name;
    }

    Person.prototype.greet = function() {
      console.log('Hello, ' + this.name);
    };

    const john = new Person('John');
    john.greet(); // Hello, John
    ```

### ES6 Classes
- **Syntax**: Provides a more concise and readable syntax for creating objects and dealing with inheritance.
  - **Example**: Using ES6 classes and inheritance.
    ```javascript
    class Person {
      constructor(name) {
        this.name = name;
      }

      greet() {
        console.log('Hello, ' + this.name);
      }
    }

    class Employee extends Person {
      constructor(name, job) {
        super(name);
        this.job = job;
      }

      work() {
        console.log(this.name + ' is working as a ' + this.job);
      }
    }

    const alice = new Employee('Alice', 'developer');
    alice.greet(); // Hello, Alice
    alice.work();  // Alice is working as a developer
    ```

- **Key Features**:
  - **`class` keyword**: Defines a class.
  - **Constructor**: A method for creating and initializing objects.
  - **Inheritance**: `extends` keyword creates a subclass.
  - **`super` keyword**: Calls the constructor of the parent class.

### Additional Notes on Prototypal Inheritance
- **Prototype Methods**: Methods added to a constructor’s prototype ensure all instances share the same method.
- **Prototype Chain Lookup**: JavaScript looks on the instance first, then up the prototype chain for properties/methods.
- **`__proto__` vs `Object.getPrototypeOf`**: `__proto__` can access the internal `[[Prototype]]` property, but `Object.getPrototypeOf` is preferred.


## ES6 Features

### Arrow Functions
- Arrow functions provide a shorter syntax and lexically bind the `this` value (Example: Arrow function).

### Template Literals
- Template literals allow for easier string interpolation using backticks (Example: String interpolation with template literals).

### Destructuring
- Destructuring allows for unpacking values from arrays or properties from objects into distinct variables (Example: Array and object destructuring).

### Default Parameters
- Default parameters allow you to specify default values for function parameters (Example: Function default parameters).

### Rest and Spread Operators
- The rest operator (`...`) allows you to represent an indefinite number of arguments as an array.
- The spread operator (`...`) allows an iterable to expand in places where multiple arguments or elements are expected (Example: Using rest and spread operators).

### Promises
- Promises provide a way to handle asynchronous operations. They have `then`, `catch`, and `finally` methods (Example: Using promises for asynchronous operations).

### Modules
- ES6 introduced a module system to export and import functionalities (Example: Exporting and importing modules).
