
---



# PROMISES Polyfils : 

```js
// Minimal Promise polyfill with .then and .catch support
(function (global) {
  function MyPromise(executor) {
    var self = this;
    self.state = "pending";
    self.value = undefined;
    self.reason = undefined;
    self.onFulfilledCallbacks = [];
    self.onRejectedCallbacks = [];
    function resolve(value) {
      if (self.state === "pending") {
        self.state = "fulfilled";
        self.value = value;
        self.onFulfilledCallbacks.forEach(function (fn) { fn(value); });
      }
    }
    function reject(reason) {
      if (self.state === "pending") {
        self.state = "rejected";
        self.reason = reason;
        self.onRejectedCallbacks.forEach(function (fn) { fn(reason); });
      }
    }
    try {
      executor(resolve, reject);
    } catch (err) {
      reject(err);
    }
  }

  MyPromise.prototype.then = function (onFulfilled, onRejected) {
    var self = this;
    return new MyPromise(function (resolve, reject) {
      function fulfilledCallback(value) {
        try {
          if (typeof onFulfilled === "function") {
            resolve(onFulfilled(value));
          } else {
            resolve(value);
          }
        } catch (e) {
          reject(e);
        }
      }
      function rejectedCallback(reason) {
        try {
          if (typeof onRejected === "function") {
            resolve(onRejected(reason));
          } else {
            reject(reason);
          }
        } catch (e) {
          reject(e);
        }
      }
      if (self.state === "fulfilled") {
        setTimeout(function () { fulfilledCallback(self.value); }, 0);
      } else if (self.state === "rejected") {
        setTimeout(function () { rejectedCallback(self.reason); }, 0);
      } else {
        self.onFulfilledCallbacks.push(fulfilledCallback);
        self.onRejectedCallbacks.push(rejectedCallback);
      }
    });
  };

  MyPromise.prototype.catch = function (onRejected) {
    return this.then(null, onRejected);
  };

  // Expose MyPromise to the global scope
  global.MyPromise = MyPromise;
})(typeof window !== "undefined" ? window : global);

// Example usage:
var promise = new MyPromise(function(resolve, reject) {
  setTimeout(function() {
    resolve("Hello, world!");
  }, 1000);
});
promise.then(function(value) {
  console.log("Resolved:", value);
}).catch(function(err) {
  console.error("Rejected:", err);
});
```


# Polyfills of call, apply, bind 
Here are simple **polyfills** for `.call()`, `.apply()`, and `.bind()` methods in JavaScript.

These are often asked in interviews to test understanding of JavaScript's `this` and function context handling.

---

## 🔹 `Function.prototype.call` Polyfill

### ✅ Usage: `func.call(thisArg, arg1, arg2, ...)`

```js
Function.prototype.myCall = function(context, ...args) {
  context = context || globalThis; // default to global object (window in browsers)
  
  const fnSymbol = Symbol(); // avoid property name collision
  context[fnSymbol] = this;  // assign function to context

  const result = context[fnSymbol](...args); // invoke function

  delete context[fnSymbol]; // clean up
  return result;
};
```

---

## 🔹 `Function.prototype.apply` Polyfill

### ✅ Usage: `func.apply(thisArg, [argsArray])`

```js
Function.prototype.myApply = function(context, args) {
  context = context || globalThis;
  
  const fnSymbol = Symbol();
  context[fnSymbol] = this;

  const result = Array.isArray(args) ? context[fnSymbol](...args) : context[fnSymbol]();

  delete context[fnSymbol];
  return result;
};
```

---

## 🔹 `Function.prototype.bind` Polyfill

### ✅ Usage: `const boundFunc = func.bind(thisArg, arg1, arg2, ...)`

```js
Function.prototype.myBind = function(context, ...args) {
  const fn = this;

  return function(...newArgs) {
    return fn.apply(context, [...args, ...newArgs]);
  };
};
```

### 🔁 Optional: Bind with `new` support (more accurate)

For a more complete polyfill (like native `bind`), it should handle being used as a constructor:

```js
Function.prototype.myBind = function(context, ...args) {
  const fn = this;

  function boundFunction(...newArgs) {
    // If used with `new`, ignore context and use new instance
    if (this instanceof boundFunction) {
      return new fn(...args, ...newArgs);
    }
    return fn.apply(context, [...args, ...newArgs]);
  }

  // Optional: preserve prototype chain
  boundFunction.prototype = Object.create(fn.prototype);

  return boundFunction;
};
```

