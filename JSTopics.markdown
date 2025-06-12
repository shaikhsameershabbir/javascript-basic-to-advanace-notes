# JavaScript and TypeScript Cheatsheet

This cheatsheet is a comprehensive reference for JavaScript and TypeScript, tailored for js JS developers By shaikhsameershabbir [Gitgub](https://duckduckgo.com "View Github Account"),[Linkdin](https://www.linkedin.com/in/shaikh-sameer07/). It covers concepts from basic to expert levels, with detailed explanations, practical examples, and advanced topics like Promises, as requested. The content is designed for interview preparation and knowledge consolidation, emphasizing why primitive data types are primitive and including additional depth for clarity.

## Table of Contents

1. [Fundamentals](#fundamentals)
2. [Arrays and Objects](#arrays-and-objects)
3. [Asynchronous Programming](#asynchronous-programming)
4. [DOM Manipulation](#dom-manipulation)
5. [Advanced Concepts](#advanced-concepts)
6. [ES6+ Features](#es6-features)
7. [Performance and Optimization](#performance-and-optimization)
8. [Functional Programming](#functional-programming)
9. [Web APIs](#web-apis)
10. [Testing](#testing)
11. [TypeScript](#typescript)
12. [Interview Preparation](#interview-preparation)

## Fundamentals

### Variables

- **`var`**: Function-scoped, hoisted to the top of the function or global scope with `undefined`, can be redeclared and reassigned. Prone to errors due to hoisting.
  - Example:
    ```javascript
    console.log(a); // undefined
    var a = 10;
    console.log(a); // 10
    ```
- **`let`**: Block-scoped, not hoisted (throws ReferenceError if used before declaration), can be reassigned but not redeclared in the same scope.
  - Example:
    ```javascript
    if (true) {
      let b = 20; // Only accessible in this block
    }
    console.log(b); // ReferenceError
    ```
- **`const`**: Block-scoped, not hoisted, must be initialized, cannot be reassigned (but object properties are mutable).
  - Example:
    ```javascript
    const c = 30;
    c = 40; // TypeError
    const obj = { key: "value" };
    obj.key = "newValue"; // Allowed
    ```

### Data Types

- **Primitive Data Types**: Basic, immutable types stored by value, optimized for performance.
  - **Number**: Represents integers and floating-point numbers.
    - Example: `let age = 25.5;`
  - **String**: Sequences of characters, enclosed in quotes.
    - Example: `let name = "Alice";`
  - **Boolean**: Represents `true` or `false`.
    - Example: `let isStudent = true;`
  - **Undefined**: Indicates an uninitialized variable.
    - Example: `let x; console.log(x); // undefined`
  - **Null**: Represents intentional absence of value.
    - Example: `let y = null;`
  - **Symbol**: Unique, immutable identifiers (ES6+).
    - Example: `let id = Symbol('id');`
  - **BigInt**: For integers beyond Number limits (ES2020+).
    - Example: `let largeNum = 12345678901234567890n;`
  - **Why Primitive?**
    - **Immutability**: Values cannot be altered (e.g., `let str = "hello"; str[0] = "H";` does not change `str`).
    - **Stored by Value**: Each variable holds its own copy, preventing unintended side effects.
    - **No Methods**: Primitives lack methods (strings use temporary String objects for methods like `.toUpperCase()`).
    - **Performance**: Direct memory access makes operations faster than with objects.
- **Objects**: Complex types stored by reference, mutable 起点

- **Objects**: Complex types stored by reference, mutable, and include arrays, functions, dates, etc.
  - Example: `let obj = { key: "value" }; let ref = obj; ref.key = "new"; console.log(obj.key); // "new"`

### Operators

- **Arithmetic**: `+`, `-`, `*`, `/`, `%`, `**` (exponentiation).
  - Example: `let power = 2 ** 3; // 8`
- **Comparison**: `==` (loose equality), `===` (strict equality), `!=`, `!==`, `>`, `<`, `>=`, `<=`.
  - Example: `console.log(5 == "5"); // true`, `console.log(5 === "5"); // false`
- **Logical**: `&&`, `||`, `!`.
  - Example: `let result = true && false; // false`
- **Assignment**: `=`, `+=`, `-=`, `*=`, `/=`.
  - Example: `let x = 10; x += 5; // x = 15`
- **Ternary**: `condition ? expr1 : expr2`.
  - Example: `let status = age > 18 ? "Adult" : "Minor";`

### Control Structures

- **If-Else**:
  ```javascript
  if (x > 10) {
    console.log("Greater");
  } else {
    console.log("Less or equal");
  }
  ```
- **Switch**:
  ```javascript
  switch (day) {
    case "Monday":
      console.log("Start of week");
      break;
    default:
      console.log("Other day");
  }
  ```
- **Loops**:
  - **For**: `for (let i = 0; i < 5; i++) { console.log(i); }`
  - **While**: `while (x > 0) { x--; }`
  - **Do-While**: `do { console.log(x); } while (x > 0);`
  - **For...of**: Iterates over iterable objects (e.g., arrays).
    - Example: `for (let value of [1, 2, 3]) { console.log(value); }`
  - **For...in**: Iterates over enumerable properties of an object.
    - Example: `for (let key in obj) { console.log(key, obj[key]); }`

### Functions

- **Declaration**: Hoisted, can be called before definition.
  ```javascript
  function greet(name) {
    return `Hello, ${name}`;
  }
  greet("Alice"); // Hello, Alice
  ```
- **Expression**: Not hoisted, assigned to a variable.
  ```javascript
  const add = function (a, b) {
    return a + b;
  };
  ```
- **Arrow Functions**: Concise, lexical `this`, not suitable as constructors.
  ```javascript
  const multiply = (a, b) => a * b;
  ```
- **Differences**:
  - Declarations are hoisted; expressions and arrows are not.
  - Arrow functions inherit `this` from their lexical scope, unlike regular functions.
  - Example:
    ```javascript
    const obj = {
      name: "Alice",
      regular: function () {
        console.log(this.name);
      },
      arrow: () => {
        console.log(this.name);
      },
    };
    obj.regular(); // Alice
    obj.arrow(); // undefined (this is window/global)
    ```

### Scope and Closures

- **Scope**:
  - **Global Scope**: Variables accessible everywhere.
  - **Function Scope**: Variables defined within functions.
  - **Block Scope**: Variables defined with `let` or `const` within `{}`.
  - Example:
    ```javascript
    let globalVar = "global";
    function test() {
      let localVar = "local";
      if (true) {
        let blockVar = "block";
      }
      console.log(blockVar); // ReferenceError
    }
    ```
- **Closures**: Functions that retain access to their lexical scope after the outer function returns.
  - Example:
    ```javascript
    function outer() {
      let count = 0;
      return function inner() {
        count++;
        return count;
      };
    }
    const increment = outer();
    console.log(increment()); // 1
    console.log(increment()); // 2
    ```
  - **Use Cases**: Data encapsulation, private variables, event handlers.

## Arrays and Objects

### Arrays

- **Creation**: `let arr = [1, 2, 3];` or `let arr = new Array(1, 2, 3);`
- **Methods**:
  - **Mutating**: `push()`, `pop()`, `shift()`, `unshift()`, `splice()`, `sort()`.
  - **Non-mutating**: `map()`, `filter()`, `reduce()`, `find()`, `slice()`, `concat()`, `join()`, `includes()`.
  - Example:
    ```javascript
    let numbers = [1, 2, 3];
    numbers.push(4); // [1, 2, 3, 4]
    let doubled = numbers.map((n) => n * 2); // [2, 4, 6, 8]
    let sum = numbers.reduce((acc, val) => acc + val, 0); // 10
    ```
- **Iteration**:
  - `forEach()`: Executes a function for each element.
  - Example: `numbers.forEach(n => console.log(n));`

### Objects

- **Creation**: `let obj = { key: "value" };` or `let obj = new Object();`
- **Accessing Properties**: `obj.key` or `obj["key"]`.
- **Methods**: `Object.keys()`, `Object.values()`, `Object.entries()`, `Object.assign()`, `Object.freeze()`.
  - Example:
    ```javascript
    let user = { name: "Alice", age: 25 };
    console.log(Object.keys(user)); // ["name", "age"]
    Object.assign(user, { city: "New York" }); // Adds city
    ```
- **Property Descriptors**: `Object.defineProperty()` for controlling property behavior (writable, enumerable, configurable).
  - Example:
    ```javascript
    Object.defineProperty(user, "name", { writable: false });
    user.name = "Bob"; // Fails silently
    ```

### Destructuring

- **Array Destructuring**: Assigns elements to variables.
  - Example: `const [a, b] = [1, 2]; // a = 1, b = 2`
- **Object Destructuring**: Assigns properties to variables.
  - Example: `const { name, age } = user; // name = "Alice", age = 25`
- **Nested Destructuring**:
  - Example: `const { address: { city } } = { address: { city: "New York" } };`

### Spread and Rest Operators

- **Spread**: Expands iterables or object properties.
  - Example: `let newArr = [...arr, 4, 5]; // [1, 2, 3, 4, 5]`
  - Example: `let newObj = { ...user, city: "New York" };`
- **Rest**: Collects remaining elements or properties.
  - Example: `function sum(...numbers) { return numbers.reduce((a, b) => a + b, 0); }`

## Asynchronous Programming

### Callbacks

- Functions passed as arguments to handle asynchronous operations.
- **Issue**: Can lead to callback hell (nested callbacks).
- Example:
  ```javascript
  setTimeout(() => console.log("Delayed"), 1000);
  ```

### Promises

- Objects representing the eventual completion or failure of an async operation.
- **Creating**: `new Promise((resolve, reject) => {...})`.
  - Example:
    ```javascript
    const promise = new Promise((resolve, reject) => {
      setTimeout(() => resolve("Success"), 1000);
    });
    ```
- **States**: Pending, Fulfilled, Rejected.
- **Methods**:
  - `.then(onFulfilled, onRejected)`: Handles resolved or rejected states.
  - `.catch(onRejected)`: Handles errors.
  - `.finally(onFinally)`: Runs regardless of outcome.
  - Example:
    ```javascript
    promise
      .then((result) => console.log(result)) // Success
      .catch((err) => console.error(err))
      .finally(() => console.log("Done"));
    ```
- **Chaining**: Allows sequential async operations.
  - Example:
    ```javascript
    promise
      .then((result) => fetch("https://api.example.com/data"))
      .then((response) => response.json())
      .then((data) => console.log(data));
    ```
- **Promise.all**: Resolves when all promises resolve or rejects on first rejection.
  - Example: `Promise.all([promise1, promise2]).then(results => console.log(results));`
- **Promise.race**: Resolves or rejects with the first settled promise.
  - Example: `Promise.race([promise1, promise2]).then(result => console.log(result));`

### Async/Await

- Syntactic sugar for promises, improving readability.
- **async function**: Always returns a promise.
- **await**: Pauses execution until the promise resolves (only in async functions).
- Example:
  ```javascript
  async function fetchData() {
    try {
      const response = await fetch("https://api.example.com/data");
      const data = await response.json();
      return data;
    } catch (error) {
      console.error(error);
    }
  }
  ```
- **Parallel Execution**: Use `Promise.all` with `await`.
  - Example:
    ```javascript
    const [data1, data2] = await Promise.all([fetch(url1), fetch(url2)]);
    ```

### Event Loop

- Manages asynchronous tasks using the call stack, callback queue, and microtask queue.
- **Components**:
  - **Call Stack**: Tracks function execution (LIFO).
  - **Callback Queue**: Holds callbacks from Web APIs (e.g., `setTimeout`).
  - **Microtask Queue**: Higher-priority queue for promises.
- Example:
  ```javascript
  console.log("Start");
  setTimeout(() => console.log("Timeout"), 0);
  Promise.resolve().then(() => console.log("Promise"));
  console.log("End");
  // Output: Start, End, Promise, Timeout
  ```
- **Explanation**: The event loop processes the microtask queue before the callback queue, ensuring promises resolve before timers.

## DOM Manipulation

### Selecting Elements

- `document.getElementById("id")`: Selects an element by ID.
- `document.querySelector(".class")`: Selects the first matching element.
- `document.querySelectorAll("tag")`: Selects all matching elements.
  - Example: `const buttons = document.querySelectorAll("button");`

### Modifying Elements

- `element.innerHTML`: Sets or gets HTML content.
- `element.style.property`: Modifies CSS properties.
- `element.setAttribute("attr", "value")`: Sets attributes.
  - Example:
    ```javascript
    const button = document.querySelector("#myButton");
    button.innerHTML = "Click Me";
    button.style.color = "blue";
    ```

### Events

- `element.addEventListener("event", handler)`: Attaches event listeners.
- Common events: `click`, `submit`, `keydown`, `mouseover`, `mouseout`, `change`.
- **Event Propagation**: Capturing (top-down) and bubbling (bottom-up).
  - Example:
    ```javascript
    button.addEventListener("click", () => alert("Button clicked!"));
    ```

## Advanced Concepts

### Prototypes and Inheritance

- Every object has a prototype, enabling inheritance via the prototype chain.
- **Prototype Chain**: Properties/methods are looked up in the object and its prototype chain.
- Example:
  ```javascript
  function Person(name) {
    this.name = name;
  }
  Person.prototype.greet = function () {
    return `Hello, ${this.name}`;
  };
  const person = new Person("Alice");
  console.log(person.greet()); // Hello, Alice
  ```

### Classes and OOP

- ES6 classes provide syntactic sugar for prototype-based inheritance.
- **Class Declaration**:
  ```javascript
  class Animal {
    constructor(name) {
      this.name = name;
    }
    speak() {
      return `${this.name} makes a sound`;
    }
  }
  ```
- **Inheritance**: Uses `extends` and `super`.
  ```javascript
  class Dog extends Animal {
    constructor(name, breed) {
      super(name);
      this.breed = breed;
    }
    speak() {
      return `${this.name} barks`;
    }
  }
  const dog = new Dog("Rex", "Labrador");
  console.log(dog.speak()); // Rex barks
  ```

### Modules

- **CommonJS**: Used in Node.js with `require()` and `module.exports`.
  - Example: `const module = require("./module");`
- **ES6 Modules**: Use `import` and `export` for browser and modern Node.js.
  - Example:
    ```javascript
    // math.js
    export const add = (a, b) => a + b;
    // main.js
    import { add } from "./math.js";
    console.log(add(2, 3)); // 5
    ```

### Error Handling

- `try/catch/finally`: Handles synchronous and async errors.
- `throw`: Creates custom errors.
- **Error Types**: `Error`, `TypeError`, `ReferenceError`, etc.
  - Example:
    ```javascript
    try {
      throw new Error("Custom error");
    } catch (error) {
      console.error(error.message); // Custom error
    } finally {
      console.log("Cleanup");
    }
    ```

### Regular Expressions

- Patterns for string matching and manipulation.
- **Modifiers**: `g` (global), `i` (case-insensitive), `m` (multiline).
- **Metacharacters**: `.` (any character), `\d` (digit), `\s` (whitespace).
- **Quantifiers**: `*` (0 or more), `+` (1 or more), `?` (0 or 1).
- Example:
  ```javascript
  const regex = /\d+/g;
  console.log("Hello123World456".match(regex)); // ["123", "456"]
  ```

### Event Loop, Call Stack, and Memory Heap

- **Call Stack**: Tracks function execution (last-in, first-out).
  - Example:
    ```javascript
    function a() {
      b();
    }
    function b() {
      console.log("b");
    }
    a(); // Call stack: a -> b
    ```
- **Memory Heap**: Stores objects and manages memory via garbage collection.
  - **Garbage Collection**: Uses mark-and-sweep to reclaim unused memory.
  - Example: `let obj = { key: "value" }; obj = null; // Eligible for garbage collection`
- **Event Loop**: Processes callback and microtask queues when the call stack is empty.
  - Example: See Event Loop example above.

### The `this` Keyword

- Determined by how a function is called.
- **Bindings**:
  - **Default**: `this` is the global object (`window` in browsers).
  - **Implicit**: `this` is the object calling the method.
  - **Explicit**: `this` is set using `call()`, `apply()`, or `bind()`.
  - **New**: `this` is the newly created object in a constructor.
  - **Arrow Functions**: `this` is lexically bound.
  - Example:
    ```javascript
    const obj = {
      name: "Alice",
      sayName: function () {
        console.log(this.name);
      },
      arrowSayName: () => {
        console.log(this.name);
      },
    };
    obj.sayName(); // Alice
    obj.arrowSayName(); // undefined
    ```

### Call, Apply, and Bind

- **Call**: Invokes a function with a specified `this` and arguments.
  - Example: `fn.call(obj, arg1, arg2);`
- **Apply**: Similar to `call`, but takes arguments as an array.
  - Example: `fn.apply(obj, [arg1, arg2]);`
- **Bind**: Returns a new function with a fixed `this`.
  - Example:
    ```javascript
    const boundFn = fn.bind(obj);
    boundFn(); // Uses obj as this
    ```

## ES6+ Features

### Template Literals

- String interpolation with backticks and `${}`.
- Example: `const name = "Alice"; console.log(`Hello, ${name}!`); // Hello, Alice!`

### Default Parameters

- Set default values for function parameters.
- Example: `function greet(name = "Guest") { return `Hello, ${name}`; }`

### Optional Chaining

- Safely accesses nested properties.
- Example: `const city = user?.address?.city; // undefined if not found`

### Nullish Coalescing

- Provides a default for `null` or `undefined`.
- Example: `const value = null ?? "default"; // default`

### Sets and Maps

- **Set**: Collection of unique values.
  - Example: `const mySet = new Set([1, 2, 2, 3]); console.log(mySet.size); // 3`
- **Map**: Key-value pairs with any key type.
  - Example: `const myMap = new Map(); myMap.set("key", "value"); console.log(myMap.get("key")); // value`

### WeakSet and WeakMap

- **WeakSet**: Stores objects, allows garbage collection if no other references exist.
  - Example: `const ws = new WeakSet(); ws.add({});`
- **WeakMap**: Stores key-value pairs, keys are objects, allows garbage collection.
  - Example: `const wm = new WeakMap(); wm.set({}, "value");`

### Proxy and Reflect

- **Proxy**: Intercepts and customizes operations on objects.
  - Example:
    ```javascript
    const target = { name: "Alice" };
    const proxy = new Proxy(target, {
      get(target, prop) {
        return target[prop] || "Unknown";
      },
    });
    console.log(proxy.name); // Alice
    console.log(proxy.age); // Unknown
    ```
- **Reflect**: Provides methods for interceptable operations.
  - Example: `Reflect.get(target, "name"); // Alice`

### Generators

- Functions that can pause and resume execution using `yield`.
- Example:
  ```javascript
  function* generator() {
    yield 1;
    yield 2;
    return 3;
  }
  const gen = generator();
  console.log(gen.next().value); // 1
  console.log(gen.next().value); // 2
  ```

## Performance and Optimization

### Memoization

- Caches function results to avoid redundant computations.
- Example:
  ```javascript
  const memoize = (fn) => {
    const cache = {};
    return (...args) => {
      const key = JSON.stringify(args);
      return cache[key] || (cache[key] = fn(...args));
    };
  };
  const expensiveFn = memoize((n) => n * 2);
  ```

### Debouncing and Throttling

- **Debouncing**: Delays function execution until after a pause.
  - Example:
    ```javascript
    function debounce(fn, delay) {
      let timeout;
      return (...args) => {
        clearTimeout(timeout);
        timeout = setTimeout(() => fn(...args), delay);
      };
    }
    ```
- **Throttling**: Limits function execution to a fixed interval.
  - Example:
    ```javascript
    function throttle(fn, limit) {
      let inThrottle;
      return (...args) => {
        if (!inThrottle) {
          fn(...args);
          inThrottle = true;
          setTimeout(() => (inThrottle = false), limit);
        }
      };
    }
    ```

### Web Workers

- Run scripts in background threads for parallel processing.
- Example:
  ```javascript
  const worker = new Worker("worker.js");
  worker.postMessage("Start");
  worker.onmessage = (e) => console.log(e.data);
  ```

### Garbage Collection

- Uses mark-and-sweep to reclaim unused memory.
- **Avoiding Memory Leaks**: Dereference unused objects, avoid global variables.
- Example: `let obj = { key: "value" }; obj = null; // Allows garbage collection`

## Functional Programming

### Higher-Order Functions

- Functions that take or return functions.
- Example:
  ```javascript
  const numbers = [1, 2, 3];
  numbers.forEach((num) => console.log(num));
  ```

### Currying

- Transforms a function with multiple arguments into a sequence of single-argument functions.
- Example:
  ```javascript
  const curryAdd = (a) => (b) => a + b;
  const add5 = curryAdd(5);
  console.log(add5(3)); // 8
  ```

### Pure Functions

- Functions with no side effects, producing consistent output for the same input.
- Example:
  ```javascript
  const add = (a, b) => a + b; // Pure
  let x = 0;
  const impureAdd = (a) => (x += a); // Impure
  ```

## Web APIs

### Fetch API

- Makes HTTP requests and returns promises.
- Example:
  ```javascript
  fetch("https://api.example.com/data")
    .then((response) => response.json())
    .then((data) => console.log(data))
    .catch((error) => console.error(error));
  ```

### Web Storage

- **localStorage**: Persists data with no expiration.
  - Example: `localStorage.setItem("key", "value"); console.log(localStorage.getItem("key")); // value`
- **sessionStorage**: Persists data for the session.
  - Example: `sessionStorage.setItem("key", "value");`

### Cookies

- Store small data in the browser.
- Example:
  ```javascript
  document.cookie = "username=John Doe; expires=Thu, 18 Dec 2025
  ```
