//------------------------------------object iterations----------------------------------------------

//---using for of----------

```jsx
let obj={ name:"akash",lastname:"dsfdf",email:"qwedsa"}
let i=0;
for(const [key,value] of Object.entries(obj))
{
    if(i<2){
     console.log(key+":"+value)
}
     i++
}
```

//-----using for in----------

//-------------------------------------------------add one more element in each object of an array-------------------------------

```jsx

let obj={ name:"akash",lastname:"dsfdf",email:"qwedsa"}
let i=0;
for(const key in obj)
{
        if(i<2){
           console.log(key+":"+obj[key])
         }
    i++
}
output => [
{ name: 'a', email: 'abc', lastname: '' },
{ name: 'b', email: 'xyz', lastname: '' }
]
```

```
//---using forEach----
```

```jsx

let arr = [
  { name: "a", email: "abc" },
  { name: "b", email: "xyz" },
];

arr.forEach((a) => {
  a.lastname = "";
});
console.log(arr);
(output) => [
  { name: "a", email: "abc", lastname: "" },
  { name: "b", email: "xyz", lastname: "" },
];

```

//------using map---

```jsx

let arr=[{name:"a",email:"abc"},{name:"b",email:"xyz"}]

let arr1=arr.map((a)=>

         { return  {...a,lastname:""} }
)
console.log(arr1)
output => [
{ name: 'a', email: 'abc', lastname: '' },
{ name: 'b', email: 'xyz', lastname: '' }
]
```

//--------------------------------------------remove an element of each object from an array----------------------------------

```jsx
let arr1=
[
    { name: 'a', email: 'abc', lastname: '' },
    { name: 'b', email: 'xyz', lastname: '' }
]

let abc= arr1.map(({lastname,...rest})=>{
return rest
})
console.log(abc)

output=>[ { name: 'a', email: 'abc' }, { name: 'b', email: 'xyz' } ]
```

//-----------------------------------------replace string with link-----------------------------------------------
//-------using for loop and array--------

let text = "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.";

```jsx

export default App;
const arr = text.split(" ");
for (let i = 0; i < arr.length; i++) {
  if (arr[i] == "Lorem") {
    arr[i] = "<a href='#'>link</a>";
  }
}

document.getElementById("demo").innerHTML = arr.join(" ");
output=>link Ipsum is simply dummy text of the printing and typesetting industry. link Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing link Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of link Ipsum
```

//------using replaceAll---------

```jsx
let text =
  "Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.";
const newText = text.replaceAll("Lorem", "<a href='#'>link</a>");
document.getElementById("demo").innerHTML = newText;

```

//---using regex and replace--------------

```jsx

let text =Please visit Microsoft! Microsoft
document.getElementById("demo").innerHTML =
text.replace(/Microsoft/g,"W3Schools");   //(for case insensitive write /microsoft/i)
output=>  Please visit W3Schools! W3Schools
```

//---------------------------------------------------------clouser------------------------------------------------
make a private variable

```jsx

const increment = () => {
  let counter = 0;
  const add = () => {
    counter = counter + 1;
    console.log(counter);
  };
  return add;
};
let add = increment();
add();
add();
add();
(output) => 1;
2;
3;

```

//------------------------------------------------------call apply and bind------------------------------------------
borrowing function from another object

```jsx

const employee = {
  firstname: "abc",
  lastname: "xyz",
  getName(location) {
    console.log(this.firstname + " " + this.lastname + " " + location);
  },
};
const employee1 = {
  firstname: "Akash",
  lastname: "T",
};
employee.getName.call(employee1, "pune");
employee.getName.apply(employee1, ["pune"]);
let fun = employee.getName.bind(employee1, "pune"); // return function borrowed from another object
fun();
output=>
Akash T pune
Akash T pune
Akash T pune
```

//----------------------------------------------------prototype--------------------------------------
with the help of prototype we can achieve the inheritance in javascript

```jsx
let obj1 = {
  name: "yash",
  age: "98",
};
let obj5 = {
  __proto__: obj1,
};

console.log(obj5.name + " " + obj1.age);
// output: yash 98
```