---

## ✅ Example Usage

```js
function greet(greeting, punctuation) {
  return `${greeting}, ${this.name}${punctuation}`;
}

const person = { name: "Alice" };

console.log(greet.myCall(person, "Hello", "!")); // "Hello, Alice!"
console.log(greet.myApply(person, ["Hi", "."])); // "Hi, Alice."
const greetAlice = greet.myBind(person, "Hey");
console.log(greetAlice("?")); // "Hey, Alice?"
```

---

Let me know if you want these polyfills explained line-by-line.




## 🟢 Array Methods

### 1. `Array.prototype.forEach`

```js
if (!Array.prototype.forEach) {
  Array.prototype.forEach = function(callback, thisArg) {
    for (var i = 0; i < this.length; i++) {
      if (i in this) callback.call(thisArg, this[i], i, this);
    }
  };
}
```

### 2. `Array.prototype.map`

```js
if (!Array.prototype.map) {
  Array.prototype.map = function(callback, thisArg) {
    var result = [];
    for (var i = 0; i < this.length; i++) {
      if (i in this) result[i] = callback.call(thisArg, this[i], i, this);
    }
    return result;
  };
}
```

### 3. `Array.prototype.filter`

```js
if (!Array.prototype.filter) {
  Array.prototype.filter = function(callback, thisArg) {
    var result = [];
    for (var i = 0; i < this.length; i++) {
      if (i in this && callback.call(thisArg, this[i], i, this)) result.push(this[i]);
    }
    return result;
  };
}
```

### 4. `Array.prototype.includes`

```js
if (!Array.prototype.includes) {
  Array.prototype.includes = function(valueToFind, fromIndex) {
    if (this == null) throw new TypeError('"this" is null or not defined');
    var o = Object(this);
    var len = o.length >>> 0;
    if (len === 0) return false;
    var n = fromIndex | 0;
    var k = Math.max(n >= 0 ? n : len - Math.abs(n), 0);
    while (k < len) {
      if (o[k] === valueToFind || (typeof o[k] === "number" && typeof valueToFind === "number" && isNaN(o[k]) && isNaN(valueToFind))) {
        return true;
      }
      k++;
    }
    return false;
  };
}
```

### 5. `Array.prototype.reduce`

```js
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback, initialValue) {
    if (this == null) throw new TypeError('Array.prototype.reduce called on null or undefined');
    if (typeof callback !== 'function') throw new TypeError(callback + ' is not a function');
    var o = Object(this), len = o.length >>> 0, k = 0, value;

    if (arguments.length >= 2) {
      value = initialValue;
    } else {
      while (k < len && !(k in o)) k++;
      if (k >= len) throw new TypeError('Reduce of empty array with no initial value');
      value = o[k++];
    }

    for (; k < len; k++) {
      if (k in o) value = callback(value, o[k], k, o);
    }
    return value;
  };
}
```

---

## 🟢 String Methods

### 6. `String.prototype.includes`

```js
if (!String.prototype.includes) {
  String.prototype.includes = function(search, start) {
    return this.indexOf(search, start || 0) !== -1;
  };
}
```

### 7. `String.prototype.startsWith`

```js
if (!String.prototype.startsWith) {
  String.prototype.startsWith = function(search, pos) {
    return this.substring(pos || 0, (pos || 0) + search.length) === search;
  };
}
```

### 8. `String.prototype.endsWith`

```js
if (!String.prototype.endsWith) {
  String.prototype.endsWith = function(searchString, position) {
    var subjectString = this.toString();
    if (typeof position !== 'number' || !isFinite(position) || Math.floor(position) !== position || position > subjectString.length)
      position = subjectString.length;
    position -= searchString.length;
    return subjectString.indexOf(searchString, position) !== -1;
  };
}
```

---

## 🟢 Object Methods

### 9. `Object.assign`

