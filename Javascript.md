
## Q. What is javascript ? 
JavaScript is a high-level programming language commonly used for creating dynamic and interactive content on websites. Initially developed by Brendan Eich at Netscape in 1995, it has since become one of the most widely used programming languages on the web.

JavaScript allows developers to add functionality to web pages, such as user interaction, form validation, animations, and dynamic content updates, without needing to reload the entire page. It is supported by all modern web browsers and can be used on both the client-side (in the browser) and the server-side (with platforms like Node.js).

JavaScript is known for its versatility and is often used in conjunction with HTML and CSS to create rich, interactive web experiences. It has a large ecosystem of libraries and frameworks, such as React, Angular, and Vue.js, which simplify the development process and provide additional functionality for building complex web applications.

<br> 

## Q.1 Why it is called javascript ? is java and  javascript are same ? 
When it was created it is known as livescript , but at that time java was very popular so later it is named as javascript. 

There is no relation between Java and JS, both are totally different languages.


<br>

<br> 

## Q. What is throttling in javascript ? 

 Throttling is a technique used to control the rate at which a function is executed. It's commonly used to limit the frequency of execution of a function, especially for events that may trigger rapidly, such as scroll or resize events.

Throttling ensures that a function is only executed at most once per specified interval, even if it's called multiple times during that interval. This can be useful for optimizing performance, reducing unnecessary function calls, and preventing overload in event-driven scenarios.

Here's a simple example of how throttling can be implemented in JavaScript:

```javascript
 const throttle = (cb, delay) => {
    let lastcall = 0;

    return function (...args) {
      let now = Date.now();
      if (now - lastcall < delay) return;
      lastcall = now;
      cb.apply(this, args);
    };
  };

// Example usage:
function handleScroll() {
  console.log('Scrolled!');
}

const throttledScroll = throttle(handleScroll, 1000); // Throttle to once per second

// Attach the throttled function to the scroll event
window.addEventListener('scroll', throttledScroll);
```

In this example, the `throttle` function takes a function `func` and a delay `delay` as arguments. It returns a new function that wraps around the original function `func`, ensuring that it's called at most once every `delay` milliseconds. This helps prevent the `handleScroll` function from being called too frequently during scrolling events.

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


## Q.4 What is let , var and const?var, let and const are used to define the variables in javascript.

difference between var , let and const are: 

1. on basis of scope 
2. Hoisting 
3. And uses

1. var : 
    1. var has functional scope.
    2. we can re-initialize value for var type variable
    3. we can redeclare variable with var type
        
        e.g. var a=10, 
        
        var a=10,
        
    4. if we do not give any type to variable then it automatically takes it as var.
    5. variable with var is hoisted in global scope.
    
2. let :
    1. let has block scope
    2. we can re-initialized value of let type
    3. we can not redeclare variable with let type
    4. let is hoisted but in script scope

1. const :
    1. const has block scope.
    2. we can not reinitialized the value of const variable
    3. also we can not redeclare variable with const type
    4. const is also hoisted but in script scope.
  
<br> 

## Q.5 this keyword in javascript
In javascript, this keyword always refers to object.

The thing about it is that the object it refers to will vary depending on how and where this is being called.

some different ways to use this keyword is : 

1. By itself 
2. Inside object method
3. Inside function 

1. By itself: 
    
    it means that it will point to window object.
    
    console.log(this)
    