--------add properties to constructor funtion (prototype)-----

```
function Student() {
  this.name = "John";
  this.gender = "M";
}
Student.prototype.age = 15;

var studObj1 = new Student();
document.write('studObj1.age = ' + studObj1.age); // 15

var studObj2 = new Student();
document.write('studObj2.age = ' + studObj2.age); // 15

Student.prototype = { age: 20 };

var studObj3 = new Student();
var studObj4 = new Student();

document.write('studObj3.age = ' + studObj3.age); // 20
document.write('studObj4.age = ' + studObj4.age); // 20
document.write('studObj1.age = ' + studObj1.age); // 15
document.write('studObj2.age = ' + studObj2.age); // 15
```

//-----------------------------------------------------duplicates in an array

```jsx
let arr = ["0", "1", "1", "2", "2", "3", "0"];
let a = arr.reduce((t, ele) => {
  t[ele] = t[ele] ? t[ele] + 1 : 1;
  return t;
}, {});
console.log(a);
// o/p=>
// {0: 2, 1: 2, 2: 2, 3: 1}

```

//---------------------------------------------------string reverse--------

```
let str1="Akash";
console.log(str1.charAt(0))
for(let i=str1.length-1;i>=0;i--){
str=str+str1.charAt(i)
console.log(str)

```

}
//--------------------------------------------------in one loop--------

```jsx

let arr = [8, -2, 3, 4, 5, -11, -5, 6, -8];
//this is the first simple way
for (let i = 0; i < arr.length; i++) {
  if (arr[i] < 0) {
    arr.unshift(arr[i]);
    arr.splice(i + 1, 1);
  }
}

```

//this is second way

```
for (let i = 0; i < arr.length; i++) {
  if (arr[i] > 0 && arr[i + 1] < 0) {
    let temp = arr[i];
    arr[i] = arr[i + 1];
    arr[i + 1] = temp;
    i = -1;
  }
}
console.log(arr);
// o/p [
// -2, -11, -5, -8, 8,
// 3,   4,  5,  6
// ]
```

//------------------------------------------this is  third way

```jsx
let arr = [8, -2, 3, 4, 5, -11, -5, 6, -8];
for (let i = 0; i < arr.length; i++) {
  if (arr[i] < 0) {
    let x = Math.trunc(arr.length / 2) - 1;
    if (x / 2 < i) {
      let t = arr[x - i];
      arr[x - i] = arr[i];
      arr[i] = t;
    }
  }
  if (arr[i] > 0 && arr[i + 1] < 0) {
    let temp = arr[i];
    arr[i] = arr[i + 1];
    arr[i + 1] = temp;
    i = -1;
  }
}
console.log(arr);
// o/p:[
// -8, -11, -5, -2, 8,
// 3,   4,  5,  6
// ]
```

//--------------------------------------addition of two numbers in arr is 10--------

```jsx
let arr = [1, 9, 5, 6, 3, 2, 5, 8, 4];
let j = 1;
for (let i = 0; i < arr.length; ) {
  if (arr[i] + arr[j] == 10) {
    console.log(arr[i] + " " + arr[j]);
  }
  j++;
  if (j == arr.length) {
    i++;
    j = i + 1;
  }
}
o/p:
1 9
5 5
6 4
2 8
```

//-------------------------------------str split logic--------------------------------

```jsx

let count = 0;
let arr = [];
const str = "       this      is  a   str   ";
for (let i = 0; i <= str.length - 1; i++) {
  if (str[i] !== " ") {
    let seprateStr = "";
    for (let j = i; j <= str.length - 1; j++) {
      if (str[j] != " ") seprateStr = seprateStr + str[j];
      if (seprateStr != "" && (str[j] == " " || j == str.length - 1)) {
        count++;
        i = j;
        arr.push(seprateStr);
        break;
      }
    }
  }
}
console.log(count);
console.log(arr);
output: (4)[("this", "is", "a", "str")];
```

