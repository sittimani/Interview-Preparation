## JavaScript Interview Questions

### 1. Debouncing and Throttling
- Debouncing and throttling are techniques used to optimize event handlers and functions that are called frequently.
- **Debouncing:** ****Delays the execution of a function**** until a certain period has elapsed since the last time the event was triggered. This is useful for events like input changes, where you want to wait for the user to finish typing before performing an action.
- **Throttling:** Limits the rate at which a function can be called. This is useful for events like scroll events, where you want to limit the number of times the function is called per second.
Code Examples:

```javascript
// Debouncing
function debounce(func, wait) {
  let timeout;
  return function() {
    clearTimeout(timeout);
    timeout = setTimeout(() => {
      func.apply(this, arguments);
    }, wait);
  };
}

// Throttling
function throttle(func, limit) {
  let last = 0;
  return function() {
    let now = Date.now();
    if (now - last >= limit) {
      last = now;
      func.apply(this, arguments);
    }
  };
}
```
- **Use Cases:**
	- **Debouncing:** Search input, form validation, window resize.
	- **Throttling:** Scroll events, mousemove events, animations.


### 2.  Hoisting
- Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their scope before code execution.
	- Variable declarations: Are hoisted but initialized with undefined.
	- Function declarations: Are hoisted completely, including the function body. **Note:** Arrow function is not hoisted.


```javascript
console.log(x); // Output: undefined
var x = 10;

greet(); // Output: Hello!

function greet() {
  console.log('Hello!');
}
```

**Note:**
- Use const and let to avoid hoisting-related issues.

### 3. Closures
- A closure is a function that has access to variables from its outer (enclosing) function, even after the outer function has returned.

```javascript
function outer() {
  let x = 10;
  return function inner() {
    console.log(x);
  };
}

let closureFunc = outer();
closureFunc(); // Output: 10
```

### 4. Currying
- Currying is a technique of transforming a function that takes multiple arguments into a chain of functions that each take a single argument.

```javascript
function add(x) {
  return function(y) {
    return x + y;
  };
}

let add5 = add(5);
console.log(add5(3)); // Output: 8
```
**Benefits:**
- Creates higher-order functions.
- Improves code readability and reusability.

### 5. Use Strict
- The 'use strict' directive introduces stricter rules for JavaScript code.
- **Benefits:**
	- Eliminates some silent errors.
	- mproves code reliability and security.
	- Disallows certain language features that are error-prone.
- Note: To implement use strict for a single function, place the directive at the beginning of the function body.

### 6. Object Immutable
-   **Object.freeze**: Prevents the modification of existing property attributes and values, and prevents new properties from being added.
    ```javascript
    const frozenObject = Object.freeze(person);
    frozenObject.age = 40; // This will not change the age property
    ```

### 7. Call, Bind, and Apply in JavaScript
-  **Call**

	-   Invokes a function immediately and sets the `this` keyword to the provided value.
	-   Accepts arguments as a comma-separated list.
- **Apply**
	-   Similar to call but accepts arguments as an array.

- **Bind**
	-   Creates a new function with a bound `this` value.
	-   Returns a new function that can be called later.

- **Tip:**
	- call -> starts with c then common separated.
	- apply -> stares with a then array.

**Example:**
```javascript
function greet() {
  console.log(`hello ${this.name}`)
}

greet.call({name: 'mani')} // Output: Hello mani
greet.apply({name: 'world')} // Output: Hello world
const newfn = greet.bind({name: 'manikandan'});
newfn() // Output: Hello manikandan
```