```js
if (typeof Object.assign !== 'function') {
  Object.assign = function(target) {
    if (target == null) throw new TypeError('Cannot convert undefined or null to object');
    var to = Object(target);
    for (var i = 1; i < arguments.length; i++) {
      var nextSource = arguments[i];
      if (nextSource != null) {
        for (var nextKey in nextSource) {
          if (Object.prototype.hasOwnProperty.call(nextSource, nextKey)) {
            to[nextKey] = nextSource[nextKey];
          }
        }
      }
    }
    return to;
  };
}
```

### 10. `Object.keys`

```js
if (!Object.keys) {
  Object.keys = function(obj) {
    if (obj !== Object(obj)) throw new TypeError('Object.keys called on a non-object');
    var keys = [], key;
    for (key in obj) {
      if (Object.prototype.hasOwnProperty.call(obj, key)) keys.push(key);
    }
    return keys;
  };
}
```

---

## 🟢 Number & Math

### 11. `Number.isNaN`

```js
if (!Number.isNaN) {
  Number.isNaN = function(value) {
    return typeof value === "number" && isNaN(value);
  };
}
```
In JavaScript, **Promises** are a powerful way to handle asynchronous operations like API calls, timers, or reading files. They represent a value that may be available now, or in the future, or never.

---

## 🔑 What is a Promise?

A **Promise** is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value.

### Promise States:

1. **Pending** – Initial state, neither fulfilled nor rejected.
2. **Fulfilled** – Operation completed successfully.
3. **Rejected** – Operation failed.

---

## 📦 Creating a Promise

```js
const promise = new Promise((resolve, reject) => {
  const success = true;
  if (success) {
    resolve("Operation successful");
  } else {
    reject("Something went wrong");
  }
});
```

---

## ✅ Consuming Promises

```js
promise
  .then(result => {
    console.log(result); // Operation successful
  })
  .catch(error => {
    console.error(error); // Something went wrong
  })
  .finally(() => {
    console.log("Done"); // Runs no matter what
  });
```

---

## 🔁 Promise Methods (Static)

### 1. **`Promise.all(iterable)`**

Waits for **all** promises to be fulfilled, or rejects if any promise rejects.

```js
Promise.all([promise1, promise2])
  .then(results => console.log(results)) // [result1, result2]
  .catch(error => console.error(error));
```

### 2. **`Promise.allSettled(iterable)`**

Waits for **all** promises to settle (either resolved or rejected), and returns an array of results.

```js
Promise.allSettled([promise1, promise2])
  .then(results => console.log(results));
/*
[
  { status: 'fulfilled', value: '...' },
  { status: 'rejected', reason: '...' }
]
*/
```

### 3. **`Promise.race(iterable)`**

Returns a promise that settles as soon as **one** of the promises settles (fulfilled or rejected).

```js
Promise.race([promise1, promise2])
  .then(result => console.log(result))
  .catch(error => console.error(error));
```

### 4. **`Promise.any(iterable)`**

Returns a promise that fulfills as soon as **any** of the promises is fulfilled. If all are rejected, it rejects with an `AggregateError`.

```js
Promise.any([promise1, promise2])
  .then(result => console.log(result))
  .catch(error => console.error(error)); // AggregateError if all fail
```

### 5. **`Promise.resolve(value)`**

Returns a resolved promise with the given value.

```js
Promise.resolve(42).then(console.log); // 42
```

### 6. **`Promise.reject(reason)`**

Returns a rejected promise with the given reason.

```js
Promise.reject("Oops").catch(console.error); // Oops
```

---

## 📌 Use Case Example

```js
function fetchData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(`Data from ${url}`);
    }, 1000);
  });
}

const p1 = fetchData("api/user");
const p2 = fetchData("api/posts");

Promise.all([p1, p2])
  .then(([user, posts]) => {
    console.log(user, posts);
  });
```

---

## Summary Table

| Method                 | Description                                             |
| ---------------------- | ------------------------------------------------------- |
| `Promise.all()`        | Waits for all to fulfill, or rejects fast.              |
| `Promise.allSettled()` | Waits for all to settle, gives results.                 |
| `Promise.race()`       | Settles as soon as one does.                            |
| `Promise.any()`        | Fulfills when any fulfills, rejects only if all reject. |
| `Promise.resolve()`    | Creates a resolved promise.                             |
| `Promise.reject()`     | Creates a rejected promise.                             |

Would you like a visual diagram of how these methods differ?