//--------------------------------------------

```jsx
const str = "   this is   javascript";
let count = 0;
let inside = false;
for (let i = 0; i < str.length; i++) {
  if (str[i] !== " " && !inside) {
    count++;
    inside = true;
  } else if (str[i] === " " && inside) {
    inside = false;
  }
}
console.log(count);
```

//----------------------------------------------brackets order------

```jsx

const str = "{([()]{}{}()())}";

String.prototype.bracketOrder = function () {
  if (this.length % 2 == 0) {
    let stack = [];
    let count = 0;
    for (let i = 0; i < this.length; i++) {
      if (this[i] == "{" || this[i] == "(" || this[i] == "[") {
        stack.push(this[i]);
        console.log(stack);
        continue;
      }
      if (this[i] == "}" && stack.pop() == "{") {
        count++;
        continue;
      } else if (this[i] == "]" && stack.pop() == "[") {
        count++;
        continue;
      } else if (this[i] == ")" && stack.pop() == "(") {
        count++;
        continue;
      } else break;
    }
    console.log(this.length);

    if (count == this.length / 2) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
};
const output = str.bracketOrder();
console.log(output); //returns boolean

```

}

//-------------------------------------------find the subArray having max sum--------------

```jsx
let arr = [-1, 5, -3, -14, 5, 15, -6];
let max = 0;
firstIndex = 0;
lastIndex = 0;
for (let i = 0; i < arr.length - 1; i++) {
  let sum = 0;
  for (let j = i; j < arr.length; j++) {
    sum = sum + arr[j];
    if (max < sum) {
      max = sum;
      lastIndex = j;
      firstIndex = i;
    }
  }
}
console.log(firstIndex);
console.log(lastIndex);
console.log(max);
```

//----same in one loop------

```jsx
let arr = [3, -1, -5, 5, 3, -5, -6, 3];
let sum = 0;
let max = 0;
for (let i = 0; i < arr.length - 1; i++) {
  sum = sum + arr[i];
  sum = sum > 0 ? sum : 0;
  console.log(sum);
  if (max < sum) {
    max = sum;
  }
}
console.log(max);
```

//-----------------------------------------------------------async calls---

```jsx

console.log("a");
setTimeout(() => {
  console.log("b");
}, 5000);
const fun = async () => {
  setTimeout(() => {
    console.log("c");
  }, 5);
  console.log("inside fun");
  const promise = new Promise((resolve, reject) => {
    resolve("response");
  });
  const res = await promise;
  console.log(res);
  console.log("e");
};
fun();
console.log("d");

// output=>a inside fun d response e c b

```

//-----------------------------------------------map polyfill---

```jsx

Array.prototype.customMap = function (cb) {
  console.log(this);
  let arr = [];
  for (let i = 0; i < this.length; i++) {
    arr.push(cb(this[i], i, this));
  }
  return arr;
};
let arr1 = [1, 2, 3, 4, 5];

const newArr = arr1.customMap((ele, i, arr) => {
  return ele * 2;
});
console.log(newArr);

```

//-------------------------filter polyfill

```jsx
Array.prototype.customFilter = function (cb) {
  console.log(this);
  let arr = [];
  for (let i = 0; i < this.length; i++) {
    if (cb(this[i], i, this)) {
      arr.push(cb(this[i], i, this));
    }
  }
  return arr;
};
let arr1Filter = [1, 2, 3, 4, 5];

const newArrFilter = arr1Filter.customFilter((ele, i, arr) => {
  if (ele > 3) {
    return ele;
  }
});
console.log(newArrFilter);

```

//----------------------------------------------------------

```jsx

let str = "{[(())]}}}";
let arr = [];
let i;
for (i = 0; i < str.length; i++) {
  if (str[i] == "{" || str[i] == "[" || str[i] == "(") {
    arr.push(str[i]);
  } else if (str[i] == "}" && arr.pop() == "{") continue;
  else if (str[i] == "]" && arr.pop() == "[") continue;
  else if (str[i] == ")" && arr.pop() == "(") continue;
  else break;
}
if (i == str.length) {
  console.log("in order");
} else {
  console.log("not in  order");
}

```

