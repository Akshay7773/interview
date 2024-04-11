

## Q.1 Why it is called javascript ? is java and  javascript are same ? 
When it was created it is known as livescript , but at that time java was very popular so later it is named as javascript. 

There is no relation between Java and JS, both are totally different languages.


<br> 

## Q.2 what is javascript ?
JavaScript is a programming language used to make websites more interactive and dynamic. It's like the glue that holds web pages together. With JavaScript,
you can create things like pop-up messages, interactive forms, animations, and much more. It's also used on the server side to build web applications.
JavaScript is popular because it's easy to learn and works on all web browsers.


<br> 


## Q.3 Data Types in javascript: 
Primitive:  Stores only single value

Number , string, boolean, null, undefined, BigInt, Symbol.

Non-primitive:  Stores multiple values 

Object , Array

In JavaScript, there are primitive data types and non-primitive (or reference) data types. Here's a breakdown of the differences between them:

1. **Primitive Data Types**:
    - Primitive data types are immutable, meaning their values cannot be changed directly.
    - They are stored directly in memory and are accessed by their value.
    - There are six primitive data types in JavaScript:
        - `Number`: Represents numeric values, including integers and floating-point numbers.
        - `String`: Represents sequences of characters, enclosed in single or double quotes.
        - `Boolean`: Represents true or false values.
        - `Null`: Represents the intentional absence of any value.
        - `Undefined`: Represents a variable that has been declared but has not been assigned a value.
        - `Symbol`: Represents unique identifiers, introduced in ECMAScript 6.
2. **Non-primitive (Reference) Data Types**:
    - Non-primitive data types are mutable, meaning their values can be changed directly.
    - They are stored by reference, meaning the variable holds a reference to the memory location where the data is stored.
    - There are three main non-primitive data types in JavaScript:
        - `Object`: Represents a collection of key-value pairs, where keys are strings and values can be of any data type, including other objects.
        - `Array`: Represents a collection of elements, which can be of any data type, accessed by numeric indices.
        - `Function`: Represents a reusable block of code that can be called with different arguments.

Here's an example to illustrate the difference between primitive and non-primitive data types in JavaScript:

```jsx
// Primitive data types
let num = 10;
let str = "Hello";
let bool = true;

// Non-primitive data types
let obj = { name: "John", age: 30 }; // Object
let arr = [1, 2, 3]; // Array
function greet() { console.log("Hello!"); } // Function

// Changing values of non-primitive types
obj.name = "Jane"; // Modify object property
arr.push(4); // Add element to array

```

In this example, changes made to the `obj` object and the `arr` array directly modify their values because they are non-primitive data types and are mutable. However, changes cannot be made directly to primitive data types like `num`, `str`, and `bool`.

<br> 