2. Inside object method: 
    
    e.g. 
    
    const obj={
    
    name:”Akshay”, 
    
     lastname:”Gawade”,
    
    fullname:function(){
    
    return this
    
    }
    
    }
    
    console.log(obj.fullname)
    
    o/p: {name:’Akshay’, lastname:’Gawade’,fullname:f}
    
    if we write [this.name](http://this.name) then it will give Akshay as output
    
    1. Inside function: 
        
        function abc(){
        
        return this;
        
        }
        
        console.log(abc())
        
        o/p: window object


<br>

## Q.6 What is call, apply and bind ? 
1. Call :  
    
	 Call is a function that helps you change the context of the invoking function. In other words it helps you to replace the value of this inside a function with whatever value you want . 
         The call() method calls the function directly and sets this to the first argument passed to the call method and if any other sequences of the arguments precending the first argument are passed to the call method then they are passed as an arugment to the function.
    
    note : call method allows an object to use the method (function) of another object.
    
    Bind and apply works same as call , but the major difference is passing parameters.
    
    e.g. 
    
    const person1={
    
    fname:”Akshay”,
    
    lname:”Gawade”,
    
    fullname:function(location){
    
    return this.fname+” ”+this.lname+” “+location
    
    }
    
    }
    
    const person2={
    
    fname:”Saurabh”,
    
    lname:”Gawade”
    
    }
    
    console.log(person1.fullname.call(person2,”Pune”));
    
    console.log(person1.fullname.apply(person2,[”Pune”]));
    
    let op=person1.fullname.bind(person2,”Pune”);
    
    console.log(op())
    
    NOTE: bind return a function, we need to call that function.



<br> 

## Q.7 What is map, filter and reduce? 
map() :

map is used to creating a new array from existing one, applying a function to each one of the elements of the first array.

**Purpose:** The **`map`** function is used to transform each element of an array based on a provided function and create a new array with the results.

var new_array=arr.map((element, index, array)⇒{

return value for new_array

}) 

filter(): 

if we want to filter some values from array based on some certain condition then we use filter. It will also return new array and not modify original array.

**Purpose:** The **`filter`** function is used to create a new array containing only the elements that satisfy a given condition.

```jsx
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter((num) => num % 2 === 0);
// evenNumbers: [2, 4]
```

reduce():

It returns single value. in this case also it is not modify original array.

**Purpose:** The **`reduce`** function is used to accumulate values from an array into a single result. It applies a provided function against an accumulator and each element in the array (from left to right) to reduce it to a single value.

```jsx
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, num) => accumulator + num, 0);
// sum: 10
```

<br> 

## Q.8 What is promise in javascript ?# Promise::
A promise is a special javascript object. It produces a value after an asynchronous operation completes successfully, or an error if it does not completes successfully due to timeout, network error and so on.

syntax:

let promise =new Promise((resolve, reject)⇒{

//make an asynchronous call and either resolve or reject.

})

** A promise object has following internal properties:

1. State: 
    1. pending: Initially when the executor function starts the execution.
    2. fulfilled: When the promise is resolved. 
    3. rejected: When the promise is rejected. 
    

e.g. 

let promise =new Promise((resolve, reject)=>{
let data=false
if(data){
resolve("resolved ")
}else{
reject("false")
}
})

promise.then((res)=>{
console.log(res)
}).catch(err=>{
console.log(err)
})

NOTE ***********************************************************************************************

WE CAN AVOID WRITING PROMISES USING THIS. 

```jsx

// Example asynchronous function with a callback
function fetchData(callback) {
  // Simulating an asynchronous operation (e.g., fetching data from an API)
  setTimeout(() => {
    const data = "Data fetched successfully";
    callback(null, data); // Pass null for the error parameter and data for the result
  }, 1000);
}

// Usage of the fetchData function with a callback
fetchData((error, result) => {
  if (error) {
    console.error(error);
  } else {
    console.log(result);
  }
});
```

<br>

## Q.9 What is event propagation? 

Event propagation: 

1. Bubbling : event travels from inner  to outer
2. Capturing : event travels from outer to inner 

Event propagation in JavaScript refers to the flow of events through the DOM (Document Object Model) hierarchy. There are two main phases of event propagation: capturing phase and bubbling phase. This process is often referred to as event flow.

1. **Capturing Phase:**
    - During the capturing phase, the event travels from the root of the DOM hierarchy down to the target element.
    - Events start from the outermost ancestor and move towards the target element.
    - This phase allows capturing events on ancestors before reaching the actual target element.
2. **Target Phase:**
    - The event reaches the target element, triggering the event listeners attached to that specific element.
3. **Bubbling Phase:**
    - After the target phase, the event then bubbles up from the target element back to the root of the DOM hierarchy.
    - Event listeners attached to ancestors of the target element can respond to the event during this phase.

NOTE: 

If you want to achieve event capturing in a traditional HTML and JavaScript setup (not using React), you can use the

```
addEventListener
```

method with the

```
useCapture
```

parameter set to

```
true
```

. Here's an example:

```jsx
document.getElementById('outer').addEventListener('click', function() {
  console.log('Capturing Phase - Outer');
}, true);
```


<br> 

## Q.10 find, filter and slice, splice
# 1. find():

it returns only first element which matches the condition. 

It returns only single element not an array.

e.g. 

let arr=[1,2,3,4,5]
let arr2=arr.find(ar=>ar%2==0)
console.log(arr2)

output : 2

note : here 4 also matches the condition but it only returns 2 as output.

# 2. filter():
filter function finds all the elements inside the array which matches the condition. It returns the array with elements which satisfies the condition.

e.g. 

let arr=[1,2,3,4,5]
let arr2=arr.filter(ar=>ar%2==0)
console.log(arr2)

output : 

 [ 2, 4 ]

# 3. slice():
slice method get a subset of the array from start index to end index.

end is not included.

e.g. 

let arr=[1,2,3,4,5,7,8]
let arr2=arr.slice(2,4)
console.log(arr2)

output : 

[ 3, 4 ]

# 4. splice():

          The splice method is used to add, remove or replace elements in an array.

syntax:

array.splice(startIndex, deleteCount, …itemsToAdd)

let arr=["a", "b", "c"]
arr.splice(1,0,"x", "y")

console.log(arr)

output: [ 'a', 'x', 'y', 'b', 'c' ]

NOTE: it changes the original array.


<br> 


## Q.11 push , pop, shift, unshift
# push():
it adds elements to the last position.

# pop():
 it removes last element of the array and return that element.

# shift():
it removes first element of the array and returns that element.

# unshift():

it adds element to the first index of array.

NOTE : 

all methods made changes in original array.


<br> 

## Q.12 map, forEach
# map():
 The map method is used when you want to modify each element of an array and create a new array with modified values.

it returns new array with modified value.

e.g

let arr1=[1,2,3]

let arr2=arr1.map((ar)⇒ar*2)

console.log(arr2)

output: 

[2,4,6]

NOTE : it will not modify original array.

# forEach():
 The forEach method is used when you want to perform some operation on each element of an array without creating new array.

e.g.
```jsx
let arr1=[1,3,4]

arr1.forEach((ar)⇒{

console.log(ar*2);

})
```
output : 2 4 6 

NOTE: it will not modify new array , also it will not return anything.


<br> 


## Q.13 what is Array destructuring? 
# Destructuring:
 Array destructuring allows you to extract elements from an array and assign them to individual variables in a single statement.

it is introduced in ES6

e.g. 
```jsx
let arr=["apple", "banana", "grapes"]
let [f1, f2, f3]=arr
console.log(f1)
console.log(f2)
console.log(f3)
```
output : 

apple 

banana 

grapes



<br> 

## Q.14 what are array like objects? 
### array like objects:

Array like objects are objects that have indexed elements and have length property, similar to arrays , but they may not have all the methods of arrays like push(), pop() and others.

e.g. string

let str=”hello”

console.log(str.length);

console.log(str[2])

```jsx
function sum(){
 console.log(arguments)
 console.log(arguments[1])
}
sum(1,2,3)
```

output : 

[Arguments] { '0': 1, '1': 2, '2': 3 }
2



<br>

## Q.15 what is callback function, higher order function? 
### callback function:
callback function is a function that is passed as an argument of another function.

### higher order function :
function  which take another function as an argument is called as higher order function.

```jsx
function display(x, y, operation) {
  var result = operation(x, y);

  console.log(result);
}

function add(a, b) {
  return a + b;
}

display(10, 5, add);
```

NOTE : here function display is higher order function and operation is callback function.’


<br>


## Q.16 What is parameters and arguments?
# parameters:
parameters are the placeholders defined in the function declaration.

# arguments:
arguments are the actual values passed to the function when it is invoked or called .

 
```jsx
//this is parameters

function add(a,b){

console.log(a, b )

}

add(3,5)   //this is arguments.
```



<br> 

## Q.17 what is first class functions ? 
### First class functions :
 if function treated like another variables  then it is called as first class function.

Functions treated like variables : 

1. Assignable .
2. Passable as arguments .
3. Returnable as values .
```jsx
const myfun=function(){

console.log(”hello”)

}
```



<br> 

## Q.18 what are pure and impure functions ? 
# pure functions :
A pure function is a function that always produces the same output for the same input.

e.g.
```jsx

function add(a,b){

console.log(a+b);

}

fun(4,5)   // output : 9

fun(4, 5)  // output: 9
```

NOTE : here output is same for both the inputs .

# impure functions :
 An impure functions produces different output for the same input

e.g. 
```jsx
let sum=0;
function count(num){
     sum+=num;
      console.log(sum)

}

count(10)   //output : 10
count(10)  // output : 20
```
NOTE : here inputs are same for both function calling but output is different.


<br> 

## Q.19 what is currying in node js ? 
### Currying:
 currying in javascript transforms a function with multiple arguments into a nested  series of functions, each taking a single argument.

e.g. 

```jsx

function fun(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}
console.log(fun(10)(5)(9));

output : 24
```


<br> 


## Q.20 what is DO# DOM : (Document Object Model)
  The DOM represents the web page as a tree like structure that allows javascript to dynamically access and manipulate the content and structure of a web page.

### Selectors in js:
 Selectors in javascript help to get specific elements from DOM based on IDs, class names , tag names .

1. getElementById()
2. getElementsByClassName()
3. getElementsByTagName()
4. querySelector()
5. querySelectorAll()M ? 


<br> 

## Q.21 Error handling in javascript
try

catch 

finally

# throw statement:
  throw statement stops the execution of the current function and passes the error to the catch block of calling function.

e.g.
```jsx

function userData() {
  try {
    validateAge(10);
  } catch (err) {
    console.log(err);
  }
}

function validateAge(a) {
  if (a < 18) {
    throw new Error("Age must be greater than or equal to 18");
  }
}
```
# Error propogation:
 Error propogation refers to the process of passing or propagating an error from one part of the code to another by using the throw statement with try catch .

# Types of errors in js :

1. Syntax error     // console.log(”hello world
2. Reference error // console.log(var1);     //no declaration of variable 
3. Type error     // const number =10 ; number.toUpperCase() // 
4. Range error // let arr=[1,2,3,4] ; console.log(arr[10]) //index out of bounds .


<br> 

## Q.21 What are objects in javascript ?
### OBJECTS IN JAVASCRIPT :
   An object is a data type that allows you to store  key-value pairs .  

OBJECT is a real world entity . 

example of object : 

let person ={

name:”Akshay”, 

hobbies: [”playing cricket”, “watching movies”],

greet:function (){

console.log(”hello world”);

}

}

# CREATING OBJECTS  :

1. OBJECT LITERAL: 
    
    var person : {
    
    name:”Akshay”
    
    }
    
    console.log(person)
    
2. OBJECT CONSTRUCTOR: 
    
    var person = new Object()
    
    person.name=”Akshay”;
    
    person.age=20
    
    consle.log(person)
    
3. OBJECT.CREATE() METHOD : 
    
    var person = {
    
    name:””,
    
    age:0,
    
    }
    
    var men=Object.create(person)
    
    men.name=”Akshay”
    
    men.age=25
    
    console.log(men)
    
    # difference between array and object:
    
    Arrays: 
    
    1. Arrays are collection of values 
    2. Arrays are denoted by [] square brackets 
    3. Elements in array are ordered. 
    
    Objects: 
    
    1. Objects are collection of key-value pairs 
    2. Objects are denoted by {} curly braces.
    3. Properties in objects are unordered.
    
    # COPY OBJECT:
    
    WAYS TO CLONE OR COPY THE OBJECT: 
    
    1. Spread syntax
    2. Object.assignt()
    3. json.parse() & json.stringify()

1. spread syntax: (shallow copy)
    
    const clonedObj={…originalObj}
    
2. Object.assign(): (shallow copy) 
    
    const clonedObj=Object.assign({}, originalObj)
    
3. Json.parse() and json.stringify(): (deep copy) 
    
    const clonedObj=JSON.parse(JSON.stringify(originalObj))
    

# Difference  between Deep copy and Shallow copy in javascript:
   Shallow copy in nested objects case will modify the parent object property value, if cloned object property value is changed. 

But deep copy will not modify the parent object property value

NOTE: SPREAD AND OBJECT.ASSIGN ARE SHALLOW COPY AND json.parse IS A DEEP COPY.

IMP NOTE :  

it will only affected on child object.

### EXAMPLE OF SHALLOW COPY

```jsx
let obj={
  name:"Akshay",
  lastname:"Gawade",
  address:{
      village:"Nandawade",
      current:"Pune"
  }
}

// let obj2=Object.assign({}, obj)
let obj2={...obj}

obj2.address.village="Chandgad"
console.log(obj2)
console.log(obj)
```

HERE address of both the object will change ( i.e. village name changes from Nandawade to Chandgad for both the object i.e. obj and obj2)

### EXMPLE OF DEEP COPY

```jsx
let obj={
  name:"Akshay",
  lastname:"Gawade",
  address:{
      village:"Nandawade",
      current:"Pune"
  }
}

// let obj2=Object.assign({}, obj)
let obj2=JSON.parse(JSON.stringify(obj))

obj2.address.village="Chandgad"
console.log(obj2)
console.log(obj)
```

Here address of just obj2 changes from Nandawade to Chandgad.


<br> 

## Q.22 What are events in javascript ? 
# Events:

Events are actions that happen in the browser, such as button click, mouse movement, or keyboard input.

## types of events:

1. click event
2. mouse over event
3. key down event
4. key up event.
5. focus , blur, change , load , resize.

# Q. What is event object in js? 
  Whenever any event is triggered, the browser automatically creates an event object and passes it as an argument to the event handler function. 

function handleclick(event){

console.log(event)

}

# Event delegation:
 it is a technique where you attach a single event handler to a parent element to handle events on its child element.

1. Event bubbling: 
    
    it is a process where an event triggered on a child element propogates up to the dom tree.
    
2. Event capturing: 
    
    it is the process where an event is handled starting from the root of the dom and moving down to the target element.
    

 

###  Q. 2 What is  the purpose of the event.preventDefault() method in js?

        it is used to prevent the default behaviour of an event and the link click will be prevented.



<br> 


## Q.22 What is memoization in javascript ? 
## Memoization in javascript :
  Memoization is an optimization technique that can be used to reduce time consuming calculations by saving previous input to something called cache and returning the result from it. 

```jsx
function calc(n){
    let sum=0;
    for(let i=1;i<=n;i++){
        sum+=i;
    }
    return sum;
}

// console.time()
// console.log(calc(500000))
// console.timeEnd()

const memoize=(fun)=>{
    let cache={}
    return function (...args){
        let n=args[0]
        if(n in cache){
            console.log("from cache")
            return cache[n];
        }else{
            console.log("first time")
            let result=fun(n)
            cache[n]=result;
            return result
        }
    }
}

let res=memoize(calc)
console.log(res(7))
```

<br> 

## Q.24 what is rest and spread operator in javascript? 
## Rest and Spread operator:
   **Spread operators allow us to expand an array or object into its individual elements, while rest operators allow us to collects multiple elements into a single array or object.**

## Spread operator:
 Spread operators are written using three consecutive dots (...), and they provide us with an easy way to break up an array or an object into its individual elements.

For example, let’s say we have the following array:

```jsx
let array = [1, 2, 3, 4];

```

If we wanted to add a fifth element to our array, we could use the Spread Operator like this:

```jsx
let newArray = [...array, 5];
```

The Spread Operator will take our array, expand it into its individual elements (1, 2, 3, 4), and then add the fifth element (5). The result is a new array that is one element longer than the original:

```jsx
newArray = [1, 2, 3, 4, 5];
```

## Rest operator:
The rest operator is essentially the opposite of the spread operator. It collects multiple elements into an array. This is useful if you don’t know how many arguments a function may receive, and you want to capture all of them as an array.

```jsx
function fun(a, ...rest){
    console.log(rest, a)
}
fun(2,3,4,5)

output : [3,4,5] 2
```

NOTE : 

The spread and rest operators are useful for quickly and easily manipulating collections and arguments. They make code much cleaner and easier to read, as well as reduce the number of lines of code needed.

They’re extremely versatile tools, and every JavaScript programmer should know how to use them.

temporal dead zone

<br> 


## Q.25 What is temporal dead zone? 
## Temporal Dead Zone:
   The **temporal dead zone** (TDZ) is a specific period in the execution of JavaScript code where variables declared with `let` and `const` exist but cannot be accessed or assigned any value. During this phase, accessing or using the variable will result in a `ReferenceError`.

To better understand the TDZ, let’s consider an example:

To better understand the TDZ, let’s consider an example:

!https://miro.medium.com/v2/resize:fit:658/1*eYwRncszhaz7KCea3cg3WQ.png

In the example above, we try to access the variable `x` before its declaration and initialization. This triggers the **TDZ** because the variable exists within the scope but has not been assigned a value yet. As a result, JavaScript throws a `ReferenceError` indicating that the variable `x` cannot be accessed before initialization.

The **TDZ** ends and the variable becomes accessible after its declaration and initialization:

!https://miro.medium.com/v2/resize:fit:650/1*CZislTmLOSOrfWTcWmDaRQ.png

Here, `x` is properly declared and initialized before we attempt to access it, so there is no TDZ violation, and the value of `x` (which is 10) is successfully printed to the console.

Similarly, the **TDZ** applies to `const` variables as well:

!https://miro.medium.com/v2/resize:fit:649/1*lSMSY7SefjjOf4brq0e4EQ.png

In this case, trying to access the `const` variable `y` before its declaration and initialization triggers the TDZ, resulting in a `ReferenceError`.

The TDZ ensures that variables are accessed only after they have been properly declared and initialized, promoting better coding practices and reducing the likelihood of accessing variables in an undefined or uninitialized state.



<br> 

## Q.26 What is pass by value and pass by reference? 
## 1. Pass by value :

- In Pass by value, the function is called by directly passing the value of the variable as an argument. So any changes made inside the function do not affect the original value.
- In Pass by value, parameters passed as arguments create their **own copy.** So any changes made inside the function are made to the copied value not to the original value

**Example:** In this example, we have shown a pass-by value.

```jsx
function Passbyvalue(a, b) {
	let tmp;
	tmp = b;
	b = a;
	a = tmp;
	console.log(`Inside Pass by value 
		function -> a = ${a} b = ${b}`);
}

let a = 1;
let b = 2;
console.log(`Before calling Pass by value 
		Function -> a = ${a} b = ${b}`);

Passbyvalue(a, b);

console.log(`After calling Pass by value 
	Function -> a =${a} b = ${b}`);
```

**Output:** 
`Before calling Pass by value 
        Function -> a = 1 b = 2
Inside Pass by value 
        function -> a = 2 b = 1
After calling Pass by value 
       Function -> a =1 b = 2`

# 

## Pass by reference :

- In Pass by Reference, Function is called by directly passing the reference/address of the variable as an argument. So changing the value inside the function also change the original value. In JavaScript **array and Object** follows pass by reference property.
- In Pass by reference, parameters passed as an arguments does not create its own copy, it refers to the original value so changes made inside function affect the original value.

**Example:** In this example we have shown pass by reference.

```jsx
function PassbyReference(obj) {
	let tmp = obj.a;
	obj.a = obj.b;
	obj.b = tmp;

	console.log(`Inside Pass By Reference 
		Function -> a = ${obj.a} b = ${obj.b}`);
}

let obj = {
	a: 10,
	b: 20

}
console.log(`Before calling Pass By Reference 
	Function -> a = ${obj.a} b = ${obj.b}`);

PassbyReference(obj)

console.log(`After calling Pass By Reference 
	Function -> a = ${obj.a} b = ${obj.b}`);
```

**Output :** 
`Before calling Pass By Reference 
    Function -> a = 10 b = 20
Inside Pass By Reference 
        Function -> a = 20 b = 10
After calling Pass By Reference 
    Function -> a = 20 b = 10`

**NOTE :** In Pass by Reference, we are mutating the original value. when we pass an object as an arguments and update that object’s reference in the function’s context, that won’t affect the object value. But if we mutate the object internally, It will affect the object .



<br> 

## Q.27 exec() and test() methods for REGEX
The **RegExp.prototype.test()** and **RegExp.prototype.exec()** methods are the methods in JavaScript used to handle regular expressions. In addition to these two JavaScript includes a number of built-in methods for manipulating and processing text using regular expressions.

***What are regular expressions?***

**Regular expressions** are patterns that are used to search for character combinations in a string. Regular expressions are treated as objects in JavaScript and are denoted by either "regex" or "RegExp."

## exec():

The exec() method makes a search for the specified match of the string in the given string. If the match of the string is present in the given string it returns an array and if the match is not found in the given string, then it returns a null value. In other words, The exec() method takes a string as the parameter. This string is which is to be checked for match in the given string.

### **Syntax**

This is the syntax of the exec() method of regular expressions in JavaScript −

```
regularExpressionObj.exec(string)

```

### **Example**

Following is an example of the exec() method in JavaScript. In here we are searching for a particular word in the given string.

```jsx
var txt ="Learning regular expressions in JavaScript";
var search1 = new RegExp("JavaScript");
var search2 = new RegExp("Akshay")
var res1 = search1.exec(txt);
var res2 = search2.exec(txt);

console.log(res1)
console.log(res2)

OUTPUT  : 

[
  'JavaScript',
  index: 32,
  input: 'Learning regular expressions in JavaScript',
  groups: undefined
]
null
```

## test () :

The **test()** method makes a search for the specified match of the string in the given string. The difference in between exec() and test() method is that the exec() method will return the specified match if present or null if not present in the given string whereas the test() method returns a Boolean result i.e., true if the specified match is present or else returns false if it is not present.

### **Syntax**

This is the syntax of the test() method in JavaScript −

```
regularExpressionObj.test(string)

```

This also takes the given input string as the parameter and returns the Boolean result.

### **Example**

This programs also searches for a given word in a string but in here we are using the test() method.

```jsx
var txt ="Learning regular expressions in JavaScript";
var search1 = new RegExp("JavaScript");
var search2 = new RegExp("Abdul")
var res1 = search1.test(txt);
var res2 = search2.test(txt);
         
console.log(res1)
console.log(res2)

output : 
    true
    false
```

<br> 

## Q.28 for…of  AND  for …in
In JavaScript, `for...of` and `for...in` are both loop constructs, but they are used for different purposes and iterate over different types of data structures.

1. **`for...of` loop:**
    - Used for iterating over iterable objects such as arrays, strings, maps, sets, etc.
    - Introduced in ECMAScript 6 (ES6).
    - Provides a concise syntax for iterating over values rather than indices.
    - Example:
        
        ```jsx
        let array = [1, 2, 3];
        
        for (let value of array) {
          console.log(value);
        }
        
        ```
        
2. **`for...in` loop:**
    - Used for iterating over the properties of an object.
    - Iterates over enumerable properties, including properties inherited from the object's prototype chain.
    - Not recommended for iterating over arrays, as it may produce unexpected results when used with arrays due to its behavior of iterating over object properties.
    - Example:
        
        ```jsx
        let obj = { a: 1, b: 2, c: 3 };
        
        for (let key in obj) {
          console.log(key, obj[key]);
        }
        
        ```
        

In summary, use `for...of` when you want to iterate over values of an iterable, and use `for...in` when you want to iterate over the properties of an object. Be cautious when using `for...in` with arrays, as it might not behave as expected if the array has additional properties beyond its numeric indices.

<br> 

## Q.29 OR  &  AND operators in javascript 
## OR ( || ):

In case of **OR** operator if first operand is true then it will return first operand and if first operand is falsy then only it returns second value.

e.g. 

```tsx

console.log(90 || 12);
console.log(0 || 32);

oputput : 90
				 32
```

## AND ( && ) :

In case of **AND** operator, if first operand is true, then it will return second operand , and if first operand is false then it will return first operand.

e.g. 

```tsx

console.log(90 && 12);
console.log(0 && 32);
console.log(22 && 0);

output : 12
				 0
		     0
```


<br> 


## Q.30 SHALLOW AND DEEP COPY

# Shallow Copy

When a reference variable is copied into a new reference variable using the **[assignment operator](https://www.geeksforgeeks.org/javascript-assignment-operators/)**, a shallow copy of the referenced object is created. In simple words, a reference variable mainly stores the address of the object it refers to. When a new reference variable is assigned the value of the old reference variable, the address stored in the old reference variable is copied into the new one. This means both the old and new reference variables point to the same object in memory. As a result, if the state of the object changes through any of the reference variables it is reflected for both. Let us take an example to understand it better.

**Example:** Below is an example of a shallow copy.

```jsx
let employee = {
  eid: "E102",

  ename: "Jack",

  eaddress: "New York",

  salary: 50000,
};
console.log("Employee=> ", employee);

let newEmployee = employee; // Shallow copy
console.log("New Employee=> ", newEmployee);

console.log("---------After modification----------");

newEmployee.ename = "Beck";

console.log("Employee=> ", employee);

console.log("New Employee=> ", newEmployee);

// Name of the employee as well as

// newEmployee is changed.
```

---

**Output:**

Top VS Code Extensions for Web Developer in 2024!! GeeksforGeeks

!https://media.geeksforgeeks.org/wp-content/uploads/20201123135651/emp1.png

**Explanation:** From the above example, it is seen that when the name of newEmployee is modified, it is also reflected for the old employee object. This can cause data inconsistency. This is known as a shallow copy. The newly created object has the same memory address as the old one. Hence, any change made to either of them changes the attributes for both. To overcome this problem, a deep copy is used. If one of them is removed from memory, the other one ceases to exist. In a way the two objects are interdependent.

# Deep Copy

**Unlike the shallow copy, deep copy** makes a copy of all the members of the old object, allocates a separate memory location for the new object, and then assigns the copied members to the new object. In this way, both the objects are independent of each other and in case of any modification to either one, the other is not affected. Also, if one of the objects is deleted the other still remains in the memory. Now to create a deep copy of an object in JavaScript we use JSON.parse() and JSON.stringify() methods. Let us take an example to understand it better.

**Example:** Below is the example of deep copy.

- Javascript
- 

```
let employee = {
  eid: "E102",

  ename: "Jack",

  eaddress: "New York",

  salary: 50000,
};

console.log("=========Deep Copy========");

let newEmployee = JSON.parse(JSON.stringify(employee));

console.log("Employee=> ", employee);

console.log("New Employee=> ", newEmployee);
console.log("---------After modification---------");

newEmployee.ename = "Beck";

newEmployee.salary = 70000;

console.log("Employee=> ", employee);
console.log("New Employee=> ", newEmployee);
```

---

**Output:**

!https://media.geeksforgeeks.org/wp-content/uploads/20201123142421/emp2.png

**Explanation:** Here the new object is created using the JSON.parse() and JSON.stringify() methods of JavaScript. JSON.stringify() takes a JavaScript object as an argument and then transforms it into a JSON string. This JSON string is passed to the JSON.parse() method which then transforms it into a JavaScript object. This method is useful when the object is small and has serializable properties. But if the object is very large and contains certain non-serializable properties then there is a risk of data loss. Especially if an object contains methods then JSON.stringify() will fail as methods are non-serializable. There are better ways to a deep clone of which one is Lodash which allows cloning methods as well.


<br> 

## Q.31 what is ES6? 
ES6, short for ECMAScript 2015, is a major update to the JavaScript language specification. It introduced several new features and improvements to the language, aimed at making JavaScript development more efficient, readable, and powerful. Some of the key features introduced in ES6 include:

1. **Arrow functions**: A more concise syntax for writing functions, making code cleaner and more readable.
2. **Let and const**: New variable declaration keywords that offer block-scoping, providing better control over variable scope and reducing bugs.
3. **Template literals**: A new way to create strings that allows for easy interpolation of variables and expressions.
4. **Enhanced object literals**: Simplified syntax for defining object properties and methods.
5. **Destructuring assignment**: A convenient way to extract values from arrays or objects into variables.
6. **Classes**: A more familiar syntax for creating object-oriented classes and inheritance in JavaScript.
7. **Promises**: A built-in mechanism for handling asynchronous operations, making asynchronous code easier to read and write.
8. **Modules**: A standardized way to organize and import/export code between files, improving code maintainability and reusability.

These are just a few of the many features introduced in ES6. Since its release, subsequent versions of ECMAScript have been introduced, each bringing new enhancements and improvements to the language. However, ES6 marked a significant milestone in the evolution of JavaScript, laying the foundation for modern JavaScript development practices.


<br> 

## Q.32 what is arrow function in javascript? 
An arrow function is a concise way to write anonymous functions in JavaScript. It was introduced in ECMAScript 6 (ES6) and provides a more compact syntax compared to traditional function expressions. Arrow functions are especially useful for short, one-line functions and for maintaining lexical `this` context.

Here's the basic syntax of an arrow function:

```jsx
(parameter1, parameter2, ...) => { statements }

```

Or for single-line functions, you can omit the curly braces and return statement:

```jsx
(parameter1, parameter2, ...) => expression

```

For example:

```jsx
// Traditional function expression
let add = function(a, b) {
  return a + b;
};

// Equivalent arrow function
let add = (a, b) => a + b;

```

Arrow functions inherit the `this` value from the enclosing lexical context, unlike traditional functions which have their own `this` context. This makes arrow functions especially useful when working with object methods or callbacks, as it can help avoid confusion and maintain the expected value of `this`.

Here's an example demonstrating how arrow functions maintain `this`:

```jsx
let obj = {
  name: 'Alice',
  greet: function() {
    // Traditional function expression
    setTimeout(function() {
      console.log('Hello, ' + this.name); // Output: Hello, undefined
    }, 1000);

    // Arrow function
    setTimeout(() => {
      console.log('Hello, ' + this.name); // Output: Hello, Alice
    }, 1000);
  }
};

obj.greet();

```

In the above example, the arrow function inside `setTimeout` retains the `this` context of the `obj` object, allowing it to access the `name` property correctly. In contrast, the traditional function expression creates its own `this` context, resulting in `undefined` for the `name` property.


<br> 

## Q.33 What are web apis ? 
1. WEB APIS:
Web APIS means which are part of browser, not javascript .
    
    ```
     1. setTimeout()
     2. DOM API
     3. fetch
     4. localstorage
     5. console
     6. location
    
    ```
    
    ```
    
    e.g.
    console.log("start")
    setTimeout(()=>{
    console.log("In settimeout");
    },5000)
    console.log("end");
    
     O/P :
     	start
     	end
     	In settimeout
    
     NOTE:
     	Here when execution starts it creates global execution context in call stack. It will first print start in the console,
    
    ```
    

then it will goes to the timeout and it throws that settimeout funtion in the web apis environment, than it print end in the console and then global
execution context destroy
.
Then after completion of 5 seconds, it will push the callback function to the callback queue, then EVENT LOOP throws this
function inside callback queue to th call stack and then again global execution context starts. And after all execution it gets destroyed.

```
 	this is for settimeout and others

 	for callback functions inside promise it will use microtask queue.

 	SO MICROTASK QUEUE MUST BE EXECUTED BEFORE callback queue.

 	NOTE :
 		 Suppose if microtask queue have more tasks , then until completion of microtask queue it will not execute the processes of

```

callback queue and
it takes more time ,so this process is known as STARVATION of the callback queue.



<br> 

## Q.34 What is hoisting in javascript? 
In javascript functions and variables are moved to the top is called as hoisting .

```
 		e.g.
 		console.log(x);
 		getName();
 		var x=8;
 		function getName(){
 			console.log("Akshay");
 		}

 		O/P:
 			undefined
 			Akshay

                 NOTE:
                 	If we write arrow function instead of normal function then it will treated as a variable and it also returns
		undefined.

```

## SCOPE CHAINING :

E.G.
```jsx
function hello() {
  var a = 10;
  function hii() {
    console.log(b);
  }
  hii();
}
hello();
```

```
		O/P : 10

		NOTE :
			here first it will search value of b in local environment i.e. in hii function, if it is not found then it will go

```

to its parent environment i.e. LEXICAL environment, if again value is not found then again it will check in its parent environment,
i.e. here in global environment.
THIS CHAINING IS CALLED AS SCOPE CHAIN..


<br> 


## Q.35 What is closure ? 
Closures are a fundamental concept in JavaScript that occur when a function is defined within another function and the inner
function has access to 	the outer function's variables and scope chain. In simpler terms, a closure allows a function to "remember" its
lexical scope even when it is executed outside of that scope.

To understand closures better, consider the following example:

```jsx
	function outerFunction() {
      	const outerVar = 'I am from the outer function';

    	function innerFunction() {
			console.log(outerVar); // The inner function has access to outerVar
	    }

	    return innerFunction;
    }

	const closureFunction = outerFunction();
	closureFunction(); // Output: "I am from the outer function"

```



<br> 

## Q.36 DIFFERENCES BETWEEN NULL AND UNDEFINED
In JavaScript, `null` and `undefined` are two distinct values that represent the absence of a meaningful value, but they have different
meanings and use cases.
	1. **undefined:**
	   - When a variable is declared but not assigned a value, it automatically gets the value `undefined`.
	   - It is a primitive data type and represents the absence of a value or uninitialized state.
	   - A function that doesn't explicitly return a value also implicitly returns `undefined`.
	   - An object property that does not exist will return `undefined` when accessed.

	Example:
```jsx
	let variable1; // declared but not assigned, so it is undefined
	const obj = { prop: 'hello' };
	console.log(obj.prop); // Output: "hello"
	console.log(obj.nonExistentProp); // Output: undefined
	function noReturnValue() {
	  // no explicit return, so it returns undefined
	}
	console.log(noReturnValue()); // Output: undefined
```

	2. **null:**
	   - `null` is a primitive data type that represents the intentional absence of any value.
	   - It is usually assigned explicitly by a developer to indicate that a variable or object property does not have a value.
	   - It is often used as a deliberate placeholder when a value is expected but not available or valid.


Example:

```jsx
let variable2 = null; // assigned null intentionally to indicate no value
const obj2 = { prop: null }; // explicitly setting prop to null

```

Here's a summary of the key differences:

- `undefined` is automatically assigned to variables that are declared but not initialized, while `null` must be explicitly assigned.
- `undefined` represents the absence of a value due to lack of assignment or an uninitialized state, while `null` represents an intentional
lack of value.
- `undefined` is often used to indicate that something is not present or not available, whereas `null` is often used to represent the absence
of a valid value.

In most cases, you don't need to assign `null` explicitly, as JavaScript will handle uninitialized variables with `undefined`.

However, using `null` can be useful when you want to explicitly indicate the absence of a value, especially when you are working with
objects and need to differentiate between "not set" and "set to null."


<br> 

## Q.37 What are Promises and async/await in JavaScript? How do they simplify asynchronous programming?

Promises and async/await are modern JavaScript features that simplify asynchronous programming and make it easier to work with asynchronous
tasks like API calls, file I/O etc.

```
1. Promises:
	Promises are objects representing the eventual completion (or failure) of an asynchronous operation and its resulting value.

```

They provide a clean and structured way to handle asynchronous tasks.

```
Promises have three states:
	Pending: The initial state. The promise is still pending and hasn't been fulfilled or rejected yet.
	Fulfilled: The asynchronous operation completed successfully, and the promise now holds the resulting value.
	Rejected: The asynchronous operation encountered an error, and the promise holds the reason for the rejection.
	Promises simplify asynchronous programming by allowing you to chain multiple asynchronous operations using .then() and

```

handle errors using .catch().

Example using Promises:

```jsx
function fetchData() {
	return new Promise((resolve, reject) => {
	 // Simulate an API call
	 setTimeout(() => {
		  const data = { id: 1, name: 'John Doe' };
 		 if (data) {
 		   resolve(data); // Fulfill the promise with data
 		 } else {
  		  reject('Error: Data not found.'); // Reject the promise with an error message
		  }
	 }, 1000);
	});
}

fetchData()
.then((data) => console.log(data))
.catch((error) => console.error(error));

```

<br> 

## Q.38  Describe the differences between let, const, and var in terms of scope and hoisting.
The differences between `let`, `const`, and `var` in terms of scope and hoisting are significant, and understanding them is essential for
writing clean and predictable JavaScript code.

1. **var:**
    - `var` was the original way to declare variables in JavaScript, introduced in ECMAScript 5 (ES5).
    - Variables declared with `var` are function-scoped, meaning they are only accessible within the function where they are declared.
    - If a `var` variable is declared outside any function, it becomes a global variable, accessible throughout the entire program.
    - Hoisting occurs with `var`, which means that variable declarations are moved to the top of their containing scope during the compilation
    phase, while the initial assignment remains in place.
    
    Example with `var`:
    
    ```jsx
    function exampleFunction() {
      if (true) {
        var x = 10;
        console.log(x); // Output: 10
      }
      console.log(x); // Output: 10 (due to hoisting)
    }
    
    ```
    
2. **let:**
    - `let` was introduced in ECMAScript 6 (ES6) to address some issues with `var`.
    - Variables declared with `let` have block scope, which means they are only accessible within the block (i.e., any set of curly braces)
    where they are defined.
    - Unlike `var`, `let` variables are not hoisted to the top of their scope, so you cannot access them before their declaration.
    
    Example with `let`:
    
    ```jsx
    function exampleFunction() {
      if (true) {
        let y = 20;
        console.log(y); // Output: 20
      }
      console.log(y); // Error: y is not defined
    }
    
    ```
    
3. **const:**
    - `const` was also introduced in ES6 and stands for "constant."
    - Variables declared with `const` are block-scoped like `let` and cannot be reassigned after they are declared.
    - The value assigned to a `const` variable must be provided at the time of declaration and cannot be changed later.
    
    Example with `const`:
    
    ```jsx
    function exampleFunction() {
      const z = 30;
      console.log(z); // Output: 30
    
      z = 40; // Error: Assignment to constant variable
    }
    
    ```
    

In summary:

- `var` is function-scoped and hoisted, which can sometimes lead to unexpected behavior and bugs.
- `let` and `const` are block-scoped and not hoisted, providing more predictable behavior and safer code.
- Use `let` when you need to reassign the variable, and use `const` when the value should remain constant throughout the program.
- In modern JavaScript, it is recommended to use `let` and `const` over `var` for better scoping and to avoid hoisting-related issues.


<br> 

## Q.39 What are the differences between map, forEach, filter, and reduce array methods? Provide use cases for each.
`map`, `forEach`, `filter`, and `reduce` are important array methods in JavaScript that allow you to manipulate arrays in different ways.
Here are the differences between them along with their use cases:

1. **`map`:**
    - `map` is used to transform each element of an array into a new array based on a given function.
    - It creates a new array with the same length as the original array, where each element is the result of applying the provided function
    to the corresponding element of the original array.
    
    Use case:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    const squaredNumbers = numbers.map((num) => num * num);
    // Output: [1, 4, 9, 16, 25]
    
    const names = ['Alice', 'Bob', 'Charlie'];
    const upperCaseNames = names.map((name) => name.toUpperCase());
    // Output: ['ALICE', 'BOB', 'CHARLIE']
    
    ```
    
2. **`forEach`:**
    - `forEach` is used to iterate over an array and perform a specific action or side effect for each element. It does not create a new array
    but instead modifies the existing array or performs some side effects.
    
    Use case:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    numbers.forEach((num) => console.log(num));
    // Output: 1 2 3 4 5
    
    ```
    
3. **`filter`:**
    - `filter` is used to create a new array containing elements that pass a certain condition specified in a callback function.
    - It returns a new array with only the elements that satisfy the condition.
    
    Use case:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    const evenNumbers = numbers.filter((num) => num % 2 === 0);
    // Output: [2, 4]
    
    const names = ['Alice', 'Bob', 'Charlie'];
    const longNames = names.filter((name) => name.length > 5);
    // Output: ['Charlie']
    
    ```
    
4. **`reduce`:**
    - `reduce` is used to "reduce" an array into a single value by applying a function to each element of the array.
    - It takes an accumulator and each element of the array, and it returns the accumulated value after applying the provided function to all
    elements.
    
    Use case:
    
    ```jsx
    const numbers = [1, 2, 3, 4, 5];
    
    const sum = numbers.reduce((acc, num) => acc + num, 0);
    // Output: 15 (sum of all elements)
    
    const names = ['Alice', 'Bob', 'Charlie'];
    const concatenatedNames = names.reduce((acc, name) => acc + ' ' + name);
    // Output: 'Alice Bob Charlie'
    
    ```
    

In summary:

- `map` is used to transform an array into a new array with the same length.
- `forEach` is used for iterating over an array and performing side effects on each element.
- `filter` is used to create a new array with only the elements that pass a specified condition.
- `reduce` is used to "reduce" an array into a single value by applying a function to each element and accumulating the results.


<br> 

## Q.40 How does this work in JavaScript? Provide examples of how it can change in different contexts?
The behavior of `this` in JavaScript can change depending on the context in which it is used. The value of `this` is determined dynamically
during the runtime based on how a function is called, rather than how it is defined. The way `this` behaves in different contexts is one of the
aspects that can lead to confusion for developers. Let's explore some common scenarios:

1. **Global context:**
When `this` is used in the global context (outside of any function or object), it refers to the global object, which is the `window` object
in browsers and the `global` object in Node.js.
    
    Example:
    
    ```jsx
    console.log(this === window); // Output: true (in a browser environment)
    console.log(this === globalThis); // Output: true (in Node.js)
    
    ```
    
2. **Function context:**
When `this` is used inside a regular function, its value depends on how the function is called. If the function is called as a standalone
function (not attached to an object), `this` will point to the global object (in non-strict mode) or be `undefined` (in strict mode).
    
    Example:
    
    ```jsx
    function showThis() {
      console.log(this);
    }
    
    showThis(); // Output: window (in a browser environment, non-strict mode)
    
    ```
    
3. **Method context:**
When `this` is used inside a method (a function defined as a property of an object), `this` refers to the object that the method is called on.
    
    Example:
    
    ```jsx
    const person = {
      name: 'John',
      greet() {
        console.log(`Hello, my name is ${this.name}.`);
      },
    };
    
    person.greet(); // Output: "Hello, my name is John."
    
    ```
    
4. **Constructor context:**
When a function is used as a constructor (invoked with the `new` keyword), `this` refers to the newly created instance of the object that
the constructor is creating.
    
    Example:
    
    ```jsx
    function Person(name) {
      this.name = name;
    }
    
    const john = new Person('John');
    console.log(john.name); // Output: "John"
    
    ```
    
5. **Event handler context:**
In event handlers, `this` often refers to the DOM element on which the event is triggered.
    
    Example:
    
    ```html
    <button onclick="console.log(this);">Click me</button>
    <!-- Output: [button HTML element] -->
    
    ```
    
6. **Arrow function context:**
Arrow functions have a different behavior for `this` compared to regular functions. In arrow functions, `this` retains the value of the enclosing context lexically, which means it captures the `this` value of the surrounding scope.
    
    Example:
    
    ```jsx
    const obj = {
      name: 'John',
      greet() {
        setTimeout(() => {
          console.log(this.name); // Output: "John" (this retains the value of the "obj" object)
        }, 100);
      },
    };
    
    obj.greet();
    
    ```
    
    Remember that understanding the context in which `this` is used is crucial for writing effective JavaScript code, especially when dealing
    with functions in different contexts or using them as event handlers. Using arrow functions can sometimes help maintain the desired behavior of
    `this`.



<br> 

## Q.41 POLYFILLS FOR MAP FUNCTION (IMPLEMENTATION OF MAP FUNCTION):
let arr=[3,4,5,67]

```jsx
let arr = [2, 3, 5, 6, 7, 9];
Array.prototype.myMap = function (cb) {
  let temp = [];
  for (let i = 0; i < this.length; i++) {
    temp.push(cb(this[i], i, this));
  }
  return temp;
};

// let ar2=arr.map((ar)=>{
//     return ar*2;
// })
// console.log(ar2)

let ar2 = arr.myMap((ar, i, arr) => {
  return ar * 2;
});
console.log(ar2);
```


<br> 


## Q.42 POLYFILLS FOR FILTER :
```jsx
let arr=[3,4,5,67]

Array.prototype.myFilter=function(cb){
  let temp=[]
 for(let i=0;i<this.length;i++){
     if(cb(this[i], i , this))temp.push(this[i])
   }
   return temp;
}

let arr2=arr.myFilter((ar,i,arr)=>{
    return ar>4;
})

console.log(arr2)
```


<br> 


## Q.43 POLYFILLS FOR REDUCE :
```jsx
let arr=[3,4,5,67]

// let sum=arr.reduce((acc, curr, i, arr)=>{
//     return acc+curr;
// },0)
// console.log(sum)

Array.prototype.myReduce=function(cb, initialValue){
		let accumulator=initialValue;
		for(let i=0;i<this.length;i++){
        	accumulator=accumulator?cb(accumulator, this[i], i, this):this[i]
		}
		return accumulator;
}

let sum=arr.myReduce((acc, curr, i, arr)=>{
		return acc+curr;
},0)

console.log(sum)
```


<br> 

## Q.44 What is the purpose of the Map object in JavaScript? How is it different from a regular JavaScript object?
Answer: The Map object in JavaScript is used to store key-value pairs where both the key and the value can be of any data type.
It is different from a regular JavaScript object in that the keys in a Map can be objects or primitive data types, while in a regular object, keys are limited to strings or symbols.
Additionally, Map maintains the insertion order of its elements, making it more suitable for scenarios where order matters.
It also provides helpful methods like size, forEach, and clear.


<br> 

## Q.45 Explain the concept of event delegation in JavaScript.
Answer: Event delegation is a technique where instead of attaching an event listener to each individual element, you attach a single event listener to a parent element. The events are then handled based on the target (the element that triggered the event) and propagated up through the
DOM tree.

consumption and simplifies event management.

This technique is useful when you have a large number of elements to which you want to attach the same event, as it reduces memory


<br> 

## Q.46 let & const declarations are hoisted or not ?
Answer: Yes , let and  const declarations are hoisted . This are in the temporal dead zone for time being .
javascript compiler push the variable and declaration on top . S
e.g.
if there are two variables, one is declared using var and another is declared using let .

then var assigned value undefined in global scope. But let variable assigned value in script scope. It happens before execution of single line . ==> that means hoisting is happens here also but in case of let and const it allocated space in script space not in global space. And in case of var it allocates memory in global space .


<br> 

## Q.47 TEMPORAL DEAD ZONE :
Answer :
it is the time since when the let variable is hoisted and till it is initialized some value .
Whenever you try to access variable inside temporal dead zone, it gives a reference error.

```
	if we try to access var  variable using window object , then it is available in window object,
	 but in case of let and const it should not available in window object.

	 ===========================================================================================================================

```

Syntax error , reference error and Type error :
1. syntax error :

```jsx
	let a=10;
	let a=10;+

	note : here we declare and define two let variables using same variable name . So it gives syntax error as
		'Identifier a has already been declared'

 in case of let,
 	let a;
 	a=10;
 	console.log(a);

 	it is fine , means reinitialization of let variable is fine but in case of const variable it will give an error.

 	const b;
 	b=200;

 	it must display syntax error as
 		Missing initializer in const declaration.

 2. Type error :
 	const a=10;
 	a=30;

 	it will gives Type Error as
 	Assignment to constant variable .

3. Reference error :
	console.log(a);
	let a =10 ;

	then it will give an reference error as ,
	 Can not access a before initaliazation .

```


<br> 


## Q.48 what is block in javascript ?
group of multiple statements can be used in a place where javascript expects a single statement.

block scope :
block scope means what all variables and functions that are accessed inside block.
e.g.

```jsx
 {
 	var a=10;
 	let b=20;
 	const c=30;
 }

 Note:
 	here a is hoisted in global scope  but b and c are hoisted in block scope.

```

Shadowing in javscript:
e.g.

```jsx
 	var a=100;
 	{
 		var a=10;
 		let b=20;
 		let c=230;
 		console.log(a);
 	}
 	console.log(a);

the value of a is changed, is called as shadowing in javascript.

 NOTE :
 	let a =10;
 	{
 		var a=20;
 	}

	it will generate error .

	but if we write here  :
	let a=10;
	{
		let a=20;
	}

	then it is fine.

	if we declare variable in function or inside block then it will not give error.

	e.g.
		let a=20;
		function x(){
			var a=20;
		}

		then it will not generate error.

		NOTE : SAME FOR THE CONST VARIABLES

```

LEXICAL SCOPE:
const a=10;
{
const a=20;
{
const a=39;
console.log(a)
}
}


<br> 

## Q.49 PRIVATE VARIABLE USING  CLOSURE:(MEMOIZATION)	
PRIVATE VARIABLE USING  CLOSURE:(MEMOIZATION)	

```jsx
function counter() {
  var count = 0;
  return function incCount() {
    count++;
    console.log(count);
  };
}
var cnt = counter();
cnt();
cnt();
cnt();

	O/P:
		1
		2
		3

```


<br> 

## Q.50 CONSTRUCTOR FUNCTION IN JAVASCRIPT :

```jsx
function Counter() {
  var count = 0;
  this.incCounter = function () {
    count++;
    console.log(count);
  };
  this.decCounter = function () {
    count--;
    console.log(count);
  };
}
var counter = new Counter();
counter.incCounter();
counter.incCounter();
counter.incCounter();
counter.decCounter();
```

```
O/P:
	1
	2
	3
	2

```

<br> 

## Q.51 WHAT IS GARBAGE COLLECTOR? 
    Garbage collector is the program in the browser or javascript engine which kind of freeze of the unitilize engine.


<br> 

## Q.52 what are pure functions in javascript ? 
A Pure Function is a function (a block of code) that always returns the same result if the same arguments are passed.
It does not depend on any state or data change during a program's execution. Rather, it only depends on its input arguments.


<br> 


# Some functional Concepts : 
1. FUNCTION STATEMENT: // FUNCTION DECLARATION:
e.g.
function a(){
console.log("this all is functions statement");
    
    ```
     }
    
     This is known as a functionn statement.
    
    ```
    
2. FUNCTION EXPRESSION:
```jsx
var b=function(){
    console.log("hii");
}

```

This is known as a function expression.
    
 NOTE :
    The major difference between this two is hoisting .
    If we called both of this function without even declaring it, then a function will give proper output but when it comes to b,
    then it will give Typeerror that b is not a function .
    i.e. this b is act as a variable , not a functionn until the this line 386 executes .
    
4. ANONYMOUS FUNCTION:
Function without name is called anonymous function.
Anonymous functions are used , when the functions are used as a values .
    
    ```jsx
     function (){
     	//some code
     }
    
    ```
    
    but it will generate errror, we need to asssign it in some variable ,
    we can also write anonymous function using arrrow function.
    
    e.g. this is IIFE (immediately invoked function expression)
   ```jsx
    (()=>{
    console.log("this is also anonymous function")
    })()
   ```
    
6. NAMED FUNCTION EXPRESSIONS:
we just need to write name for function expression.
    ```jsx
    var a=function xyz(){
    console.log("named function expression")
    }
    a()
``

7. DIFFERENCE BETWEEN PARAMETERS AND ARGUMENTS :
e.g.
    
    function abc(a,b){   // this are known as parameters
    
    }
    
    abc(2,5);      // this are known as arguments


   
8. FIRST CLASS FUNCTIONS :
Passing another function inside a function or returning another function inside a function.
The ability of function to used as values and can be passed it as argument to another function and can be return another function is
called as First Class Functions.
e.g.
    
    ```jsx
     var b=function(param1){
     	return function(){
    
     	}
     }
    
     function xyz(){
    
     }
     b(xyz);
    
    ```



## Q.53 STARVATION OF THE CALLBACK QUEUE(TASK QUEUE):
suppose microtaskk queue have many tasks in it , then callback queue is waiting to complete tasks inside microtask queue,
so this is known as starvation of callback queue.


<br> 

## Q.54 IMPLEMENTATION OF PROMISE ALL :
IMPLEMENTATION OF PROMISE ALL :

```jsx
function showtext(text, time) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(text);
    }, time);
  });
}

// Promise.all([showtext("hello",1000), Promise.resolve("hiii")]).then((val)=>console.log(val))

function myPromiseall(promises) {
  let result = [];

  return new Promise((resolve, reject) => {
    promises.forEach((p, index) => {
      p.then((res) => {
        result.push(res);
        if (index === promises.length - 1) {
          resolve(result);
        }
      }).catch((error) => {
        reject(error);
      });
    });
  });
}
myPromiseall([showtext("hello", 1000), Promise.resolve("hiii")]).then((val) =>
  console.log(val)
);
```


<br> 

## Q.55 Implementaion of Debouncing:
Debouncing means adding timeout to the perticular event.


```jsx
const debounce = (cb, d) => {
  let timer;
  return function (...args) {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => {
      cb(...args);
    }, d);
  };
};
const handleChange = debounce((e) => {
  console.log(e.target.value);
}, 1000);
```


<br> 

## Q.56 TO FIND LARGEST AND SECONDALARGEST IN ARRAY
TO FIND LARGEST AND SECONDALARGEST IN ARRAY

```jsx

const arr = [12, 35, 1, 10, 34, 1];
let largest = Number.NEGATIVE_INFINITY;
let secondLarge = Number.NEGATIVE_INFINITY;
for (let i = 0; i < arr.length; i++) {
  if (arr[i] > largest) {
    secondLarge = largest;
    largest = arr[i];
  } else if (arr[i] != largest && arr[i] > secondLarge) {
    secondLarge = arr[i];
  }
}
console.log(largest, secondLarge);

```


<br> 

## Q.57 THROATLING IN JAVASCRIPT:
suppose we have added button in our component,and onclick of that button there is an API call, but if user clicks more times on that button
then api calls more times , so for that we use throatning, its like debouncing, we will add certain time in that throatling so that it will work only
after that certain time.

<br> 


## Q.58 How does javascript handle asynchronous operations?
Sure, let's delve a bit deeper into how JavaScript handles asynchronous operations within its event loop:

1. **Event Loop**: JavaScript runs in a single-threaded environment, meaning it can only execute one piece of code at a time. The event loop is a mechanism that allows JavaScript to handle asynchronous operations efficiently without blocking the main thread.
2. **Call Stack**: The call stack is a data structure that keeps track of function calls in the current execution context. When a function is called, it's added to the top of the call stack, and when it completes, it's removed from the stack.
3. **Task Queue (or Message Queue)**: JavaScript has a task queue where asynchronous operations, such as callbacks from I/O operations (like fetching data from an API) or timer events (like setTimeout()), are placed once they are completed.
4. **Event Loop Process**: Here's how the event loop works:
    - When the call stack is empty, the event loop checks if there are any tasks in the task queue.
    - If there are tasks in the queue, the event loop takes the first task and pushes it onto the call stack for execution.
    - Once the task is executed, it may result in synchronous code execution, which adds more functions to the call stack, or it may schedule more asynchronous tasks.
    - Any newly scheduled asynchronous tasks are added to the task queue.
    - This process continues, with the event loop repeatedly checking the call stack and task queue, until both are empty.
5. **Non-blocking I/O**: JavaScript's event loop allows it to perform non-blocking I/O operations. When an asynchronous operation like fetching data from an API is initiated, JavaScript doesn't wait for it to complete. Instead, it continues executing the rest of the code. Once the operation is complete, its callback is placed in the task queue, and eventually, the event loop picks it up for execution.

This event-driven model enables JavaScript to handle asynchronous operations efficiently while ensuring that the user interface remains responsive. It's crucial to understand this mechanism when working with asynchronous code in JavaScript to avoid blocking the main thread and creating a smooth user experience.



<br> 


## Q.59 task and microtask queue
In JavaScript, the task queue and microtask queue are two separate queues that are part of the event loop mechanism, responsible for handling asynchronous operations.

1. **Task Queue**:
    - The task queue (also known as the callback queue or message queue) holds tasks that are ready to be executed by the JavaScript engine.
    - Tasks in the task queue typically include events like DOM events (e.g., click, mouseover), timer events (e.g., setTimeout(), setInterval()), and I/O events (e.g., fetching data from an API).
    - When the call stack is empty, the event loop checks the task queue. If there are tasks in the queue, the event loop takes the first task and pushes it onto the call stack for execution.
    - Task queue tasks have lower priority compared to microtasks and are executed after all microtasks have been processed.
2. **Microtask Queue**:
    - The microtask queue (also known as the microtask queue or job queue) holds microtasks, which are tasks with higher priority than tasks in the task queue.
    - Microtasks typically include promises (resolved or rejected) and queueMicrotask() calls.
    - When the call stack is empty and there are microtasks in the microtask queue, the event loop processes all microtasks before checking the task queue for tasks.
    - Microtasks are executed in the same event loop iteration, before any new tasks are added to the call stack, allowing for more immediate execution of important tasks.
    - Microtasks are usually used for tasks that need to be executed asynchronously but with higher priority than regular tasks, such as updating the UI after a promise is resolved.

In summary, both the task queue and microtask queue play crucial roles in handling asynchronous operations in JavaScript. The task queue holds tasks like DOM events and timer events, while the microtask queue handles higher-priority tasks like promises. Understanding these queues is essential for understanding the event loop and asynchronous JavaScript execution.


<br> 


## Q.60 How event loop works in javacript ? 
The event loop is a crucial part of how JavaScript handles asynchronous operations, ensuring that code execution remains efficient and responsive. Here's a simplified explanation of how the event loop works in JavaScript:

1. **Call Stack**: JavaScript is single-threaded, meaning it can only execute one piece of code at a time. The call stack is a data structure that keeps track of function calls in the current execution context. When a function is called, it's added to the top of the call stack, and when it completes, it's removed from the stack.
2. **Task Queue and Microtask Queue**: JavaScript also has two queues: the task queue and the microtask queue.
    - **Task Queue**: This queue holds tasks that are ready to be executed by the JavaScript engine, such as DOM events, timer events, and I/O events.
    - **Microtask Queue**: This queue holds microtasks, which are tasks with higher priority than tasks in the task queue. Microtasks typically include promises (resolved or rejected) and queueMicrotask() calls.
3. **Event Loop Process**:
    - When JavaScript starts running, it begins executing synchronous code line by line, adding functions to the call stack and executing them.
    - If JavaScript encounters an asynchronous operation, such as a timer event (e.g., setTimeout()) or a promise, it doesn't wait for it to complete. Instead, it continues executing the remaining synchronous code.
    - Once the call stack is empty (i.e., there are no more synchronous tasks to execute), the event loop kicks in.
    - The event loop continuously checks if the call stack is empty. If it is, the event loop checks the microtask queue first.
    - If there are microtasks in the microtask queue, the event loop processes all microtasks before moving on to the task queue.
    - After processing all microtasks, the event loop checks the task queue for any pending tasks.
    - If there are tasks in the task queue, the event loop takes the first task and pushes it onto the call stack for execution.
    - This process continues indefinitely, with the event loop iterating over the microtask queue and task queue, ensuring that asynchronous tasks are executed in the correct order and without blocking the main thread.

In summary, the event loop is responsible for managing the execution of asynchronous tasks in JavaScript, ensuring that code remains responsive and efficient even when dealing with time-consuming operations. Understanding how the event loop works is crucial for writing efficient and responsive JavaScript code.


<br> 

## Q.61 difference between promise.all and promise.allSettled
| Feature | Promise.all() | Promise.allSettled() |
| --- | --- | --- |
| Handling of Rejected Promises | Fails immediately when any promise rejects. | Waits for all promises to settle, collecting results regardless of rejection. |
| Return Value | Returns a single promise. | Returns a single promise. |
|  | Fulfills with an array of values when all promises fulfill. | Fulfills with an array of result objects once all promises have settled. |
|  | Rejects immediately when any promise rejects. | Each result object contains a status and value or reason. |
| Use Cases | Useful for concurrent execution of multiple promises. | Useful for collecting outcomes of all promises, regardless of rejection. |

This table summarizes the main differences between `Promise.all()` and `Promise.allSettled()` in terms of their behavior and usage.


### example of promise.all()
```jsx
// Example promises
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 1 resolved');
  }, 1000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 2 resolved');
  }, 2000);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 3 resolved');
  }, 3000);
});

// Using Promise.all
Promise.all([promise1, promise2, promise3])
  .then((results) => {
    console.log('All promises resolved:', results);
  })
  .catch((error) => {
    console.error('At least one promise rejected:', error);
  });
```


### example of promise.allSettled(): 
```jsx
// Example promises
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 1 resolved');
  }, 1000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject('Promise 2 rejected');
  }, 2000);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Promise 3 resolved');
  }, 3000);
});

// Using Promise.allSettled
Promise.allSettled([promise1, promise2, promise3])
  .then((results) => {
    console.log('All promises settled:', results);
  });
```

<br>

## Q.62 freeze method Object
`Object.freeze()` is a method in JavaScript that is used to freeze an object, preventing any changes to the object's properties or prototype. When an object is frozen, its properties become read-only, and you cannot add, delete, or modify any properties or their attributes (such as value, writable, enumerable, and configurable).

Here's how you can use `Object.freeze()`:

```jsx
const obj = {
  prop1: 42,
  prop2: 'Hello'
};

Object.freeze(obj); // Freeze the object

// Attempting to modify properties after freezing
obj.prop1 = 100; // This assignment will not have any effect
delete obj.prop2; // This deletion will not be allowed

console.log(obj); // Output: { prop1: 42, prop2: 'Hello' }

```

In this example:

- We first define an object `obj` with two properties.
- We then use `Object.freeze(obj)` to freeze the object.
- Any attempts to modify or delete the properties of `obj` after freezing will be ignored.
- The console log at the end will output the original object, demonstrating that the properties remain unchanged.

`Object.freeze()` operates shallowly. This means that only the immediate properties of the object are frozen. If the properties of the object are themselves objects, their properties are not frozen. To freeze nested objects, you would need to explicitly call `Object.freeze()` on each nested object.

```jsx
const obj = {
  nestedObj: {
    prop1: 42
  }
};

Object.freeze(obj);

// Attempting to modify nested property
obj.nestedObj.prop1 = 100; // This assignment will be allowed

console.log(obj); // Output: { nestedObj: { prop1: 100 } }

```

In this case, `obj.nestedObj` is not frozen, so its properties can still be modified. If you want to freeze `nestedObj`, you would need to call `Object.freeze(obj.nestedObj)` separately.



<br> 

## Q.63 javascript shallow copy and deep copy
In JavaScript, when you want to copy an object, you can perform either a shallow copy or a deep copy, depending on your requirements. Here's an explanation of each:

1. **Shallow Copy**:
    - A shallow copy creates a new object and copies all top-level properties of the original object to the new object.
    - If the properties of the original object are primitive values (such as numbers, strings, or booleans) or references to other objects, a shallow copy will copy those references, not the actual objects.
    - This means that changes made to nested objects within the copied object will be reflected in the original object and vice versa.
    - Shallow copy can be achieved using methods like `Object.assign()`, spread operator (`...`), or by iterating through the properties of the original object and copying them manually.
    
    Example of shallow copy:
    
    ```jsx
    const original = { a: 1, b: { c: 2 } };
    const shallowCopy = Object.assign({}, original);
    original.b.c = 3;
    console.log(shallowCopy.b.c); // Output: 3
    
    ```
    
2. **Deep Copy**:
    - A deep copy creates a new object and recursively copies all properties, including nested objects, from the original object to the new object.
    - It ensures that the copied object is completely independent of the original object, so changes made to nested objects within the copied object will not affect the original object, and vice versa.
    - Deep copy can be more resource-intensive, especially for complex objects with deeply nested structures.
    - Deep copy can be achieved using libraries like Lodash (`_.cloneDeep()`) or by implementing a custom recursive function to traverse the entire object tree and copy each property.
    
    Example of deep copy using Lodash:
    
    ```jsx
    const _ = require('lodash');
    const original = { a: 1, b: { c: 2 } };
    const deepCopy = _.cloneDeep(original);
    original.b.c = 3;
    console.log(deepCopy.b.c); // Output: 2
    
    ```


    ## Deep copy implementation
    ```jsx
 		function deepCloneObj(obj) {
    			if (typeof obj !== 'object') return obj;
    			const clonedObj = Array.isArray(obj) ? [] : {};
    			for (let key in obj) {
      				clonedObj[key] = deepCloneObj(obj[key]);
    			}
    			return clonedObj;
  		}
  		// const obj2 = obj1;
  		// const obj2 = {...obj1}
  		const obj2 = deepCloneObj(obj1);

    ```
    

In summary, a shallow copy copies only the top-level properties of an object, while a deep copy copies all properties, including nested objects, creating a completely independent copy of the original object. The choice between shallow copy and deep copy depends on whether you need a completely independent copy of the original object or if shallow copying is sufficient.


<br> 

## Q.64 difference between this and arrow function
The main differences between a simple function (also known as a regular function) and an arrow function in JavaScript are related to syntax, behavior of the `this` keyword, and handling of arguments and context. Here's a breakdown:

1. **Syntax**:
    - Simple Function:
        
        ```jsx
        function myFunction(param1, param2) {
          // Function body
        }
        
        ```
        
    - Arrow Function:
        
        ```jsx
        const myFunction = (param1, param2) => {
          // Function body
        };
        
        ```
        
2. **Binding of `this`**:
    - Simple Function:
        - Own `this`: A regular function creates its own `this` context when it is invoked.
        - Dynamic `this`: The value of `this` inside a regular function depends on how the function is called (e.g., via `obj.method()` or `myFunction()`).
    - Arrow Function:
        - Lexical `this`: An arrow function does not create its own `this` context. Instead, it captures the `this` value from its surrounding lexical scope (the context in which it is defined).
        - Arrow functions are especially useful when you want to preserve the value of `this` from the enclosing scope.
3. **Arguments Object**:
    - Simple Function:
        - Has its own `arguments` object, which contains all the arguments passed to the function.
    - Arrow Function:
        - Does not have its own `arguments` object. Instead, it inherits the `arguments` object from its surrounding lexical scope.
4. **Usage**:
    - Simple functions have been around since the early days of JavaScript and are still widely used.
    - Arrow functions were introduced in ES6 and are favored for their concise syntax and lexical scoping behavior. They are commonly used in modern JavaScript development, especially for handling callbacks, array methods, and short anonymous functions.

In summary, arrow functions offer a more concise syntax, capture the `this` value lexically, and do not have their own `arguments` object, whereas simple functions have their own `this` context and `arguments` object. The choice between them depends on the specific use case and coding style preferences.


<br> 


## Q.65 javascript shallow copy and deep copy
In JavaScript, when you want to copy an object, you can perform either a shallow copy or a deep copy, depending on your requirements. Here's an explanation of each:

1. **Shallow Copy**:
    - A shallow copy creates a new object and copies all top-level properties of the original object to the new object.
    - If the properties of the original object are primitive values (such as numbers, strings, or booleans) or references to other objects, a shallow copy will copy those references, not the actual objects.
    - This means that changes made to nested objects within the copied object will be reflected in the original object and vice versa.
    - Shallow copy can be achieved using methods like `Object.assign()`, spread operator (`...`), or by iterating through the properties of the original object and copying them manually.
    
    Example of shallow copy:
    
    ```jsx
    const original = { a: 1, b: { c: 2 } };
    const shallowCopy = Object.assign({}, original);
    original.b.c = 3;
    console.log(shallowCopy.b.c); // Output: 3
    
    ```
    
2. **Deep Copy**:
    - A deep copy creates a new object and recursively copies all properties, including nested objects, from the original object to the new object.
    - It ensures that the copied object is completely independent of the original object, so changes made to nested objects within the copied object will not affect the original object, and vice versa.
    - Deep copy can be more resource-intensive, especially for complex objects with deeply nested structures.
    - Deep copy can be achieved using libraries like Lodash (`_.cloneDeep()`) or by implementing a custom recursive function to traverse the entire object tree and copy each property.
    
    Example of deep copy using Lodash:
    
    ```jsx
    const _ = require('lodash');
    const original = { a: 1, b: { c: 2 } };
    const deepCopy = _.cloneDeep(original);
    original.b.c = 3;
    console.log(deepCopy.b.c); // Output: 2
    
    ```
    

In summary, a shallow copy copies only the top-level properties of an object, while a deep copy copies all properties, including nested objects, creating a completely independent copy of the original object. The choice between shallow copy and deep copy depends on whether you need a completely independent copy of the original object or if shallow copying is sufficient.



<br> 


## What is the difference between localstorage and session storage ? 
Certainly! Here's a table highlighting the key differences between LocalStorage and SessionStorage:

| Feature                | LocalStorage                              | SessionStorage                           |
|------------------------|-------------------------------------------|------------------------------------------|
| **Persistence**        | Until explicitly deleted                  | Until the tab/window is closed           |
| **Scope**              | Shared across all tabs/windows of the same origin | Specific to each tab/window              |
| **Storage Limit**      | Typically 5-10 MB per origin              | Typically about 5 MB per origin          |
| **Use Case Examples**  | User preferences, settings, cached data   | Temporary form data, session-specific data |



<br> 


## Difference between cookies, localstorage and session Storage ? 
Certainly! Here’s a table comparing Cookies, LocalStorage, and SessionStorage:

| Feature                | Cookies                                     | LocalStorage                           | SessionStorage                        |
|------------------------|---------------------------------------------|----------------------------------------|---------------------------------------|
| **Storage Location**   | Browser, sent with every HTTP request       | Browser (client-side only)             | Browser (client-side only)            |
| **Persistence**        | Can be set to expire at a specific time     | Until explicitly deleted               | Until the tab/window is closed        |
| **Scope**              | Domain and path                             | Origin (domain and protocol)           | Origin (domain and protocol)          |
| **Size Limit**         | ~4 KB per cookie                            | 5-10 MB per origin                     | ~5 MB per origin                      |
| **Use Cases**          | Session management, personalization, tracking | Persistent data like settings and preferences | Temporary data like session-specific information |
| **Security Options**   | Secure, HttpOnly flags                      | No inherent security features          | No inherent security features         |