//-------------------------------------------is anagram---

```jsx

let isAnagram = (str1, str2) => {
  let obj1 = {};
  let obj2 = {};
  if (str1.length != str2.length) return false;
  for (let i = 0; i < str1.length; i++) {
    obj1[str1[i]] = obj1[str1[i]] ? obj1[str1[i]] + 1 : 1;
    obj2[str2[i]] = obj2[str2[i]] ? obj2[str2[i]] + 1 : 1;
  }
  for (const key in obj1) {
    if (obj1[key] != obj2[key]) return false;
  }
  return true;
};
console.log(isAnagram("oet", "eot"));

```

//---------------------------------------------recursion--------------

```jsx
let i = 1;
function inc() {
  if (i < 11) {
    console.log(i);
    i++;
    return inc();
  }
}
inc();
// output:1 2 3 4 5 6 7 8 9
```

//-------------------------------------addition of two numbers should be targeted number-----

```jsx

const twoAdd = (arr, target) => {
  let obj = {};
  for (let i = 0; i < arr.length; i++) {
    if (obj[target - i] >= 0) {
      //   obj[i]=i

      console.log(target - i, i);
    } else {
      obj[arr[i]] = i;
    }
  }
  console.log(obj);
};
const result = twoAdd([3, 4, 2, 5, 7, 8, 0, 6, 1], 11);
console.log(result);
// output: 3,8
// 4,7
// 5,6
```

//-----------------------------------debounce---

```jsx

function Debounce() {
  const handleChange = (arg) => {
    document.write(arg);
  };

  function debounce(cb, delay) {
    let timer;
    return function (...args) {
      console.log(...args);
      clearTimeout(timer);
      timer = setTimeout(() => cb(...args), delay);
    };
  }
  let handle = debounce(handleChange, 500);
  return (
    <div>
      Debounce
      <input input="text" onChange={(e) => handle(e.target.value)}></input>
    </div>
  );
}

export default Debounce;

```

//-----add number at index position in an array------

```jsx

let arr = [1, 2, 3, 4, 5];
arr[arr.length] = 6;
index = 3;
for (let i = arr.length - 1; i >= index; i--) {
  let temp = arr[i];
  arr[i] = arr[i - 1];
  arr[i - 1] = temp;
}
console.log(arr);

```

//---delete element at index---------

```jsx

let arr = [1, 2, 3, 4, 5];

index = 2;
for (let i = index; i < arr.length; i++) {
  if (i == arr.length - 1) {
    arr[i] = arr[i + 1];
    arr.length = arr.length - 1;
  } else {
    arr[i] = arr[i + 1];
  }
}
console.log(arr);

```

//---------remove extra spaces from string(optimized)--------------

```jsx
let str = "      this   is a  js ";
let str1 = "";
let word = "";
for (let i = 0; i < str.length; i++) {
  if (str[i] != " ") {
    word = word + str[i];
  } else if (word != "") {
    str1 = str1 + " " + word;
    word = "";
  }
}
console.log(str1);

```

//--------------------------------------Promise Methods---------

```jsx

// rejects if any
Promise.all([Promise.resolve("resolve"), Promise.reject("reject")])
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  });
// o/p: reject

// all fulfilled and rejected
Promise.allSettled([Promise.resolve("resolve"), Promise.reject("reject")])
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  });
// o/p:
// [
// { status: 'fulfilled', value: 'resolve' },
// { status: 'rejected', reason: 'reject' }
// ]

// first fulfilled or rejected
Promise.race([Promise.reject("reject"), Promise.resolve("resolve")])
  .then((result) => {
    console.log(result);
  })
  .catch((err) => {
    console.log(err);
  });
// o/p: reject or resolve whichever is faster

// first fulfilled only
Promise.any([Promise.resolve("resolve"), Promise.reject("reject")])
  .then((result) => {
    console.log(result, "any");
  })
  .catch((err) => {
    console.log(err, "any");
  });
// o/p: resolve

```

- --------------------------Promise chaining----------

```jsx
const promise1 = new Promise((resolve, reject) => {
  resolve(1);
});
promise1
  .then((result) => {
    console.log(result);
    return result2;
  })
  .then((result) => {
    console.log(result);
    return result2;
  })
  .then((result) => {
    console.log(result);
    return Promise.reject("reject");
  })
  .then((result) => {
    console.log(result);
    return "result";
  })
  .catch((err) => {
    console.log(err);
  });
// o/P:
// 1
// 2
// 4
// reject

```

## ---------------------------------------subarray-------------

```jsx
let arr = [4, 1, -6, -2, 1, -7, 4, -13, 3, -1, 11, -8, 7];
let sum = 0;
let max = arr[0];
let firstInd;
let lastInd;
for (let i = 0; i < arr.length; i++) {
  sum = sum + arr[i];
  if (sum > max) {
    max = sum;
    lastInd = i;
  }
  if (sum < 0) {
    sum = 0;
    firstInd = i + 1;
  }
}
console.log("max=", max, "firstInd=", firstInd, "lastInd=", lastInd);

```

```jsx
let arr = [5, 4, 3, 8, 9, 6, 7, 0];
let arr1 = [];
for (let i = 0; i < arr.length; i++) {
  let count = 0;
  for (let j = i; j < arr.length; j++) {
    if (arr[j] < arr[i]) {
      count++;
    }
  }
  arr1.push([arr[i], count]);
}
console.log(arr1);
// output:[
// [ 5, 3 ], [ 4, 2 ],
// [ 3, 1 ], [ 8, 3 ],
// [ 9, 3 ], [ 6, 1 ],
// [ 7, 1 ], [ 0, 0 ]
// ]
```

```jsx
const arr = [6, 4, 9, 7, 5];
let obj = {};
for (let i = 0; arr.length; i++) {
  const requireNumber = 11 - arr[i];
  if (requireNumber in obj) {
    console.log([obj[requireNumber], i]);
  }
  obj[arr[i]] = i;
}
output: [1, 3][(0, 4)];
```

------------------- unique elements--

```jsx
let uArr = [3, 5, 8, 65, 3, 4, 5, 1, 4];
let obj1 = {};
let uniqueArray = [];
for (let i = 0; i < uArr.length; i++) {
  obj1[uArr[i]] = obj1[uArr[i]] ? +obj1[uArr[i]] + 1 : 1;
  if (obj1[uArr[i]] <= 1) {
    uniqueArray.push(uArr[i]);
  }
}
console.log(uniqueArray);
output: [3, 5, 8, 65, 4, 1];
```

---------------------------variables----

```jsx

let a = { key: "value", key1: "value2" };
let b = { key: "value", key1: "value2" };
console.log(a == b); // false
a = b;
console.log(a == b); // true
a.key = "value.....";
console.log(b.key); // value.....

console.log([] === []); // false
console.log([] == []); // false

console.log([] == ![]); // true
console.log([] == ![]); // true

console.log(5 + "2"); // 52
console.log(5 + "2" + 7); // 527
console.log(5 + "2" + 7 - 2); // 525
console.log(5 + 8 + "2"); // 132
console.log("3" + "4"); // 34

let p = 4;
let r = p;
console.log(p == r); // true
console.log(p === r); // true

let x = 7;
let y = 7;
console.log(x == y); // true
console.log(x === y); // true

console.log([2, 44] + [99, 50] + [60]); // 2,4499,5060
console.log([] + []); // empty string
console.log({} + {}); // [object Object][object Object]
console.log({ a: "b" } + { a: "c" }); // [object Object][object Object]

console.log(typeof null); // object
console.log(typeof undefined); // undefined
console.log(undefined + null); // NaN;
console.log(null + undefined); // NaN;
console.log(null + 5); // 5
console.log(undefined + 8);
NaN;

console.log(0 == null); // false
console.log(null == undefined); // true
console.log(null === undefined); // false

```
