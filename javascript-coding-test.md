## Programming in JavaScript

### Q1. How to check if object is empty or not in javaScript?

```javascript
function isEmpty(obj) {
  return Object.keys(obj).length === 0;
}
```
---

### Q2. What is the output?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

- A: `20` and `62.83185307179586`
- B: `20` and `NaN`
- C: `20` and `63`
- D: `NaN` and `63`

**Answer: B**

<details><summary><b>Explanation</b></summary>
<p>

Note that the value of `diameter` is a regular function, whereas the value of `perimeter` is an arrow function.

With arrow functions, the `this` keyword refers to its current surrounding scope, unlike regular functions! This means that when we call `perimeter`, it doesn't refer to the shape object, but to its surrounding scope (window for example).

There is no value `radius` on that object, which returns `NaN`.

</p>
</details>

---

### Q3. What will be the output of the following code?

```javascript
var output = (function(x) {
  delete x;
  return x;
})(0);

console.log(output);
```
**Answer: 0**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `0` as output. `delete` operator is used to delete a property from an object. Here `x` is not an object it's **local variable**. `delete` operator doesn't affect local variables.
</p>
</details>

---

### Q4. What will be the output of the following code?

```javascript
var x = 1;
var output = (function () {
  delete x;
  return x;
})();

console.log(output);
```
**Answer: 0**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `1` as output. `delete` operator is used to delete a property from an object. Here `x` is not an object it's **global variable** of type `number`.
</p>
</details>

---

### Q5. What will be the output of the following code?

```javascript
var x = { foo : 1};
var output = (function() {
  delete x.foo;
  return x.foo;
})();

console.log(output);
```
**Answer: undefined**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `undefined` as output. `delete` operator is used to delete a property from an object. Here `x` is an object which has foo as a property and from a self-invoking function, we are deleting the `foo` property of object `x` and after deletion, we are trying to reference deleted property `foo` which result `undefined`.
</p>
</details>

---

### Q6. What will be the output of the following code?

```javascript
var Employee = {
  company: "xyz",
};
var emp1 = Object.create(Employee);
delete emp1.company;
console.log(emp1.company);
```
**Answer: xyz**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `xyz` as output. Here `emp1` object got company as **prototype** property. delete operator doesn't delete prototype property.

`emp1` object doesn't have **company** as its own property. you can test it `console.log(emp1.hasOwnProperty('company')); //output : false` However, we can delete company property directly from `Employee` object using `delete Employee.company` or we can also delete from `emp1` object using `__proto__` property `delete emp1.__proto__.company`.
</p>
</details>

---

### Q7. What is `undefined x 1` in JavaScript

```javascript
var trees = ["redwood", "bay", "cedar", "oak", "maple"];
delete trees[3];
```

<details><summary><b>Explanation</b></summary>
<p>
 - When you run the code above and do `console.log(trees);` in chrome developer console then you will get `["redwood", "bay", "cedar", undefined × 1, "maple"]`.
 - In the recent versions of Chrome you will see the word `empty` of `undefined x 1`.
 - When you run the same code in Firefox browser console then you will get `["redwood", "bay", "cedar", undefined, "maple"]`
  
Clearly we can see that Chrome has its own way of displaying uninitialized index in arrays. However when you check `trees[3] === undefined` in any browser you will get similar output as `true`.

**Note:** Please remember that you need not check for the uninitialized index of the array in  `trees[3] === 'undefined × 1'` it will give an error because `'undefined × 1'` this is just way of displaying an uninitialized index of an array in chrome.
</p>
</details>

---

### Q8. What will be the output of the following code?

```javascript
var trees = ["xyz", "xxxx", "test", "ryan", "apple"];
delete trees[3];
console.log(trees.length);
```
**Answer: 5**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `5` as output. When we used `delete` operator for deleting an array element then, the array length is not affected by this. This holds even if you deleted all elements of an array using `delete` operator.

So when delete operator removes an array element that deleted element is no longer present in the array. In place of value at deleted index `undefined x 1` in **chrome** and `undefined` is placed at the index. If you do `console.log(trees)` output `["xyz", "xxxx", "test", undefined × 1, "apple"]` in Chrome and in Firefox `["xyz", "xxxx", "test", undefined, "apple"]`.
</p>
</details>
 
 ---

### Q9. What will be the output of the following code?

```javascript
var bar = true;
console.log(bar + 0);
console.log(bar + "xyz");
console.log(bar + true);
console.log(bar + false);
```
**Answer: 1,"truexyz, 2, 1**

<details><summary><b>Explanation</b></summary>
<p>
The code above will output `1, "truexyz", 2, 1` as output. Here's a general guideline for the plus operator:

- Number + Number -> Addition
- Boolean + Number -> Addition
- Boolean + Boolean -> Addition
- Number + String -> Concatenation
- String + Boolean -> Concatenation
- String + String -> Concatenation
</p>
</details>

---
 
### Q10. What will be the output of the following code?

```javascript
var z = 1,
  y = (z = typeof y);
console.log(y);
```
**Answer: undefined**

<details><summary><b>Explanation</b></summary>
<p>
The code above will print string `"undefined"` as output. According to associativity rule operator with the same precedence are processed based on their associativity property of operator. Here associativity of the assignment operator is `Right to Left` so first `typeof y` will evaluate first which is string `"undefined"` and assigned to `z` and then `y` would be assigned the value of z. The overall sequence will look like that:

```javascript
var z;
z = 1;
var y;
z = typeof y;
y = z;
```
</p>
</details>

---

### Q11. What will be the output of the following code?

```javascript
// NFE (Named Function Expression)
var foo = function bar() {
  return 12;
};
typeof bar();
```
**Answer: Reference Error**

<details><summary><b>Explanation</b></summary>
<p>
The output will be `Reference Error`. To fix the bug we can try to rewrite the code a little bit:

**Sample 1**

```javascript
var bar = function () {
  return 12;
};
typeof bar();
```

or

**Sample 2**

```javascript
function bar() {
  return 12;
}
typeof bar();
```

The function definition can have only one reference variable as a function name, In **sample 1** `bar` is reference variable which is pointing to `anonymous function` and in **sample 2** we have function statement and `bar` is the function name.

```javascript
var foo = function bar() {
  // foo is visible here
  // bar is visible here
  console.log(typeof bar()); // Works here :)
};
// foo is visible here
// bar is undefined here
```
</p>
</details>

---

### Q12. What is the output of the following?

```javascript
bar();
(function abc() {
  console.log("something");
})();
function bar() {
  console.log("bar got called");
}
```

**Answer: **
```
bar got called
something
```
<details><summary><b>Explanation</b></summary>
<p>
Since the function is called first and defined during parse time the JS engine will try to find any possible parse time definitions and start the execution loop which will mean function is called first even if the definition is post another function.
<p>
</details>

---

### Q13. What is the difference between declaring a function in the formats listed below?

```javascript
var foo = function() {
  // Some code
}
```

```javascript
function bar () {
  // Some code
}
```
<details><summary><b>Explanation</b></summary>
<p>
The main difference is that function `foo` is defined at `run-time` and is called a function expression, whereas function `bar` is defined at `parse time` and is called a function statement. To understand it better, let's take a look at the code below :

```javascript
// Run-Time function declaration
  foo(); // Call foo function here, It will give an error
  var foo = function() {
    console.log("Hi I am inside Foo");
  };
```

```javascript
// Parse-Time function declaration
bar(); // Call bar function here, It will not give an Error
function bar() {
  console.log("Hi I am inside Foo");
}
```
</p>
</details>

---

### Q14. What will be the output of the following code?

```javascript
var salary = "1000$";

(function () {
  console.log("Original salary was " + salary);

  var salary = "5000$";

  console.log("My New Salary " + salary);
})();
```
**Answer: undefined, 5000$ **

<details><summary><b>Explanation</b></summary>
<p>
The code above will output: `undefined, 5000$` because of hoisting. In the code presented above, you might be expecting `salary` to retain it values from outer scope until the point that `salary` was re-declared in the inner scope. But due to `hoisting` salary value was `undefined` instead. To understand it better have a look of the following code, here `salary` variable is hoisted and declared at the top in function scope. When we print its value using `console.log` the result is `undefined`. Afterwards the variable is redeclared and the new value `"5000$"` is assigned to it.

```javascript
var salary = "1000$";

(function () {
  var salary = undefined;
  console.log("Original salary was " + salary);

  salary = "5000$";

  console.log("My New Salary " + salary);
})();
```
</p>
</details>

---

### Q15. JavaScript Regular Expression to validate Email and to test password strength

For Email:

```javascript 
var pattern = /^\w+@[a-zA-Z_]+?\.[a-zA-Z]{2,3}$/;
```

For Password:

```javascript
var newPassword = "Pq5*@a{J";
var regularExpression = new RegExp(
  "^(?=.*[a-z])(?=.*[A-Z])(?=.*[0-9])(?=.*[!@#$%^&*])(?=.{8,})"
);

if (!regularExpression.test(newPassword)) {
  alert(
    "Password should contain atleast one number and one special character !"
  );
}
```

---

### Q16. How to compare objects ES6?

Example 01:

```javascript
const matches = (obj, source) =>
  Object.keys(source).every(
    (key) => obj.hasOwnProperty(key) && obj[key] === source[key]
  );

console.log(
  matches({ age: 25, hair: "long", beard: true }, { hair: "long", beard: true })
); // true
console.log(
  matches({ hair: "long", beard: true }, { age: 25, hair: "long", beard: true })
); // false
console.log(
  matches({ hair: "long", beard: true }, { age: 26, hair: "long", beard: true })
); // false
```

Example 02:

```javascript
const k1 = { fruit: "🥝" };
const k2 = { fruit: "🥝" };

// Using JavaScript
JSON.stringify(k1) === JSON.stringify(k2); // true
```

Example 03:

```javascript
const one = {
  fruit: "🥝",
  energy: "255kJ",
};

const two = {
  energy: "255kJ",
  fruit: "🥝",
};

// Using JavaScript
JSON.stringify(one) === JSON.stringify(two); // false
```
---

### Q17. How to remove array element based on object property?

```javascript
var myArray = [
  { field: "id", operator: "eq" },
  { field: "cStatus", operator: "eq" },
  { field: "money", operator: "eq" },
];

myArray = myArray.filter(function (obj) {
  return obj.field !== "money";
});

Console.log(myArray);
```

**Answer: **

```
myArray = [
    {field: "id", operator: "eq"}
    {field: "cStatus", operator: "eq"}
]
```

---

### Q18. Predict the output of the following JavaScript code?

```javascript
console.log(+"meow");
```
**Answer: NaN **

---

### Q19. Predict the output of the following JavaScript code?

```javascript
var result;
for (var i = 5; i > 0; i--) {
  result = result + i;
}
console.log(result);
```
**Answer: NaN **

---

### Q20. Predict the output of the following JavaScript code?

```javascript
var a = 1.2;
console.log(typeof a);
```
**Answer: Number **

---

### Q21. Predict the output of the following JavaScript code?

```javascript
var x = 10;
if (x) {
  let x = 4;
}
console.log(x); 
```
**Answer: 10 **

---

### Q22. Predict the output of the following JavaScript code?

```javascript
console.log(0.1 + 0.2 == 0.3);
```
**Answer: false **

---

### Q23. Predict the output of the following JavaScript code?

```javascript
console.log(1 + -"1" + 2);
```
**Answer: 2 **

---

### Q24. Predict the output of the following JavaScript code?

```javascript
(function (x) {
  return (function (y) {
    console.log(x);
  })(10);
})(20);
```
**Answer: 20 **

---

### Q25. Predict the output of the following JavaScript code?

```javascript
var num = 20;
var getNumber = function () {
  console.log(num);
  var num = 10;
};
getNumber();
```
**Answer: undefined **

---

### Q26. Predict the output of the following JavaScript code?

```javascript
function f1() {
  num = 10;
}
f1();
console.log("window.num: " + window.num);
```
**Answer: 10 **

---

### Q27. Predict the output of the following JavaScript code?

```javascript
console.log("(null + undefined): " + (null + undefined));
```
**Answer: NaN **

---

### Q28. Predict the output of the following JavaScript code?

```javascript
(function () {
  var a = (b = 3);
})();

console.log("value of a : " + a);
console.log("value of b : " + b);
```
**Answer: undefined 3 **

---

### Q29. Predict the output of the following JavaScript code?

```javascript
var y = 1;
if (function f() {}) {
  y += typeof f;
}
console.log(y);
```
**Answer: 10object **

---

### Q30. Predict the output of the following JavaScript code?

```javascript
var k = 1;
if (1) {
  eval(function foo() {});
  k += typeof foo;
}
console.log(k);
```
**Answer: 1undefined **

---

### Q31. Predict the output of the following JavaScript code?

```javascript
var k = 1;
if (1) {
  function foo() {}
  k += typeof foo;
}
console.log(k);
```
**Answer: 1function **

---

### Q32. Predict the output of the following JavaScript code?

```javascript
console.log("(-1 / 0): " + -1 / 0); 
console.log("(1 / 0): " + 1 / 0);
console.log("(0 / 0): " + 0 / 0); 
console.log("(0 / 1): " + 0 / 1);
```
**Answer: -Infinity  Infinity  NaN  0 **

---

### Q33. Predict the output of the following JavaScript code?

```javascript
var a = 4;
var b = "5";
var c = 6;

console.log("(a + b): " + (a + b));
console.log("(a - b): " + (a - b));
console.log("(a * b): " + a * b);
console.log("(a / b): " + a / b);
console.log("(a % b): " + (a % b));
```

**Answer: 45  -1  20  0.8  4 **

---

### Q34. Predict the output of the following JavaScript code?

```javascript
console.log("MAX : " + Math.max(10, 2, NaN));
console.log("MAX : " + Math.max());
```
**Answer: NaN  -Infinity **

---

### Q35. Predict the output of the following JavaScript code?

```javascript
(function () {
  var a = (b = 3);
})();

console.log("a defined? " + (typeof a !== "undefined"));
console.log("b defined? " + (typeof b !== "undefined"));
```
**Answer: true  true **

---

### Q36. Predict the output of the following JavaScript code?

```javascript
var myObject = {
  foo: "bar",
  func: function () {
    var self = this;
    console.log("outer func:  this.foo = " + this.foo); // Output: this.foo = bar
    console.log("outer func:  self.foo = " + self.foo); // Output: self.foo = bar
    (function () {
      console.log("inner func:  this.foo = " + this.foo); // Output: this.foo = function foo() {}
      console.log("inner func:  self.foo = " + self.foo); // Output: self.foo = bar
    })();
  },
};
myObject.func();
```
**Answer: bar  bar  function foo() {}   bar **

---


### Q37. Predict the output of the following JavaScript code?

```javascript
console.log(0.1 + 0.2);
console.log(0.1 + 0.2 == 0.3);
```
**Answer: 0.30000000000000004  false **

---

### Q38. Predict the output of the following JavaScript code?

```javascript
(function () {
  console.log(1);
  setTimeout(function () {
    console.log(2);
  }, 1000);
  setTimeout(function () {
    console.log(3);
  }, 0);
  console.log(4);
})();
```
**Answer: 1, 4, 3, 2 **

---

### Q39. Predict the output of the following JavaScript code?

```javascript
var arr1 = "john".split("");
var arr2 = arr1.reverse();
var arr3 = "jones".split("");
arr2.push(arr3);
console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1)); //array 1: length=5 last=j,o,n,e,s
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1)); //array 2: length=5 last=j,o,n,e,s
```
**Answer: 
array 1 : length=5 last=j,o,n,e,s
array 2 : length=5 last=j,o,n,e,s
**

---

### Q40. Predict the output of the following JavaScript code?

```javascript
console.log(1 + "2" + "2"); 
console.log(1 + +"2" + "2"); 
console.log(1 + -"1" + "2");
console.log(+"1" + "1" + "2");
console.log("A" - "B" + "2"); 
console.log("A" - "B" + 2);
```
**Answer: 122  32  02  112  NaN2  NaN**

---

### Q. Predict the output of the following JavaScript code?

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}
// Output: 145, 5, 5, 5, 5, 5
```

### Q. Predict the output of the following JavaScript code?

```javascript
for (var i = 0; i < 5; i++) {
  (function (x) {
    setTimeout(function () {
      console.log(x);
    }, x * 1000);
  })(i);
}
//Output:- 0, 1, 2, 3, 4
```

### Q. Predict the output of the following JavaScript code?

```javascript
console.log("0 || 1 = " + (0 || 1)); // Output: 1
console.log("1 || 2 = " + (1 || 2)); // Output: 1
console.log("0 && 1 = " + (0 && 1)); // Output: 0
console.log("1 && 2 = " + (1 && 2)); // Output: 2
```

---

### Q. Predict the output of the following JavaScript code?

```javascript
console.log(false == "0"); // Output: true
console.log(false === "0"); // Output: false
```

### Q. Predict the output of the following JavaScript code?

```javascript
var a = {},
  b = { key: "b" },
  c = { key: "c" };

a[b] = 123;
a[c] = 456;
console.log(a[b]); // Output: 456
```

### Q. Predict the output of the following JavaScript code?

```javascript
console.log(
  (function f(n) {
    return n > 1 ? n * f(n - 1) : n;
  })(10)
); // Output: 3628800
```

### Q. Predict the output of the following JavaScript code?

```javascript
(function (x) {
  return (function (y) {
    console.log(x); //1
  })(2);
})(1);
```

---

### Q. Predict the output of the following JavaScript code?

```javascript
var hero = {
  _name: "John Doe",
  getSecretIdentity: function () {
    return this._name;
  },
};
var stoleSecretIdentity = hero.getSecretIdentity;

console.log(stoleSecretIdentity()); // Output: undefined
console.log(hero.getSecretIdentity()); // Output: John Doe
```

### Q. Predict the output of the following JavaScript code?

```javascript
var length = 10;
function fn() {
  console.log(this.length);
}

var obj = {
  length: 5,
  method: function (fn) {
    fn();
    arguments[0]();
  },
};

obj.method(fn, 1);
//Output: 10, 2
```

---

### Q. Predict the output of the following JavaScript code?

```javascript
(function () {
  try {
    throw new Error();
  } catch (x) {
    var x = 1,
      y = 2;
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
//Output:  1, undefined, 2
```

### Q. Predict the output of the following JavaScript code?

```javascript
var x = 21;
var girl = function () {
  console.log(x); // Output: undefined
  var x = 20;
};
girl();
```
---

### Q. Predict the output of the following JavaScript code?

```javascript
console.log(1 < 2 < 3); // Output: true
console.log(3 > 2 > 1); // Output: false
```

---

### Q. Predict the output of the following JavaScript code?

```javascript
var b = 1;
function outer() {
  var b = 2;
  function inner() {
    b++;
    var b = 3;
    console.log(b); //3
  }
  inner();
}
outer();
```

---

### Q. Hoisting example in javascript

```javascript
x = 10;
console.log(x);
var x; // Output: 10
```

### Q. Predict the output of the following JavaScript code?

```javascript
const arr = [1, 2];
arr.push(3); // Output: 1, 2, 3
```

### Q. Predict the output of the following JavaScript code?

```javascript
var o = new F();
o.constructor === F;
```

---

### Q. Predict the output of the following JavaScript code?

```javascript
let sum = (a, b) => {
  a + b;
};
console.log(sum(10, 20)); // Output: undefined; return keyword is missing
```

### Q. Predict the output of the following JavaScript code?

```javascript
var arr = ["javascript", "typescript", "es6"];
var searchValue = (value) => {
  return arr.filter((item) => {
    return item.indexOf(value) > -1;
  });
};
console.log(searchValue("script"));
```

### Q. Write the program using fatarrow function?

```javascript
var a = [1, 2, 3, 4];
function sumUsingFunction(acc, value) {
  return acc + value;
}
var sumOfArrayUsingFunc = a.reduce(sumUsingFunc);
```

### Q. Write a program that prints the numbers from 1 to 15. But for multiples of three print “Fizz” instead of the number and for the multiples of five print “Buzz”. For numbers which are multiples of both three and five print “FizzBuzz”?

```javascript
for (var i = 1; i <= 15; i++) {
  if (i % 15 == 0) console.log("FizzBuzz");
  else if (i % 3 == 0) console.log("Fizz");
  else if (i % 5 == 0) console.log("Buzz");
  else console.log(i);
}
```

Output:

```
1
2
Fizz
4
Buzz
Fizz
7
8
Fizz
Buzz
11
Fizz
13
14
FizzBuzz
```

Solution - 02

```javascript
for (var i = 1; i <= 15; i++) {
  var f = i % 3 == 0,
    b = i % 5 == 0;
  console.log(f ? (b ? "FizzBuzz" : "Fizz") : b ? "Buzz" : i);
}
```

---

### Q. What would be the output of the following code?

```javascript
function User(name) {
  this.name = name || "JsGeeks";
}

var person = (new User("xyz")["location"] = "USA");
console.log(person);
```

The output of above code would be `"USA"`. Here `new User("xyz")` creates a brand new object and created property `location` on that and `USA` has been assigned to object property location and that has been referenced by the person.

Let say `new User("xyz")` created a object called `foo`. The value `"USA"` will be assigned to `foo["location"]`, but according to [ECMAScript Specification](http://www.ecma-international.org/ecma-262/6.0/#sec-assignment-operators-runtime-semantics-evaluation) , pt 12.14.4 the assignment will itself return the rightmost value: in our case it's `"USA"`.
Then it will be assigned to person.

To better understand What is going on here, try to execute this code in console, line by line:

```javascript
function User(name) {
  this.name = name || "JsGeeks";
}

var person;
var foo = new User("xyz");
foo["location"] = "USA";
// the console will show you that the result of this is "USA"
```

---

### Q. What would be the output of following code?

```javascript
var strA = "hi there";
var strB = strA;
strB = "bye there!";
console.log(strA);
```

The output will `'hi there'` because we're dealing with strings here. Strings are
passed by value, that is, copied.

---

### Q. What would be the output of following code?

```javascript
var objA = { prop1: 42 };
var objB = objA;
objB.prop1 = 90;
console.log(objA);
```

The output will `{prop1: 90}` because we're dealing with objects here. Objects are
passed by reference, that is, `objA` and `objB` point to the same object in memory.

### Q. What would be the output of following code?

```javascript
var objA = { prop1: 42 };
var objB = objA;
objB = {};
console.log(objA);
```

The output will `{prop1: 42}`.

When we assign `objA` to `objB`, the `objB` variable will point
to the same object as the `objB` variable.

However, when we reassign `objB` to an empty object, we simply change where `objB` variable references to.
This doesn't affect where `objA` variable references to.

---

### Q. What would be the output of following code?

```javascript
var arrA = [0, 1, 2, 3, 4, 5];
var arrB = arrA;
arrB[0] = 42;
console.log(arrA);
```

The output will be `[42,1,2,3,4,5]`.

Arrays are object in JavaScript and they are passed and assigned by reference. This is why
both `arrA` and `arrB` point to the same array `[0,1,2,3,4,5]`. That's why changing the first
element of the `arrB` will also modify `arrA`: it's the same array in the memory.

### Q. What would be the output of following code?

```javascript
var arrA = [0, 1, 2, 3, 4, 5];
var arrB = arrA.slice();
arrB[0] = 42;
console.log(arrA);
```

The output will be `[0,1,2,3,4,5]`.

The `slice` function copies all the elements of the array returning the new array. That's why
`arrA` and `arrB` reference two completely different arrays.

---

### Q. What would be the output of following code?

```javascript
var arrA = [
  { prop1: "value of array A!!" },
  { someProp: "also value of array A!" },
  3,
  4,
  5,
];
var arrB = arrA;
arrB[0].prop1 = 42;
console.log(arrA);
```

The output will be `[{prop1: 42}, {someProp: "also value of array A!"}, 3,4,5]`.

Arrays are object in JS, so both varaibles arrA and arrB point to the same array. Changing
`arrB[0]` is the same as changing `arrA[0]`

### Q. What would be the output of following code?

```javascript
var arrA = [
  { prop1: "value of array A!!" },
  { someProp: "also value of array A!" },
  3,
  4,
  5,
];
var arrB = arrA.slice();
arrB[0].prop1 = 42;
arrB[3] = 20;
console.log(arrA);
```

The output will be `[{prop1: 42}, {someProp: "also value of array A!"}, 3,4,5]`.

The `slice` function copies all the elements of the array returning the new array. However,
it doesn't do deep copying. Instead it does shallow copying. You can imagine slice implemented like this:

```javascript
function slice(arr) {
  var result = [];
  for (i = 0; i < arr.length; i++) {
    result.push(arr[i]);
  }
  return result;
}
```

Look at the line with `result.push(arr[i])`. If `arr[i]` happens to be a number or string,
it will be passed by value, in other words, copied. If `arr[i]` is an object, it will be passed by reference.

In case of our array `arr[0]` is an object `{prop1: "value of array A!!"}`. Only the reference
to this object will be copied. This effectively means that arrays arrA and arrB share first
two elements.

This is why changing the property of `arrB[0]` in `arrB` will also change the `arrA[0]`.

---

### Q. console.log(employeeId);

1.  Some Value
2.  Undefined
3.  Type Error
4.  ReferenceError: employeeId is not defined

_Answer:_ 4) ReferenceError: employeeId is not defined

### Q. What would be the output of following code?

```javascript
console.log(employeeId);
var employeeId = "19000";
```

1.  Some Value
2.  undefined
3.  Type Error
4.  ReferenceError: employeeId is not defined

_Answer:_ 2) undefined

### Q. What would be the output of following code?

```javascript
var employeeId = "1234abe";
(function () {
  console.log(employeeId);
  var employeeId = "122345";
})();
```

1.  '122345'
2.  undefined
3.  Type Error
4.  ReferenceError: employeeId is not defined

_Answer:_ 2) undefined

---

### Q. What would be the output of following code?

```javascript
var employeeId = "1234abe";
(function () {
  console.log(employeeId);
  var employeeId = "122345";
  (function () {
    var employeeId = "abc1234";
  })();
})();
```

1.  '122345'
2.  undefined
3.  '1234abe'
4.  ReferenceError: employeeId is not defined

_Answer:_ 2) undefined

### Q. What would be the output of following code?

```javascript
(function () {
  console.log(typeof displayFunc);
  var displayFunc = function () {
    console.log("Hi I am inside displayFunc");
  };
})();
```

1.  undefined
2.  function
3.  'Hi I am inside displayFunc'
4.  ReferenceError: displayFunc is not defined

_Answer:_ 1) undefined

---

### Q. What would be the output of following code?

```javascript
var employeeId = "abc123";
function foo() {
  employeeId = "123bcd";
  return;
}
foo();
console.log(employeeId);
```

1.  undefined
2.  '123bcd'
3.  'abc123'
4.  ReferenceError: employeeId is not defined

_Answer:_ 2) '123bcd'

### Q. What would be the output of following code?

```javascript
var employeeId = "abc123";

function foo() {
  employeeId = "123bcd";
  return;

  function employeeId() {}
}
foo();
console.log(employeeId);
```

1.  undefined
2.  '123bcd'
3.  'abc123'
4.  ReferenceError: employeeId is not defined

_Answer:_ 3) 'abc123'

---

### Q. What would be the output of following code?

```javascript
var employeeId = "abc123";

function foo() {
  employeeId();
  return;

  function employeeId() {
    console.log(typeof employeeId);
  }
}
foo();
```

1.  undefined
2.  function
3.  string
4.  ReferenceError: employeeId is not defined

_Answer:_ 2) 'function'

### Q. What would be the output of following code?

```javascript
function foo() {
  employeeId();
  var product = "Car";
  return;

  function employeeId() {
    console.log(product);
  }
}
foo();
```

1.  undefined
2.  Type Error
3.  'Car'
4.  ReferenceError: product is not defined

_Answer:_ 1) undefined

---

### Q. What would be the output of following code?

```javascript
(function foo() {
  bar();

  function bar() {
    abc();
    console.log(typeof abc);
  }

  function abc() {
    console.log(typeof bar);
  }
})();
```

1.  undefined undefined
2.  Type Error
3.  function function
4.  ReferenceError: bar is not defined

_Answer:_ 3) function function

---

### Q. What would be the output of following code?

```javascript
(function () {
  "use strict";

  var person = {
    name: "John",
  };
  person.salary = "10000$";
  person["country"] = "USA";

  Object.defineProperty(person, "phoneNo", {
    value: "8888888888",
    enumerable: true,
  });

  console.log(Object.keys(person));
})();
```

1.  Type Error
2.  undefined
3.  ["name", "salary", "country", "phoneNo"]
4.  ["name", "salary", "country"]

_Answer:_ 3) ["name", "salary", "country", "phoneNo"]

---

### Q. What would be the output of following code?

```javascript
(function () {
  "use strict";

  var person = {
    name: "John",
  };
  person.salary = "10000$";
  person["country"] = "USA";

  Object.defineProperty(person, "phoneNo", {
    value: "8888888888",
    enumerable: false,
  });

  console.log(Object.keys(person));
})();
```

1.  Type Error
2.  undefined
3.  ["name", "salary", "country", "phoneNo"]
4.  ["name", "salary", "country"]

_Answer:_ 4) ["name", "salary", "country"]

---

### Q. What would be the output of following code?

```javascript
(function () {
  var objA = {
    foo: "foo",
    bar: "bar",
  };
  var objB = {
    foo: "foo",
    bar: "bar",
  };
  console.log(objA == objB);
  console.log(objA === objB);
})();
```

1.  false true
2.  false false
3.  true false
4.  true true

_Answer:_ 2) false false

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = new Object({ foo: "foo" });
  var objB = new Object({ foo: "foo" });
  console.log(objA == objB);
  console.log(objA === objB);
})();
```

1.  false true
2.  false false
3.  true false
4.  true true

_Answer:_ 2) false false

---

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = Object.create({
    foo: "foo",
  });
  console.log(objA == objB);
  console.log(objA === objB);
})();
```

1.  false true
2.  false false
3.  true false
4.  true true

_Answer:_ 2) false false

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = Object.create(objA);
  console.log(objA == objB);
  console.log(objA === objB);
})();
```

1.  false true
2.  false false
3.  true false
4.  true true

_Answer:_ 2) false false

---

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = Object.create(objA);
  console.log(objA.toString() == objB.toString());
  console.log(objA.toString() === objB.toString());
})();
```

1.  false true
2.  false false
3.  true false
4.  true true

_Answer:_ 4) true true

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = objA;
  console.log(objA == objB);
  console.log(objA === objB);
  console.log(objA.toString() == objB.toString());
  console.log(objA.toString() === objB.toString());
})();
```

1.  true true true false
2.  true false true true
3.  true true true true
4.  true true false false

_Answer:_ 3) true true true true

---

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = objA;
  objB.foo = "bar";
  console.log(objA.foo);
  console.log(objB.foo);
})();
```

1.  foo bar
2.  bar bar
3.  foo foo
4.  bar foo

_Answer:_ 2) bar bar

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = Object.create({
    foo: "foo",
  });
  var objB = objA;
  objB.foo = "bar";

  delete objA.foo;
  console.log(objA.foo);
  console.log(objB.foo);
})();
```

1.  foo bar
2.  bar bar
3.  foo foo
4.  bar foo

_Answer:_ 3) foo foo

---

### Q. What would be the output of following code ?

```javascript
(function () {
  var objA = {
    foo: "foo",
  };
  var objB = objA;
  objB.foo = "bar";

  delete objA.foo;
  console.log(objA.foo);
  console.log(objB.foo);
})();
```

1.  foo bar
2.  undefined undefined
3.  foo foo
4.  undefined bar

_Answer:_ 2) undefined undefined

### Q. What would be the output of following code?

```javascript
(function () {
  var array = new Array("100");
  console.log(array);
  console.log(array.length);
})();
```

1.  undefined undefined
2.  [undefined × 100] 100
3.  ["100"] 1
4.  ReferenceError: array is not defined

_Answer:_ 3) ["100"] 1

---

### Q. What would be the output of following code?

```javascript
(function () {
  var array1 = [];
  var array2 = new Array(100);
  var array3 = new Array(["1", 2, "3", 4, 5.6]);
  console.log(array1);
  console.log(array2);
  console.log(array3);
  console.log(array3.length);
})();
```

1.  [] [] [Array[5]] 1
2.  [] [undefined × 100] Array[5] 1
3.  [] [] ['1',2,'3',4,5.6] 5
4.  [] [] [Array[5]] 5

_Answer:_ 1) [] [] [Array[5]] 1

### Q. What would be the output of following code?

```javascript
(function () {
  var array = new Array("a", "b", "c", "d", "e");
  array[10] = "f";
  delete array[10];
  console.log(array.length);
})();
```

1.  11
2.  5
3.  6
4.  undefined

_Answer:_ 1) 11

---

### Q. What would be the output of following code?

```javascript
(function () {
  var animal = ["cow", "horse"];
  animal.push("cat");
  animal.push("dog", "rat", "goat");
  console.log(animal.length);
})();
```

1.  4
2.  5
3.  6
4.  undefined

_Answer:_ 3) 6

### Q. What would be the output of following code?

```javascript
(function () {
  var animal = ["cow", "horse"];
  animal.push("cat");
  animal.unshift("dog", "rat", "goat");
  console.log(animal);
})();
```

1.  [ 'dog', 'rat', 'goat', 'cow', 'horse', 'cat' ]
2.  [ 'cow', 'horse', 'cat', 'dog', 'rat', 'goat' ]
3.  Type Error
4.  undefined

_Answer:_ 1) [ 'dog', 'rat', 'goat', 'cow', 'horse', 'cat' ]

---

### Q. What would be the output of following code?

```javascript
(function () {
  var array = [1, 2, 3, 4, 5];
  console.log(array.indexOf(2));
  console.log([{ name: "John" }, { name: "John" }].indexOf({ name: "John" }));
  console.log([[1], [2], [3], [4]].indexOf([3]));
  console.log("abcdefgh".indexOf("e"));
})();
```

1.  1 -1 -1 4
2.  1 0 -1 4
3.  1 -1 -1 -1
4.  1 undefined -1 4

_Answer:_ 1) 1 -1 -1 4

### Q. What would be the output of following code?

```javascript
(function () {
  var array = [1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 6];
  console.log(array.indexOf(2));
  console.log(array.indexOf(2, 3));
  console.log(array.indexOf(2, 10));
})();
```

1.  1 -1 -1
2.  1 6 -1
3.  1 1 -1
4.  1 undefined undefined

_Answer:_ 2) 1 6 -1

---

### Q. What would be the output of following code?

```javascript
(function () {
  var numbers = [2, 3, 4, 8, 9, 11, 13, 12, 16];
  var even = numbers.filter(function (element, index) {
    return element % 2 === 0;
  });
  console.log(even);

  var containsDivisibleby3 = numbers.some(function (element, index) {
    return element % 3 === 0;
  });

  console.log(containsDivisibleby3);
})();
```

1.  [ 2, 4, 8, 12, 16 ] [ 0, 3, 0, 0, 9, 0, 12]
2.  [ 2, 4, 8, 12, 16 ] [ 3, 9, 12]
3.  [ 2, 4, 8, 12, 16 ] true
4.  [ 2, 4, 8, 12, 16 ] false

_Answer:_ 3) [ 2, 4, 8, 12, 16 ] true

### Q. What would be the output of following code?

```javascript
(function () {
  var containers = [2, 0, false, "", "12", true];
  var containers = containers.filter(Boolean);
  console.log(containers);
  var containers = containers.filter(Number);
  console.log(containers);
  var containers = containers.filter(String);
  console.log(containers);
  var containers = containers.filter(Object);
  console.log(containers);
})();
```

1. [ 2, '12', true ]
   [ 2, '12', true ]
   [ 2, '12', true ]
   [ 2, '12', true ]
2. [false, true]
   [ 2 ]
   ['12']
   [ ]
3. [2,0,false,"", '12', true]
   [2,0,false,"", '12', true]
   [2,0,false,"", '12', true]
   [2,0,false,"", '12', true]
4. [ 2, '12', true ]
   [ 2, '12', true, false ]
   [ 2, '12', true,false ]
   [ 2, '12', true,false]

_Answer:_ 1) [ 2, '12', true ]
[ 2, '12', true ]
[ 2, '12', true ]
[ 2, '12', true ]

---

### Q. What would be the output of following code?

```javascript
(function () {
  var list = ["foo", "bar", "john", "ritz"];
  console.log(list.slice(1));
  console.log(list.slice(1, 3));
  console.log(list.slice());
  console.log(list.slice(2, 2));
  console.log(list);
})();
```

1. [ 'bar', 'john', 'ritz' ]
   [ 'bar', 'john' ]
   [ 'foo', 'bar', 'john', 'ritz' ]
   []
   [ 'foo', 'bar', 'john', 'ritz' ]
2. [ 'bar', 'john', 'ritz' ]
   [ 'bar', 'john','ritz ]
   [ 'foo', 'bar', 'john', 'ritz' ]
   []
   [ 'foo', 'bar', 'john', 'ritz' ]
3. [ 'john', 'ritz' ]
   [ 'bar', 'john' ]
   [ 'foo', 'bar', 'john', 'ritz' ]
   []
   [ 'foo', 'bar', 'john', 'ritz' ]
4. [ 'foo' ]
   [ 'bar', 'john' ]
   [ 'foo', 'bar', 'john', 'ritz' ]
   []
   [ 'foo', 'bar', 'john', 'ritz' ]

_Answer:_ 1) [ 'bar', 'john', 'ritz' ]
[ 'bar', 'john' ]
[ 'foo', 'bar', 'john', 'ritz' ]
[]
[ 'foo', 'bar', 'john', 'ritz' ]

### Q. What would be the output of following code?

```javascript
(function () {
  var list = ["foo", "bar", "john"];
  console.log(list.splice(1));
  console.log(list.splice(1, 2));
  console.log(list);
})();
```

1.  [ 'bar', 'john' ] [] [ 'foo' ]
2.  [ 'bar', 'john' ] [] [ 'bar', 'john' ]
3.  [ 'bar', 'john' ] [ 'bar', 'john' ] [ 'bar', 'john' ]
4.  [ 'bar', 'john' ] [] []

_Answer:_ 1. [ 'bar', 'john' ] [] [ 'foo' ]

---

### Q. What would be the output of following code?

```javascript
(function () {
  var arrayNumb = [2, 8, 15, 16, 23, 42];
  arrayNumb.sort();
  console.log(arrayNumb);
})();
```

1.  [2, 8, 15, 16, 23, 42]
2.  [42, 23, 26, 15, 8, 2]
3.  [ 15, 16, 2, 23, 42, 8 ]
4.  [ 2, 8, 15, 16, 23, 42 ]

_Answer:_ 3. [ 15, 16, 2, 23, 42, 8 ]

### Q. What would be the output of following code?

```javascript
function funcA() {
  console.log("funcA ", this);
  (function innerFuncA1() {
    console.log("innerFunc1", this);
    (function innerFunA11() {
      console.log("innerFunA11", this);
    })();
  })();
}

console.log(funcA());
```

1.  funcA Window {...}
    innerFunc1 Window {...}
    innerFunA11 Window {...}
2.  undefined
3.  Type Error
4.  ReferenceError: this is not defined

_Answer:_ 1)

---

### Q. What would be the output of following code?

```javascript
var obj = {
  message: "Hello",
  innerMessage: !(function () {
    console.log(this.message);
  })(),
};

console.log(obj.innerMessage);
```

1.  ReferenceError: this.message is not defined
2.  undefined
3.  Type Error
4.  undefined true

_Answer:_ 4) undefined true

### Q. What would be the output of following code?

```javascript
var obj = {
  message: "Hello",
  innerMessage: function () {
    return this.message;
  },
};

console.log(obj.innerMessage());
```

1.  Hello
2.  undefined
3.  Type Error
4.  ReferenceError: this.message is not defined

_Answer:_ 1) Hello

---

### Q. What would be the output of following code?

```javascript
var obj = {
  message: "Hello",
  innerMessage: function () {
    (function () {
      console.log(this.message);
    })();
  },
};
console.log(obj.innerMessage());
```

1.  Type Error
2.  Hello
3.  undefined
4.  ReferenceError: this.message is not defined

_Answer:_ 3) undefined

### Q. What would be the output of following code?

```javascript
var obj = {
  message: "Hello",
  innerMessage: function () {
    var self = this;
    (function () {
      console.log(self.message);
    })();
  },
};
console.log(obj.innerMessage());
```

1.  Type Error
2.  'Hello'
3.  undefined
4.  ReferenceError: self.message is not defined

_Answer:_ 2) 'Hello'

---

### Q. What would be the output of following code?

```javascript
function myFunc() {
  console.log(this.message);
}
myFunc.message = "Hi John";

console.log(myFunc());
```

1.  Type Error
2.  'Hi John'
3.  undefined
4.  ReferenceError: this.message is not defined

_Answer:_ 3) undefined

### Q. What would be the output of following code?

```javascript
function myFunc() {
  console.log(myFunc.message);
}
myFunc.message = "Hi John";

console.log(myFunc());
```

1.  Type Error
2.  'Hi John'
3.  undefined
4.  ReferenceError: this.message is not defined

_Answer:_ 2) 'Hi John'

---

### Q. What would be the output of following code?

```javascript
function myFunc() {
  myFunc.message = "Hi John";
  console.log(myFunc.message);
}
console.log(myFunc());
```

1.  Type Error
2.  'Hi John'
3.  undefined
4.  ReferenceError: this.message is not defined

_Answer:_ 2) 'Hi John'

### Q. What would be the output of following code?

```javascript
function myFunc(param1, param2) {
  console.log(myFunc.length);
}
console.log(myFunc());
console.log(myFunc("a", "b"));
console.log(myFunc("a", "b", "c", "d"));
```

1.  2 2 2
2.  0 2 4
3.  undefined
4.  ReferenceError

_Answer:_ a) 2 2 2

---

### Q. What would be the output of following code?

```javascript
function myFunc() {
  console.log(arguments.length);
}
console.log(myFunc());
console.log(myFunc("a", "b"));
console.log(myFunc("a", "b", "c", "d"));
```

1.  2 2 2
2.  0 2 4
3.  undefined
4.  ReferenceError

_Answer:_ 2) 0 2 4

### Q. What would be the output of following code?

```javascript
function Person(name, age) {
  this.name = name || "John";
  this.age = age || 24;
  this.displayName = function () {
    console.log(this.name);
  };
}

Person.name = "John";
Person.displayName = function () {
  console.log(this.name);
};

var person1 = new Person("John");
person1.displayName();
Person.displayName();
```

1.  John Person
2.  John John
3.  John undefined
4.  John John

_Answer:_ 1) John Person

---

### Q. What would be the output of following code?

```javascript
function passWordMngr() {
  var password = "12345678";
  this.userName = "John";
  return {
    pwd: password,
  };
}
// Block End
var userInfo = passWordMngr();
console.log(userInfo.pwd);
console.log(userInfo.userName);
```

1.  12345678 Window
2.  12345678 John
3.  12345678 undefined
4.  undefined undefined

_Answer:_ 3) 12345678 undefined

### Q. What would be the output of following code?

```javascript
var employeeId = "aq123";
function Employee() {
  this.employeeId = "bq1uy";
}
console.log(Employee.employeeId);
```

1.  Reference Error
2.  aq123
3.  bq1uy
4.  undefined

_Answer:_ 4) undefined

---

### Q. What would be the output of following code?

```javascript
var employeeId = "aq123";

function Employee() {
  this.employeeId = "bq1uy";
}
console.log(new Employee().employeeId);
Employee.prototype.employeeId = "kj182";
Employee.prototype.JobId = "1BJKSJ";
console.log(new Employee().JobId);
console.log(new Employee().employeeId);
```

1.  bq1uy 1BJKSJ bq1uy undefined
2.  bq1uy 1BJKSJ bq1uy
3.  bq1uy 1BJKSJ kj182
4.  undefined 1BJKSJ kj182

_Answer:_ 2) bq1uy 1BJKSJ bq1uy

### Q. What would be the output of following code?

```javascript
var employeeId = "aq123";
(function Employee() {
  try {
    throw "foo123";
  } catch (employeeId) {
    console.log(employeeId);
  }
  console.log(employeeId);
})();
```

1.  foo123 aq123
2.  foo123 foo123
3.  aq123 aq123
4.  foo123 undefined

_Answer:_ 1) foo123 aq123

---

### Q. What would be the output of following code?

```javascript
(function () {
  var greet = "Hello World";
  var toGreet = [].filter.call(greet, function (element, index) {
    return index > 5;
  });
  console.log(toGreet);
})();
```

1.  Hello World
2.  undefined
3.  World
4.  [ 'W', 'o', 'r', 'l', 'd' ]

_Answer:_ 4) [ 'W', 'o', 'r', 'l', 'd' ]

### Q. What would be the output of following code?

```javascript
(function () {
  var fooAccount = {
    name: "John",
    amount: 4000,
    deductAmount: function (amount) {
      this.amount -= amount;
      return "Total amount left in account: " + this.amount;
    },
  };
  var barAccount = {
    name: "John",
    amount: 6000,
  };
  var withdrawAmountBy = function (totalAmount) {
    return fooAccount.deductAmount.bind(barAccount, totalAmount);
  };
  console.log(withdrawAmountBy(400)());
  console.log(withdrawAmountBy(300)());
})();
```

1. Total amount left in account: 5600 Total amount left in account: 5300
2. undefined undefined
3. Total amount left in account: 3600 Total amount left in account: 3300
4. Total amount left in account: 5600 Total amount left in account: 5600

_Answer:_ 1) Total amount left in account: 5600 Total amount left in account: 5300

---

### Q. What would be the output of following code?

```javascript
(function () {
  var fooAccount = {
    name: "John",
    amount: 4000,
    deductAmount: function (amount) {
      this.amount -= amount;
      return this.amount;
    },
  };
  var barAccount = {
    name: "John",
    amount: 6000,
  };
  var withdrawAmountBy = function (totalAmount) {
    return fooAccount.deductAmount.apply(barAccount, [totalAmount]);
  };
  console.log(withdrawAmountBy(400));
  console.log(withdrawAmountBy(300));
  console.log(withdrawAmountBy(200));
})();
```

1. 5600 5300 5100
2. 3600 3300 3100
3. 5600 3300 5100
4. undefined undefined undefined

_Answer:_ 1) 5600 5300 5100

---

### Q. What would be the output of following code?

```javascript
(function () {
  var fooAccount = {
    name: "John",
    amount: 6000,
    deductAmount: function (amount) {
      this.amount -= amount;
      return this.amount;
    },
  };
  var barAccount = {
    name: "John",
    amount: 4000,
  };
  var withdrawAmountBy = function (totalAmount) {
    return fooAccount.deductAmount.call(barAccount, totalAmount);
  };
  console.log(withdrawAmountBy(400));
  console.log(withdrawAmountBy(300));
  console.log(withdrawAmountBy(200));
})();
```

1. 5600 5300 5100
2. 3600 3300 3100
3. 5600 3300 5100
4. undefined undefined undefined

_Answer:_ 2) 3600 3300 3100

---

### Q. What would be the output of following code?

```javascript
(function greetNewCustomer() {
  console.log("Hello " + this.name);
}.bind({
  name: "John",
})());
```

1. Hello John
2. Reference Error
3. Window
4. undefined

_Answer:_ 1) Hello John

### Q. What would be the output of following code ?

```javascript
function getDataFromServer(apiUrl) {
  var name = "John";
  return {
    then: function (fn) {
      fn(name);
    },
  };
}

getDataFromServer("www.google.com").then(function (name) {
  console.log(name);
});
```

1. John
2. undefined
3. Reference Error
4. fn is not defined

_Answer:_ 1) John

---

### Q. What would be the output of following code?

```javascript
(function () {
  var arrayNumb = [2, 8, 15, 16, 23, 42];
  Array.prototype.sort = function (a, b) {
    return a - b;
  };
  arrayNumb.sort();
  console.log(arrayNumb);
})();

(function () {
  var numberArray = [2, 8, 15, 16, 23, 42];
  numberArray.sort(function (a, b) {
    if (a == b) {
      return 0;
    } else {
      return a < b ? -1 : 1;
    }
  });
  console.log(numberArray);
})();

(function () {
  var numberArray = [2, 8, 15, 16, 23, 42];
  numberArray.sort(function (a, b) {
    return a - b;
  });
  console.log(numberArray);
})();
```

1. [ 2, 8, 15, 16, 23, 42 ]
   [ 2, 8, 15, 16, 23, 42 ]
   [ 2, 8, 15, 16, 23, 42 ]
2. undefined undefined undefined
3. [42, 23, 16, 15, 8, 2]
   [42, 23, 16, 15, 8, 2]
   [42, 23, 16, 15, 8, 2]
4. Reference Error

_Answer:_ 1) [ 2, 8, 15, 16, 23, 42 ]
[ 2, 8, 15, 16, 23, 42 ]
[ 2, 8, 15, 16, 23, 42 ]

---

### Q. What would be the output of following code?

```javascript
(function () {
  function sayHello() {
    var name = "Hi John";
    return;
    {
      fullName: name;
    }
  }
  console.log(sayHello().fullName);
})();
```

1. Hi John
2. undefined
3. Reference Error
4. Uncaught TypeError: Cannot read property 'fullName' of undefined

_Answer:_ 4) Uncaught TypeError: Cannot read property 'fullName' of undefined

### Q. What would be the output of following code?

```javascript
function getNumber() {
  return 2, 4, 5;
}

var numb = getNumber();
console.log(numb);
```

1. 5
2. undefined
3. 2
4. (2,4,5)

_Answer:_ 1) 5

---

### Q. What would be the output of following code?

```javascript
function getNumber() {
  return;
}

var numb = getNumber();
console.log(numb);
```

1. null
2. undefined
3. ""
4. 0

_Answer:_ 2) undefined

### Q. What would be the output of following code?

```javascript
function mul(x) {
  return function (y) {
    return [
      x * y,
      function (z) {
        return x * y + z;
      },
    ];
  };
}

console.log(mul(2)(3)[0]);
console.log(mul(2)(3)[1](4));
```

1. 6, 10
2. undefined undefined
3. Reference Error
4. 10, 6

_Answer:_ 1) 6, 10

---

### Q. What would be the output of following code?

```javascript
function mul(x) {
  return function (y) {
    return {
      result: x * y,
      sum: function (z) {
        return x * y + z;
      },
    };
  };
}
console.log(mul(2)(3).result);
console.log(mul(2)(3).sum(4));
```

1. 6, 10
2. undefined undefined
3. Reference Error
4. 10, 6

_Answer:_ 1) 6, 10

### Q. What would be the output of following code?

```javascript
function mul(x) {
  return function (y) {
    return function (z) {
      return function (w) {
        return function (p) {
          return x * y * z * w * p;
        };
      };
    };
  };
}
console.log(mul(2)(3)(4)(5)(6));
```

1. 720
2. undefined
3. Reference Error
4. Type Error

_Answer:_ 1) 720

---

### Q. What is the value of `foo`?

```javascript
var foo = 10 + "20";
```

_Answer:_ `'1020'`, because of type coercion from Number to String

### Q. How would you make this work?

```javascript
add(2, 5); // 7
add(2)(5); // 7
```

_Answer:_ A general solution for any number of parameters

```javascript
"use strict";

let sum = (arr) => arr.reduce((a, b) => a + b);
let addGenerator = (numArgs, prevArgs) => {
  return function () {
    let totalArgs = prevArgs.concat(Array.from(arguments));
    if (totalArgs.length === numArgs) {
      return sum(totalArgs);
    }
    return addGenerator(numArgs, totalArgs);
  };
};

let add = addGenerator(2, []);

add(2, 5); // 7
add(2)(5); // 7
add()(2, 5); // 7
add()(2)(5); // 7
add()()(2)(5); // 7
```

---

### Q. What value is returned from the following statement?

```javascript
"i'm a lasagna hog".split("").reverse().join("");
```

_Answer:_ It's actually a reverse method for a string - `'goh angasal a m\'i'`

### Q. What is the value of `window.foo`?

```javascript
window.foo || (window.foo = "bar");
```

_Answer:_ Always `'bar'`

### Q. What is the outcome of the two alerts below?

```javascript
var foo = "Hello";
(function () {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
```

_Answer:_

- First: `Hello World`
- Second: Throws an exception, `ReferenceError: bar is not defined`

---

### Q. What is the value of `foo.length`?

```javascript
var foo = [];
foo.push(1);
foo.push(2);
```

_Answer:_ `.push` is mutable - `2`

### Q. What is the value of `foo.x`?

```javascript
var foo = { n: 1 };
var bar = foo;
foo.x = foo = { n: 2 };
```

_Answer:_ `undefined`. Rather, `bar.x` is `{n: 2}`.

`foo.x = foo = {n: 2}` is the same as `foo.x = (foo = {n: 2})`. It is because
a left term is first referenced and then a right term is evaluated when an
assignment is performed in JavaScript. When `foo.x` is referenced, it refers
to an original object, `{n: 1}`. So, when the result of the right term, `{n: 2}`, is evaluated, it will assigned to the original object, which is at the
moment referenced by `bar`.

---

### Q. What does the following code print?\*

```javascript
console.log("one");
setTimeout(function () {
  console.log("two");
}, 0);
console.log("three");
```

_Answer:_ `one`, `three` and `two`. It's because `console.log('two');` will be
invoked in the next event loop.

### Q. What would be the result of 1+2+'3'?

The output is going to be `33`. Since `1` and `2` are numeric values, the result of first two digits is going to be a numeric value `3`. The next digit is a string type value because of that the addition of numeric value `3` and string type value `3` is just going to be a concatenation value `33`.

### Q. Write a script that returns the number of occurrences of character given a string as input?

```javascript
function countCharacters(str) {
  return str
    .replace(/ /g, "")
    .toLowerCase()
    .split("")
    .reduce((arr, character) => {
      if (character in arr) {
        arr[character]++;
      } else {
        arr[character] = 1;
      }
      return arr;
    }, {});
}
console.log(countCharacters("the brown fox jumps over the lazy dog"));
```

---

### Q. What is the value of `foo`?

```javascript
var foo = 10 + "20";
```

_Answer:_ `'1020'`, because of type coercion from Number to String

### Q. How would you make this work?

```javascript
add(2, 5); // 7
add(2)(5); // 7
```

_Answer:_ A general solution for any number of parameters

```js
"use strict";

let sum = (arr) => arr.reduce((a, b) => a + b);
let addGenerator = (numArgs, prevArgs) => {
  return function () {
    let totalArgs = prevArgs.concat(Array.from(arguments));
    if (totalArgs.length === numArgs) {
      return sum(totalArgs);
    }
    return addGenerator(numArgs, totalArgs);
  };
};

let add = addGenerator(2, []);

add(2, 5); // 7
add(2)(5); // 7
add()(2, 5); // 7
add()(2)(5); // 7
add()()(2)(5); // 7
```

---

### Q. What value is returned from the following statement?

```javascript
"i'm a lasagna hog".split("").reverse().join("");
```

_Answer:_ It's actually a reverse method for a string - `'goh angasal a m\'i'`

### Q. What is the value of `window.foo`?

```javascript
window.foo || (window.foo = "bar");
```

_Answer:_ Always `'bar'`

### Q. What is the outcome of the two alerts below?

```javascript
var foo = "Hello";
(function () {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
```

_Answer:_

- First: `Hello World`
- Second: Throws an exception, `ReferenceError: bar is not defined`

### Q. What is the value of `foo.length`?

```javascript
var foo = [];
foo.push(1);
foo.push(2);
```

_Answer:_ `.push` is mutable - `2`

---

### Q. What is the value of `foo.x`?

```javascript
var foo = { n: 1 };
var bar = foo;
foo.x = foo = { n: 2 };
```

_Answer:_ `undefined`. Rather, `bar.x` is `{n: 2}`.

`foo.x = foo = {n: 2}` is the same as `foo.x = (foo = {n: 2})`. It is because
a left term is first referenced and then a right term is evaluated when an
assignment is performed in JavaScript. When `foo.x` is referenced, it refers
to an original object, `{n: 1}`. So, when the result of the right term, `{n: 2}`, is evaluated, it will assigned to the original object, which is at the
moment referenced by `bar`.

---

### Q. What does the following code print?

```javascript
console.log("one");
setTimeout(function () {
  console.log("two");
}, 0);
console.log("three");
```

_Answer:_ `one`, `three` and `two`. It's because `console.log('two');` will be
invoked in the next event loop.

### Q. For which value of x the results of the following statements are not the same?

```javascript
//  if( x <= 100 ) {...}
if( !(x > 100) ) {...}
```

_Answer:_ `NaN <= 100` is `false` and `NaN > 100` is also false, so if the value of `x` is `NaN`, the statements are not the same.

The same holds true for any value of x that being converted to Number, returns NaN, e.g.: `undefined`, `[1,2,5]`, `{a:22}`, etc.

### Q. What is g value?

```javascript
f = g = 0;
(function () {
  try {
    f =
      function () {
        return f();
      } && f();
  } catch (e) {
    return g++ && f();
  } finally {
    return ++g;
  }
  function f() {
    g += 5;
    return 0;
  }
})();
```

---

### Q. What will be the output?

```javascript
function b(b) {
  return this.b && b(b);
}
b(b.bind(b));
```

### Q. What will be the output?

```javascript
c = (c) => {
  return this.c && c(c);
};
c(c.bind(c));
```

### Q. Predict the output of the following JavaScript code?

```javascript
var g = 0;
g = 1 && g++;
console.log(g);
```

### Q. Predict the output of the following JavaScript code?

```javascript
!function(){}()
function(){}()
true && function(){}()
(function(){})()
function(){}
!function(){}
```

### Q. What will expression return?

```javascript
var a = (b = true),
  c = (a) => a;
(function a(a = (c(b).a = c = () => a)) {
  return a();
})();
```

### Q. Predict the output of the following JavaScript code?

```javascript
var a = true;
(a = function () {
  return a;
})();
```

### Q. What will be the output?

```javascript
var v = 0;
try {
  throw (v = (function (c) {
    throw (v = function (a) {
      return v;
    });
  })());
} catch (e) {
  console.log(e()());
}
```

---

### Q. What will the following code output?

```javascript
const arr = [10, 12, 15, 21];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function () {
    console.log("Index: " + i + ", element: " + arr[i]);
  }, 3000);
}
```

### Q. What will be the output of the following code?

```javascript
var output = (function (x) {
  delete x;
  return x;
})(0);

console.log(output);
```

### Q. What will be the output of the following code?

```javascript
var Employee = {
  company: "xyz",
};
var emp1 = Object.create(Employee);
delete emp1.company;
console.log(emp1.company);
```

---

### Q. Make this work:

```javascript
duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
```

```javascript
function duplicate(arr) {
  return arr.concat(arr);
}

duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
```

---

### Q. Fix the bug using ES5 only

```javascript
var arr = [10, 32, 65, 2];
for (var i = 0; i < arr.length; i++) {
  setTimeout(function () {
    console.log("The index of this number is: " + i);
  }, 3000);
}
```

For ES6, you can just replace `var i` with `let i`.

For ES5, you need to create a function scope like here:

```javascript
var arr = [10, 32, 65, 2];
for (var i = 0; i < arr.length; i++) {
  setTimeout(
    (function (j) {
      return function () {
        console.log("The index of this number is: " + j);
      };
    })(i),
    3000
  );
}
```

---

### Q. What will be the output of the following code?

```javascript
console.log(eval("10 + 10")); // 20

console.log(eval("5 + 5" + 10)); // 515

console.log(eval("5 + 5 + 5" + 10)); // 520

console.log(eval(10 + "5 + 5")); // 110

console.log(eval(10 + "5 + 5 + 5")); // 115
```

### Q. What will be the output of the following code?

```javascript
var x = 10;
var y = 20;
var a = eval("x * y") + "<br>";
var b = eval("2 + 2") + "<br>";
var c = eval("x + 30") + "<br>";

let result = a + b + c;
console.log(result); // 200<br>4<br>40<br>
```

---

### Q. What will be the output of the following code?

```javascript
// Example 01:
var prices = [12, 20, 18];
var newPriceArray = [...prices];
console.log(newPriceArray);

// Example 02:
var alphabets = ["A", ..."BCD", "E"];
console.log(alphabets);

// Example 03:
var prices = [12, 20, 18];
var maxPrice = Math.max(...prices);
console.log(maxPrice);

// Example 04:
var max = Math.max(..."43210");
console.log(max);

// Example 05:
const fruits = ["apple", "orange"];
const vegetables = ["carrot", "potato"];

const result = ["bread", ...vegetables, "chicken", ...fruits];
console.log(result);

// Example 06:
const country = "USA";
console.log([...country]);
```

---

### Q. Given and object and property path. Get value from property path

```javascript
function getPropertyValue(TEMP_OBJECT, path) {
  return path.split('.').reduce((prev, key) => {
      return prev ? prev[key] : undefined;
    }, TEMP_OBJECT)
}

//Input :
let srcObject = {
    'system' : {
        'database' : {
              '0' : {
                'host' : '54.232.122',
                'port' : 3306
             },
              '1' : {
                'host' : '54.232.123',
             },
             'port' : 3307
              '2' : {
                'host' : '54.232.123',
             }
       }
   }
},
path = "system.database.1.port";

//Output: 3307
```

---

### Q. How to filter object from Arrays of Objects

```javascript
let filteredArray = [{name: 'john'},{name: 'kelly'}].filter(value => value.name === 'kelly');

Filter method return Array of objects
```

### Q. How to replace all the occurrences of string

```javascript
str = str.replace(/test/g, "");
```

---

### Q. write a script that returns the number of occurrences of character given a string as input

```javascript
function countCharacters(str) {
  return str
    .replace(/ /g, "")
    .toLowerCase()
    .split("")
    .reduce((p, c) => {
      if (c in p) {
        p[c]++;
      } else {
        p[c] = 1;
      }
      return p;
    }, {});
}
console.log(countCharacters("the brown fox jumps over the lazy dog"));
```

---

### Q. write a script that return the number of occurrences of a character in paragraph

```javascript
function charCount(str, searchChar) {
  let count = 0;
  if (str) {
    let stripStr = str.replace(/ /g, "").toLowerCase(); //remove spaces and covert to lowercase
    for (let chr of stripStr) {
      if (chr === searchChar) {
        count++;
      }
    }
  }
  return count;
}
console.log(charCount("the brown fox jumps over the lazy dog", "o"));
```

---

### Q. Recursive and non-recursive Factorial function

```javascript
function recursiveFactorial(n) {
  if (n < 1) {
    throw Error("Value of N has to be greater then 1");
  }
  if (n === 1) {
    return 1;
  } else {
    return n * recursiveFactorial(n - 1);
  }
}

console.log(recursiveFactorial(5));

function factorial(n) {
  if (n < 1) {
    throw Error("Value of N has to be greater then 1");
  }
  if (n === 1) {
    return 1;
  }
  let result = 1;
  for (let i = 1; i <= n; i++) {
    result = result * i;
  }
  return result;
}

console.log(factorial(5));
```

---

### Q. Recursive and non recursive fibonacci-sequence

```javascript
// 1, 1, 2, 3, 5, 8, 13, 21, 34

function recursiveFibonacci(num) {
  if (num <= 1) {
    return 1;
  } else {
    return recursiveFibonacci(num - 1) + recursiveFibonacci(num - 2);
  }
}

console.log(recursiveFibonacci(8));

function fibonnaci(num) {
  let a = 1,
    b = 0,
    temp;
  while (num >= 0) {
    temp = a;
    a = a + b;
    b = temp;
    num--;
  }
  return b;
}

console.log(fibonnaci(7));

// Memoization fibonnaci

function fibonnaci(num, memo = {}) {
  if (num in memo) {
    return memo[num];
  }
  if (num <= 1) {
    return 1;
  }
  return (memo[num] = fibonnaci(num - 1, memo) + fibonnaci(num - 2, memo));
}

console.log(fibonnaci(5)); // 8
```

### Q. Random Number between min and max

```javascript
// 5 to 7
let min = 5;
let max = 7;
console.log(min + Math.floor(Math.random() * (max - min + 1)));
```

---

### Q. Get HTML form values as JSON object

```javascript
// Use the array reduce function with form elements.
const formToJSON = (elements) =>
  [].reduce.call(
    elements,
    (data, element) => {
      data[element.name] = element.value;
      // Check if name and value exist on element
      // Check if it checkbox or radio button which can select multiple or single
      //check for multiple select options
      return data;
    },
    {}
  );

// pass the elements to above method, to get values
document.querySelector("HTML_FORM_CLASS").elements;
```

---

### Q. Reverse the number

```javascript
function reverse(num) {
  let result = 0;
  while (num != 0) {
    result = result * 10;
    result = result + (num % 10);
    num = Math.floor(num / 10);
  }
  return result;
}

console.log(reverse(12345));
```

---

### Q. Remove Duplicate elements from Array

```javascript
var arr = [1, 2, 3, 5, 1, 5, 9, 1, 2, 8];
function removeDuplicate() {
  return ar.reduce((prev, current) => {
    //Cannot use includes of array, since it is not supported by many browser
    if (prev.indexOf(current) === -1) {
      prev.push(current);
    }
    return prev;
  }, []);
}
console.log(removeDuplicate(ar));

const removeDuplicates = (arr) => {
  let holder = {};
  return arr.filter((el) => {
    if (!holder[el]) {
      holder[el] = true;
      return true;
    }
    return false;
  });
};
const arr = [1, 2, 3, 5, 1, 5, 9, 1, 2, 8];
console.log(removeDuplicates(arr)); // ["1", "2", "3", "5", "8", "9"] // O(n)

// Es6
console.log([...new Set(arr)]);
```

---

### Q. Deep copy of object or clone of object

```javascript
function deepExtend(out = {}) {
  for (let i = 1; i < arguments.length; i++) {
    let obj = arguments[i];
    if (obj == null)
      // skip undefined and null [check with double equal not triple]
      continue;

    obj = Object(obj);

    for (let key in obj) {
      // avoid shadow hasownproperty of parent
      if (Object.prototype.hasOwnProperty.call(obj, key)) {
        if (
          typeof obj[key] === "object" &&
          !Array.isArray(obj[key]) &&
          obj[key] != null
        )
          out[key] = deepExtend(out[key], obj[key]);
        else out[key] = obj[key];
      }
    }
  }
  return out;
}

//Alternative if there are no function
let cloneObj = JSON.parse(JSON.stringify(obj));

console.log(deepExtend({}, { a: 1, b: { c: 2, d: 3 } }, { e: 4, b: { f: 1 } }));
//output : { a: 1, b: {c: 2, d: 3, f: 1}, e: 4 }
```

---

### Q. Sort ticket based on flying order.

```javascript
"use strict";

function SortTickets(tickets) {
  this.tickets = tickets;

  // reverse the order of tickets
  this.reverseTickets = {};
  for (let key in this.tickets) {
    this.reverseTickets[tickets[key]] = key;
  }

  // Get the starting point of ticket
  let orderedTivckets = [...this.getStartingPoint()];

  // Get the ticket destination.
  let currentValue = orderedTickets[orderedTickets.length - 1];
  while (currentValue) {
    currentValue = this.tickets[currentValue];
    if (currentValue) {
      orderedTickets.push(currentValue);
    }
  }
  console.log(orderedTickets);
}

SortTickets.prototype.getStartingPoint = function () {
  for (let tick in this.tickets) {
    if (!(tick in this.reverseTickets)) {
      return [tick, this.tickets[tick]];
    }
  }
  return null;
};

new SortTickets({
  Athens: "Rio",
  Barcelona: "Athens",
  London: "NYC",
  ND: "Lahore",
  NYC: "Barcelona",
  Rio: "ND",
});
```

---

### Q. Cuncurrent execute function based on input number

```javascript
function concurrent(num) {
  this.queue = [];
  this.num = num;
}

concurrent.prototype.enqueue = function (value) {
  this.queue.push(value);
};

concurrent.prototype.start = function () {
  this.runningCount = 0;
  while (this.queue.length > 0) {
    if (this.runningCount < this.num) {
      this.queue.pop().call(this, () => {
        this.runningCount--;
        let count = this.runningCount;
        if (count === 0) {
          this.start();
        }
      });
      this.runningCount++;
    }
  }
};

let callback = (done) => {
  console.log("starting");
  setTimeout(() => {
    console.log("stopped");
    done();
  }, 200);
};

let c = new concurrent(2);
c.enqueue(callback);
c.enqueue(callback);
c.enqueue(callback);
c.enqueue(callback);
c.enqueue(callback);
c.enqueue(callback);
c.start();
```

---

### Q. Reversing an array

```javascript
let a = [1, 2, 3, 4, 5];

//Approach 1:
console.log(a.reverse());

//Approach 2:
let reverse = a.reduce((prev, current) => {
  prev.unshift(current);
  return prev;
}, []);

console.log(reverse);
```

### Q. Rotate 2D array

```javascript
const transpose = (arr) => arr[0].map((col, i) => arr.map((row) => row[i]));

console.log(
  transpose([
    [1, 2, 3, 4],
    [5, 6, 7, 8],
    [9, 10, 11, 12],
  ])
);
```

### Q. Get Column from 2D Array

```javascript
const getColumn = (arr, n) => arr.map((x) => x[n]);

const twoDimensionalArray = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9],
];

console.log(getColumn(twoDimensionalArray, 1)); //Result = [2,5,8]
```

### Q. Get top N from array

```javascript
function topN(arr, num) {
  let sorted = arr.sort((a, b) => a - b);
  return sorted.slice(sorted.length - num, sorted.length);
}

console.log(topN([1, 8, 3, 4, 5], 2)); // [5,8]
```

---

### Q. Get query params from Object

```javascript
function getQueryParams(obj) {
  let parms = "";
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      if (parms.length > 0) {
        parms += "&";
      }
      parms += encodeURI(`${key}=${obj[key]}`);
    }
  }
  return parms;
}

console.log(
  getQueryParams({
    name: "Umesh",
    tel: "48289",
    add: "3333 emearld st",
  })
);
```

---

### Q. Consecutive 1's in binary

```javascript
function consecutiveOne(num) {
  let binaryArray = num.toString(2);

  let maxOccurence = 0,
    occurence = 0;
  for (let val of binaryArray) {
    if (val === "1") {
      occurence += 1;
      maxOccurence = Math.max(maxOccurence, occurence);
    } else {
      occurence = 0;
    }
  }
  return maxOccurence;
}
//13 = 1101 = 2
//5 = 101 = 1
console.log(consecutiveOne(5)); //1
```

---

### Q. Spiral travesal of matrix

```javascript
var input = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12],
  [13, 14, 15, 16],
];

var spiralTraversal = function (matriks) {
  let result = [];
  var goAround = function (matrix) {
    if (matrix.length === 0) {
      return;
    }

    // right
    result = result.concat(matrix.shift());

    // down
    for (var j = 0; j < matrix.length - 1; j++) {
      result.push(matrix[j].pop());
    }

    // bottom
    result = result.concat(matrix.pop().reverse());

    // up
    for (var k = matrix.length - 1; k > 0; k--) {
      result.push(matrix[k].shift());
    }

    return goAround(matrix);
  };

  goAround(matriks);

  return result;
};
console.log(spiralTraversal(input)); // [1, 2, 3, 4, 8, 12, 16, 15, 14, 13, 9, 5, 6, 7, 11, 10]
```

---

### Q. Merge Sorted array and sort it.

```javascript
function mergeSortedArray(arr1, arr2) {
  return [...new Set(arr1.concat(arr2))].sort((a, b) => a - b);
}

console.log(mergeSortedArray([1, 2, 3, 4, 5, 6], [0, 3, 4, 7])); // [0, 1, 2, 3, 4, 5, 6, 7]
```

---

### Q. Anagram of words

```javascript
const alphabetize = (word) => word.split("").sort().join("");

function groupAnagram(wordsArr) {
  return wordsArr.reduce((p, c) => {
    const sortedWord = alphabetize(c);
    if (sortedWord in p) {
      p[sortedWord].push(c);
    } else {
      p[sortedWord] = [c];
    }
    return p;
  }, {});
}

console.log(
  groupAnagram(["map", "art", "how", "rat", "tar", "who", "pam", "shoop"])
);
// result : {
//  amp: ["map", "pam"],
//  art: ["art", "rat", "tar"],
//  hoops: ["shoop"],
//  how: ["how", "who"]
// }
```

---

### Q. Print the largest (maximum) hourglass sum found in 2d array.

```javascript
// if arr 6 X 6 then iterate it till 4 X 4  [reduce by two]
// if arr 8 X 8 then iterate it till 6 X 6  [reduce by two]
function main(arr) {
  let maxScore = -999;
  let len = arr.length;
  for (let i = 0; i < len - 2; i++) {
    for (let j = 0; j < len - 2; j++) {
      let total =
        arr[i][j] +
        arr[i][j + 1] +
        arr[i][j + 2] +
        arr[i + 1][j + 1] +
        arr[i + 2][j] +
        arr[i + 2][j + 1] +
        arr[i + 2][j + 2];

      maxScore = Math.max(maxScore, total);
    }
  }
  console.log(maxScore);
}
```

---

### Q. Transform array of object to array

```javascript
let data = [
  { vid: "aaa", san: 12 },
  { vid: "aaa", san: 18 },
  { vid: "aaa", san: 2 },
  { vid: "bbb", san: 33 },
  { vid: "bbb", san: 44 },
  { vid: "aaa", san: 100 },
];

let newData = data.reduce((acc, item) => {
  acc[item.vid] = acc[item.vid] || { vid: item.vid, san: [] };
  acc[item.vid]["san"].push(item.san);
  return acc;
}, {});

console.log(Object.keys(newData).map((key) => newData[key]));

// Result
// [[object Object] {
//   san: [12, 18, 2, 100],
//   vid: "aaa"
// }, [object Object] {
//   san: [33, 44],
//   vid: "bbb"
// }]
```

---

### Q. Create a private variable or private method in object

```javascript
let obj = (function () {
  function getPrivateFunction() {
    console.log("this is private function");
  }
  let p = "You are accessing private variable";
  return {
    getPrivateProperty: () => {
      console.log(p);
    },
    callPrivateFunction: getPrivateFunction,
  };
})();

obj.getPrivateValue(); // You are accessing private variable
console.log("p" in obj); // false
obj.callPrivateFunction(); // this is private function
```

---

### Q. Flatten only Array not objects

```javascript
function flatten(arr, result = []) {
  arr.forEach((val) => {
    if (Array.isArray(val)) {
      flatten(val, result);
    } else {
      result.push(val);
    }
  });
  return result;
}

let input = [1, { a: [2, [3]] }, 4, [5, [6]], [[7, ["hi"]], 8, 9], 10];
console.log(flatten(input)); // [1, { a: [2, [3]]}, 4, 5, 6, 7, "hi", 8, 9, 10]

function flattenIterative(out) {
  // iteratively
  let result = out;
  while (result.some(Array.isArray)) {
    result = [].concat.apply([], result);
  }
  return result;
}
var list1 = [
  [0, 1],
  [2, 3],
  [4, 5],
];
console.log(flattenIterative(list1)); // [0, 1, 2, 3, 4, 5]

function flattenIterative1(current) {
  let result = [];
  while (current.length) {
    let firstValue = current.shift();
    if (Array.isArray(firstValue)) {
      current = firstValue.concat(current);
    } else {
      result.push(firstValue);
    }
  }
  return result;
}

let input = [1, { a: [2, [3]] }, 4, [5, [6]], [[7, ["hi"]], 8, 9], 10];
console.log(flattenIterative1(input));
var list2 = [0, [1, [2, [3, [4, [5]]]]]];
console.log(flattenIterative1(list2)); // [0, 1, 2, 3, 4, 5]
```

---

### Q. Find max difference between two number in Array

```javascript
function maxDifference(arr) {
  let maxDiff = 0;

  for (let i = 0; i < arr.length; i++) {
    for (let j = i + 1; j < arr.length; j++) {
      let diff = Math.abs(arr[i] - arr[j]);
      maxDiff = Math.max(maxDiff, diff);
    }
  }
  return maxDiff;
}

console.log(maxDifference([1, 2, 4])); // [1 - 4 ] = 3
```

### Q. swap two number in ES6 [destructing]

```javascript
let a = 10,
  b = 5;
[a, b] = [b, a];
```

---

### Q. Panagram ? it means all the 26 letters of alphabet are there

```javascript
function panagram(input) {
  if (input == null) {
    // Check for null and undefined
    return false;
  }

  if (input.length < 26) {
    // if length is less then 26 then it is not
    return false;
  }
  input = input.replace(/ /g, "").toLowerCase().split("");
  let obj = input.reduce((prev, current) => {
    if (!(current in prev)) {
      prev[current] = current;
    }
    return prev;
  }, {});
  console.log(Object.keys(obj).length === 26 ? "panagram" : "not pangram");
}
processData("We promptly judged antique ivory buckles for the next prize"); // pangram
processData("We promptly judged antique ivory buckles for the prize"); // Not Pangram
```

---

### Q. Given two identical DOM trees (not the same one), and a node from one of them find the node in the other one.

```javascript
function indexOf(arrLike, target) {
  return Array.prototype.indexOf.call(arrLike, target);
}

// Given a node and a tree, extract the nodes path
function getPath(root, target) {
  var current = target;
  var path = [];
  while (current !== root) {
    let parentNode = current.parentNode;
    path.unshift(indexOf(parentNode.childNodes, current));
    current = parentNode;
  }
  return path;
}

// Given a tree and a path, let's locate a node
function locateNodeFromPath(node, path) {
  return path.reduce((root, index) => root.childNodes[index], node);
}

const rootA = document.querySelector("#root-a");
const rootB = document.querySelector("#root-b");
const target = rootA.querySelector(".person__age");

console.log(locateNodeFromPath(rootB, getPath(rootA, target)));
```

---

### Q. Convert a number into a Roman Numeral

```javascript
function romanize(num) {
  let lookup = {
      M: 1000,
      CM: 900,
      D: 500,
      CD: 400,
      C: 100,
      XC: 90,
      L: 50,
      XL: 40,
      X: 10,
      IX: 9,
      V: 5,
      IV: 4,
      I: 1,
    },
    roman = "";
  for (let i in lookup) {
    while (num >= lookup[i]) {
      roman += i;
      num -= lookup[i];
    }
  }
  return roman;
}

console.log(romanize(3)); // III
```

---

### Q. check if parenthesis is malformed or not

```javascript
function matchParenthesis(str) {
  let obj = { "{": "}", "(": ")", "[": "]" };
  let result = [];
  for (let s of str) {
    if (s === "{" || s === "(" || s === "[") {
      // All opening brackets
      result.push(s);
    } else {
      if (result.length > 0) {
        let lastValue = result.pop(); //pop the last value and compare with key
        if (obj[lastValue] !== s) {
          // if it is not same then it is not formated properly
          return false;
        }
      } else {
        return false; // empty array, there is nothing to pop. so it is not formated properly
      }
    }
  }
  return result.length === 0;
}

console.log(matchParenthesis("}{{}}"), matchParenthesis("{{[]}}")); // false - true
```

---

### Q. Create Custom Event Emitter class

```javascript
class EventEmitter {
  constructor() {
    this.holder = {};
  }

  on(eventName, fn) {
    if (eventName && typeof fn === "function") {
      this.holder[eventName] = this.holder[eventName] || [];
      this.holder[eventName].push(fn);
    }
  }

  emit(eventName, ...args) {
    let eventColl = this.holder[eventName];
    if (eventColl) {
      eventColl.forEach((callback) => callback(args));
    }
  }
}

let e = new EventEmitter();
e.on("callme", function (args) {
  console.log(`you called me ${args}`);
});
e.on("callme", function (args) {
  console.log(`testing`);
});

e.emit("callme", ["a", "b"], { firstName: "umesh", lastName: "gohil" });
```

---

### Q. Max value from an array

```javascript
const arr = [-2, -3, 4, 3, 2, 1];
Math.max(...arr); // Fastest

Math.max.apply(Math, arr); // Slow
```

---

### Q. DOM methods

```javascript
https://github.com/nefe/You-Dont-Need-jQuery

var el = document.querySelector('div');
el.childNodes;   // get the list of child nodes of el
el.firstChild;   // get the first child node of el
el.lastChild;    // get the last child node of el
el.parentNode;   // get the parent node of el
el.previousSibling;    // get the previous sibling of el
el.nextSibling;  // get the next sibling of el
el.textContent;  // get the text content of el
el.innerHTML;    // get the inner html of el

document.createElement('div')  // create dom element
document.creatTextNode('Hello world');  // create text node
document.createDocumentFragment();

el.appendChild(); //append child to el;
el.insertBefore(); // insert child before el;
el.parentNode.replaceChild(NEW_NODE, REPLACE_ME)  // replace the node
el.removechild();  // remove the child node

Array.from(NODES) // convert nodelist to regular array

el.classList[contains | add | remove | replace]  // class of el

el.dataset.<camelCaseName> // data-count is dataset.count, data-index-number is dataset.indexNumber

el.setAttribute | el.getAttribute | el.removeAttribute // attributes of el

el.style    // get the style of el
```

---

### Q. search function called after 500 ms

```javascript
<input type="text" class="search" />;

let timer = null;
function searchOptions(value) {
  clearTimeout(timer);
  timer = setTimeout(() => {
    console.log(`value is - ${value}`);
  }, 500);
}

let search = document.querySelector(".search");
search.addEventListener("keyup", function () {
  searchOptions(this.value);
});
```

---

### Q. Move all zero's to end

```javascript
const moveZeroToEnd = (arr) => {
  for (let i = 0, j = 0; j < arr.length; j++) {
    if (arr[j] !== 0) {
      if (i < j) {
        [arr[i], arr[j]] = [arr[j], arr[i]]; // swap i and j
      }
      i++;
    }
  }
  return arr;
};

console.log(moveZeroToEnd([1, 8, 2, 0, 0, 0, 3, 4, 0, 5, 0])); // [1, 8, 2, 3, 4, 5, 0, 0, 0, 0, 0]
```

---

### Q. Decode message in matrix [diagional down right, diagional up right]

```javascript
const decodeMessage = (mat) => {
  // check if matrix is null or empty
  if (mat == null || mat.length === 0) {
    return "";
  }
  let x = mat.length - 1;
  let y = mat[0].length - 1;
  let message = "";
  let decode = (mat, i = 0, j = 0, direction = "DOWN") => {
    message += mat[i][j];

    if (i === x) {
      direction = "UP";
    }

    if (direction === "DOWN") {
      i++;
    } else {
      i--;
    }

    if (j === y) {
      return;
    }

    j++;
    decode(mat, i, j, direction);
  };
  decode(mat);
  return message;
};

let mat = [
  ["I", "B", "C", "A", "L", "K", "A"],
  ["D", "R", "F", "C", "A", "E", "A"],
  ["G", "H", "O", "E", "L", "A", "D"],
  ["G", "H", "O", "E", "L", "A", "D"],
];

console.log(decodeMessage(mat)); //IROELEA
```

---

### Q. find a pair in array, whose sum is equal to given number.

```javascript
const hasPairSum = (arr, sum) => {
  if (arr == null && arr.length < 2) {
    return false;
  }

  let left = 0;
  let right = arr.length - 1;
  let result = false;

  while (left < right && !result) {
    let pairSum = arr[left] + arr[right];
    if (pairSum < sum) {
      left++;
    } else if (pairSum > sum) {
      right--;
    } else {
      result = true;
    }
  }
  return result;
};

console.log(hasPairSum([1, 2, 4, 5], 8)); // null
console.log(hasPairSum([1, 2, 4, 4], 8)); // [2,3]

const hasPairSum = (arr, sum) => {
  let difference = {};
  let hasPair = false;
  arr.forEach((item) => {
    let diff = sum - item;
    if (!difference[diff]) {
      difference[item] = true;
    } else {
      hasPair = true;
    }
  });
  return hasPair;
};
console.log(hasPairSum([6, 4, 3, 8], 8));

// NOTE: if array is not sorted then subtract the value with sum and store in difference
// then see if that value exist in difference then return true.
```

---

### Q. Binary Search [Array should be sorted]

```javascript
function binarySearch(arr, val) {
  let startIndex = 0,
    stopIndex = arr.length - 1,
    middleIndex = Math.floor((startIndex + stopIndex) / 2);

  while (arr[middleIndex] !== val && startIndex < stopIndex) {
    if (val < arr[middleIndex]) {
      stopIndex = middleIndex - 1;
    } else if (val > arr[middleIndex]) {
      startIndex = middleIndex + 1;
    }
    middleIndex = Math.floor((startIndex + stopIndex) / 2);
  }

  return arr[middleIndex] === val ? middleIndex : -1;
}

console.log(binarySearch([-1, 10, 22, 35, 48, 56, 67], 22));
console.log(binarySearch([-1, 10, 22, 35, 48, 56, 67], 27));
```

---

### Q. Pascal triangle.

```javascript
function pascalTriangle(n) {
  let last = [1],
    triangle = [last];
  for (let i = 0; i < n; i++) {
    const ls = [0].concat(last), //[0,1]           // [0,1,1]
      rs = last.concat([0]); //[1,0]           // [1,1,0]
    last = rs.map((r, i) => ls[i] + r); //[1, 1]          // [1,2,1]
    triangle = triangle.concat([last]); // [[1], [1,1]]   // [1], [1, 1], [1, 2, 1]
  }
  return triangle;
}

console.log(pascalTriangle(2));
```

---

### Q. Explain the code below. How many times the createVal function is called?

```javascript
function createVal() {
  return Math.random();
}

function fun(val = createVal()) {
  console.log(val);
}

fun();
fun(5);
```

`createVal()` function will execute only once.

Output

```
0.2162050091554224
VM298:6 5
```

---

### Q. What is the output?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = "Jhone";
  let age = 21;
}

sayHi();
```

- A: `Jhone` and `undefined`
- B: `Jhone` and `ReferenceError`
- C: `ReferenceError` and `21`
- D: `undefined` and `ReferenceError`

**Answer: D**

<details><summary><b>Explanation</b></summary>
<p>
Within the function, we first declare the `name` variable with the `var` keyword. This means that the variable gets hoisted (memory space is set up during the creation phase) with the default value of `undefined`, until we actually get to the line where we define the variable. We haven't defined the variable yet on the line where we try to log the `name` variable, so it still holds the value of `undefined`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get <i>initialized</i>. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a `ReferenceError`.

</p>
</details>

---


### Q. What is the output?

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` and `0 1 2`
- B: `0 1 2` and `3 3 3`
- C: `3 3 3` and `0 1 2`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>
Because of the event queue in JavaScript, the `setTimeout` callback function is called _after_ the loop has been executed. Since the variable `i` in the first loop was declared using the `var` keyword, this value was global. During the loop, we incremented the value of `i` by `1` each time, using the unary operator `++`. By the time the `setTimeout` callback function was invoked, `i` was equal to `3` in the first example.

In the second loop, the variable `i` was declared using the `let` keyword: variables declared with the `let` (and `const`) keyword are block-scoped (a block is anything between `{ }`). During each iteration, `i` will have a new value, and each value is scoped inside the loop.
</p>
</details>

---

### Q. What is the output?

```javascript
+true;
!"Jhone";
```

- A: `1` and `false`
- B: `false` and `NaN`
- C: `false` and `false`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
The unary plus tries to convert an operand to a number. `true` is `1`, and `false` is `0`.

The string `'Jhone'` is a truthy value. What we're actually asking, is "is this truthy value falsy?". This returns `false`.
</p>
</details>

---

### Q. Which one is true?

```javascript
const bird = {
  size: "small",
};

const mouse = {
  name: "Mickey",
  small: true,
};
```

- A: `mouse.bird.size` is not valid
- B: `mouse[bird.size]` is not valid
- C: `mouse[bird["size"]]` is not valid
- D: All of them are valid

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
In JavaScript, all object keys are strings (unless it's a Symbol). Even though we might not _type_ them as strings, they are always converted into strings under the hood.

JavaScript interprets (or unboxes) statements. When we use bracket notation, it sees the first opening bracket `[` and keeps going until it finds the closing bracket `]`. Only then, it will evaluate the statement.

`mouse[bird.size]`: First it evaluates `bird.size`, which is `"small"`. `mouse["small"]` returns `true`

However, with dot notation, this doesn't happen. `mouse` does not have a key called `bird`, which means that `mouse.bird` is `undefined`. Then, we ask for the `size` using dot notation: `mouse.bird.size`. Since `mouse.bird` is `undefined`, we're actually asking `undefined.size`. This isn't valid, and will throw an error similar to `Cannot read property "size" of undefined`.
</p>
</details>

---

### Q. What is the output?

```javascript
let c = { greeting: "Hey!" };
let d;

d = c;
c.greeting = "Hello";
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey!`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
In JavaScript, all objects interact by _reference_ when setting them equal to each other.

First, variable `c` holds a value to an object. Later, we assign `d` with the same reference that `c` has to the object.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

When you change one object, you change all of them.
</p>
</details>

---

### Q. What is the output?

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>
`new Number()` is a built-in function constructor. Although it looks like a number, it's not really a number: it has a bunch of extra features and is an object.

When we use the `==` operator, it only checks whether it has the same _value_. They both have the value of `3`, so it returns `true`.

However, when we use the `===` operator, both value _and_ type should be the same. It's not: `new Number()` is not a number, it's an **object**. Both return `false.`
</p>
</details>

---

### Q. What is the output?

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = "green" } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: "purple" });
console.log(freddie.colorChange("orange"));
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>
The `colorChange` function is static. Static methods are designed to live only on the constructor in which they are created, and cannot be passed down to any children. Since `freddie` is a child, the function is not passed down, and not available on the `freddie` instance: a `TypeError` is thrown.
</p>
</details>

---

### Q. What is the output?

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
It logs the object, because we just created an empty object on the global object! When we mistyped `greeting` as `greetign`, the JS interpreter actually saw this as `global.greetign = {}` (or `window.greetign = {}` in a browser).

In order to avoid this, we can use `"use strict"`. This makes sure that you have declared a variable before setting it equal to anything.
</p>
</details>

---

### Q. What happens when we do this?

```javascript
function bark() {
  console.log("Woof!");
}

bark.animal = "dog";
```

- A: Nothing, this is totally fine!
- B: `SyntaxError`. You cannot add properties to a function this way.
- C: `"Woof"` gets logged.
- D: `ReferenceError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
This is possible in JavaScript, because functions are objects! (Everything besides primitive types are objects)

A function is a special type of object. The code you write yourself isn't the actual function. The function is an object with properties. This property is invocable.
</p>
</details>

---

### Q. What is the output?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Jhone", "Hallie");
Person.getFullName = function () {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Jhone Hallie`
- D: `undefined` `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
In JavaScript, functions are objects, and therefore, the method `getFullName` gets added to the constructor function object itself. For that reason, we can call `Person.getFullName()`, but `member.getFullName` throws a `TypeError`. 

If you want a method to be available to all object instances, you have to add it to the prototype property:

```js
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};```

would have made `member.getFullName()` work. Why is this beneficial? Say that we added this method to the constructor itself. Maybe not every `Person` instance needed this method. This would waste a lot of memory space, since they would still have that property, which takes of memory space for each instance. Instead, if we only add it to the prototype, we just have it at one spot in memory, yet they all have access to it!
</p>
</details>

---

### Q. What is the output?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const Jhone = new Person("Jhone", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(Jhone);
console.log(sarah);
```

- A: `Person {firstName: "Jhone", lastName: "Hallie"}` and `undefined`
- B: `Person {firstName: "Jhone", lastName: "Hallie"}` and `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Jhone", lastName: "Hallie"}` and `{}`
- D:`Person {firstName: "Jhone", lastName: "Hallie"}` and `ReferenceError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
For `sarah`, we didn't use the `new` keyword. When using `new`, `this` refers to the new empty object we create. However, if you don't add `new`, `this` refers to the **global object**!

We said that `this.firstName` equals `"Sarah"` and `this.lastName` equals `"Smith"`. What we actually did, is defining `global.firstName = 'Sarah'` and `global.lastName = 'Smith'`. `sarah` itself is left `undefined`, since we don't return a value from the `Person` function.
</p>
</details>

---

### Q. What are the three phases of event propagation?

- A: Target > Capturing > Bubbling
- B: Bubbling > Target > Capturing
- C: Target > Bubbling > Capturing
- D: Capturing > Target > Bubbling

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>
During the **capturing** phase, the event goes through the ancestor elements down to the target element. It then reaches the **target** element, and **bubbling** begins.

<img src="https://i.imgur.com/N18oRgd.png" width="200">

</p>
</details>

---

### Q. All object have prototypes.

- A: true
- B: false

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>
All objects have prototypes, except for the **base object**. The base object is the object created by the user, or an object that is created using the `new` keyword. The base object has access to some methods and properties, such as `.toString`. This is the reason why you can use built-in JavaScript methods! All of such methods are available on the prototype. Although JavaScript can't find it directly on your object, it goes down the prototype chain and finds it there, which makes it accessible for you.
</p>
</details>

---

### Q. What is the output?

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, "2");
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

JavaScript is a **dynamically typed language**: we don't specify what types certain variables are. Values can automatically be converted into another type without you knowing, which is called _implicit type coercion_. **Coercion** is converting from one type into another.

In this example, JavaScript converts the number `1` into a string, in order for the function to make sense and return a value. During the addition of a numeric type (`1`) and a string type (`'2'`), the number is treated as a string. We can concatenate strings like `"Hello" + "World"`, so what's happening here is `"1" + "2"` which returns `"12"`.

</p>
</details>

---

### Q. What is the output?

```javascript
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

- A: `1` `1` `2`
- B: `1` `2` `2`
- C: `0` `2` `2`
- D: `0` `1` `2`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The **postfix** unary operator `++`:

1. Returns the value (this returns `0`)
2. Increments the value (number is now `1`)

The **prefix** unary operator `++`:

1. Increments the value (number is now `2`)
2. Returns the value (this returns `2`)

This returns `0 2 2`.

</p>
</details>

---

### Q. What is the output?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = "Jhone";
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Jhone"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Jhone"` `21`
- C: `"Jhone"` `["", " is ", " years old"]` `21`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

If you use tagged template literals, the value of the first argument is always an array of the string values. The remaining arguments get the values of the passed expressions!

</p>
</details>

---

### Q. What is the output?

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log("You are an adult!");
  } else if (data == { age: 18 }) {
    console.log("You are still an adult.");
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

- A: `You are an adult!`
- B: `You are still an adult.`
- C: `Hmm.. You don't have an age I guess`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

When testing equality, primitives are compared by their _value_, while objects are compared by their _reference_. JavaScript checks if the objects have a reference to the same location in memory.

The two objects that we are comparing don't have that: the object we passed as a parameter refers to a different location in memory than the object we used in order to check equality.

This is why both `{ age: 18 } === { age: 18 }` and `{ age: 18 } == { age: 18 }` return `false`.

</p>
</details>

---

### Q. What is the output?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The rest parameter (`...args`) lets us "collect" all remaining arguments into an array. An array is an object, so `typeof args` returns `"object"`

</p>
</details>

---

### Q. What is the output?

```javascript
function getAge() {
  "use strict";
  age = 21;
  console.log(age);
}

getAge();
```

- A: `21`
- B: `undefined`
- C: `ReferenceError`
- D: `TypeError`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

With `"use strict"`, you can make sure that you don't accidentally declare global variables. We never declared the variable `age`, and since we use `"use strict"`, it will throw a reference error. If we didn't use `"use strict"`, it would have worked, since the property `age` would have gotten added to the global object.

</p>
</details>

---

### Q. What is value of `sum`?

```javascript
const sum = eval("10*10+5");
```

- A: `105`
- B: `"105"`
- C: `TypeError`
- D: `"10*10+5"`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
`eval` evaluates codes that's passed as a string. If it's an expression, like in this case, it evaluates the expression. The expression is `10 * 10 + 5`. This returns the number `105`.

</p>
</details>

---

### Q. How long is cool_secret accessible?

```javascript
sessionStorage.setItem("cool_secret", 123);
```

- A: Forever, the data doesn't get lost.
- B: When the user closes the tab.
- C: When the user closes the entire browser, not only the tab.
- D: When the user shuts off their computer.

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

The data stored in `sessionStorage` is removed after closing the _tab_.

If you used `localStorage`, the data would've been there forever, unless for example `localStorage.clear()` is invoked.

</p>
</details>

---

### Q. What is the output?

```javascript
var num = 8;
var num = 10;

console.log(num);
```

- A: `8`
- B: `10`
- C: `SyntaxError`
- D: `ReferenceError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

With the `var` keyword, you can declare multiple variables with the same name. The variable will then hold the latest value.
You cannot do this with `let` or `const` since they're block-scoped.

</p>
</details>

---

### Q. What is the output?

```javascript
const obj = { 1: "a", 2: "b", 3: "c" };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty("1");
obj.hasOwnProperty(1);
set.has("1");
set.has(1);
```

- A: `false` `true` `false` `true`
- B: `false` `true` `true` `true`
- C: `true` `true` `false` `true`
- D: `true` `true` `true` `true`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

All object keys (excluding Symbols) are strings under the hood, even if you don't type it yourself as a string. This is why `obj.hasOwnProperty('1')` also returns true.

It doesn't work that way for a set. There is no `'1'` in our set: `set.has('1')` returns `false`. It has the numeric type `1`, `set.has(1)` returns `true`.

</p>
</details>

---

### Q. What is the output?

```javascript
const obj = { a: "one", b: "two", a: "three" };
console.log(obj);
```

- A: `{ a: "one", b: "two" }`
- B: `{ b: "two", a: "three" }`
- C: `{ a: "three", b: "two" }`
- D: `SyntaxError`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

If you have two keys with the same name, the key will be replaced. It will still be in its first position, but with the last specified value.

</p>
</details>

---

### Q. The JavaScript global execution context creates two things for you: the global object, and the "this" keyword.

- A: true
- B: false
- C: it depends

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
The base execution context is the global execution context: it's what's accessible everywhere in your code.

</p>
</details>

---

### Q. What is the output?

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The `continue` statement skips an iteration if a certain condition returns `true`.

</p>
</details>

---

### Q. What is the output?

```javascript
String.prototype.giveJhonePizza = () => {
  return "Just give Jhone pizza already!";
};

const name = "Jhone";

name.giveJhonePizza();
```

- A: `"Just give Jhone pizza already!"`
- B: `TypeError: not a function`
- C: `SyntaxError`
- D: `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

`String` is a built-in constructor, which we can add properties to. I just added a method to its prototype. Primitive strings are automatically converted into a string object, generated by the string prototype function. So, all strings (string objects) have access to that method!

</p>
</details>

---

### Q. What is the output?

```javascript
const a = {};
const b = { key: "b" };
const c = { key: "c" };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

Object keys are automatically converted into strings. We are trying to set an object as a key to object `a`, with the value of `123`.

However, when we stringify an object, it becomes `"[object Object]"`. So what we are saying here, is that `a["[object Object]"] = 123`. Then, we can try to do the same again. `c` is another object that we are implicitly stringifying. So then, `a["[object Object]"] = 456`.

Then, we log `a[b]`, which is actually `a["[object Object]"]`. We just set that to `456`, so it returns `456`.

</p>
</details>

---

### Q. What is the output?

```javascript
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"));
const baz = () => console.log("Third");

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

We have a `setTimeout` function and invoked it first. Yet, it was logged last.

This is because in browsers, we don't just have the runtime engine, we also have something called a `WebAPI`. The `WebAPI` gives us the `setTimeout` function to start with, and for example the DOM.

After the _callback_ is pushed to the WebAPI, the `setTimeout` function itself (but not the callback!) is popped off the stack.

<img src="https://i.imgur.com/X5wsHOg.png" width="200">

Now, `foo` gets invoked, and `"First"` is being logged.

<img src="https://i.imgur.com/Pvc0dGq.png" width="200">

`foo` is popped off the stack, and `baz` gets invoked. `"Third"` gets logged.

<img src="https://i.imgur.com/WhA2bCP.png" width="200">

The WebAPI can't just add stuff to the stack whenever it's ready. Instead, it pushes the callback function to something called the _queue_.

<img src="https://i.imgur.com/NSnDZmU.png" width="200">

This is where an event loop starts to work. An **event loop** looks at the stack and task queue. If the stack is empty, it takes the first thing on the queue and pushes it onto the stack.

<img src="https://i.imgur.com/uyiScAI.png" width="200">

`bar` gets invoked, `"Second"` gets logged, and it's popped off the stack.

</p>
</details>

---


### Q. What is the event.target when clicking the button?

```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">Click!</button>
  </div>
</div>
```

- A: Outer `div`
- B: Inner `div`
- C: `button`
- D: An array of all nested elements.

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The deepest nested element that caused the event is the target of the event. You can stop bubbling by `event.stopPropagation`

</p>
</details>

---

### Q. When you click the paragraph, What is the logged output?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">Click here!</p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

If we click `p`, we see two logs: `p` and `div`. During event propagation, there are 3 phases: capturing, target, and bubbling. By default, event handlers are executed in the bubbling phase (unless you set `useCapture` to `true`). It goes from the deepest nested element outwards.

</p>
</details>

---

### Q. What is the output?

```javascript
const person = { name: "Jhone" };

function sayHi(age) {
  console.log(`${this.name} is ${age}`);
}

sayHi.call(person, 21);
sayHi.bind(person, 21);
```

- A: `undefined is 21` `Jhone is 21`
- B: `function` `function`
- C: `Jhone is 21` `Jhone is 21`
- D: `Jhone is 21` `function`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

With both, we can pass the object to which we want the `this` keyword to refer to. However, `.call` is also _executed immediately_!

`.bind.` returns a _copy_ of the function, but with a bound context! It is not executed immediately.

</p>
</details>

---

### Q. What is the output?

```javascript
function sayHi() {
  return (() => 0)();
}

console.log(typeof sayHi());
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

**Answer: B**

<details><summary><b>Explanation</b></summary>
<p>
The `sayHi` function returns the returned value of the immediately invoked function expression (IIFE). This function returned `0`, which is type `"number"`.

FYI: there are only 7 built-in types: `null`, `undefined`, `boolean`, `number`, `string`, `object`, and `symbol`. `"function"` is not a type, since functions are objects, it's of type `"object"`.

</p>
</details>

---

### Q. Which of these values are falsy?

```javascript
0;
new Number(0);
("");
(" ");
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: All of them are falsy

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

There are 8 falsy values:

- `undefined`
- `null`
- `NaN`
- `false`
- `''` (empty string)
- `0`
- `-0`
- `0n` (BigInt(0))

Function constructors, like `new Number` and `new Boolean` are truthy.

</p>
</details>

---

### Q. Predict the output of the following JavaScript code?

```javascript
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

`typeof 1` returns `"number"`.
`typeof "number"` returns `"string"`

</p>
</details>

---

### Q. What is the output?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

When you set a value to an element in an array that exceeds the length of the array, JavaScript creates something called "empty slots". These actually have the value of `undefined`, but you will see something like:

`[1, 2, 3, 7 x empty, 11]`

depending on where you run it (it's different for every browser, node, etc.)

</p>
</details>

---

### Q. What is the output?

```javascript
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

The `catch` block receives the argument `x`. This is not the same `x` as the variable when we pass arguments. This variable `x` is block-scoped.

Later, we set this block-scoped variable equal to `1`, and set the value of the variable `y`. Now, we log the block-scoped variable `x`, which is equal to `1`.

Outside of the `catch` block, `x` is still `undefined`, and `y` is `2`. When we want to `console.log(x)` outside of the `catch` block, it returns `undefined`, and `y` returns `2`.

</p>
</details>

---

### Q. Everything in JavaScript is either a...

- A: primitive or object
- B: function or object
- C: trick question! only objects
- D: number or object

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
JavaScript only has primitive types and objects.

Primitive types are `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, and `symbol`.

What differentiates a primitive from an object is that primitives do not have any properties or methods; however, you'll note that `'foo'.toUpperCase()` evaluates to `'FOO'` and does not result in a `TypeError`. This is because when you try to access a property or method on a primitive like a string, JavaScript will implicitly wrap the primitive type using one of the wrapper classes, i.e. `String`, and then immediately discard the wrapper after the expression evaluates. All primitives except for `null` and `undefined` exhibit this behaviour.

</p>
</details>

---

### Q. What is the output?

```javascript
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2]
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

`[1, 2]` is our initial value. This is the value we start with, and the value of the very first `acc`. During the first round, `acc` is `[1,2]`, and `cur` is `[0, 1]`. We concatenate them, which results in `[1, 2, 0, 1]`.

Then, `[1, 2, 0, 1]` is `acc` and `[2, 3]` is `cur`. We concatenate them, and get `[1, 2, 0, 1, 2, 3]`

</p>
</details>

---

### Q. What is the output?

```javascript
!!null;
!!"";
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

`null` is falsy. `!null` returns `true`. `!true` returns `false`.

`""` is falsy. `!""` returns `true`. `!true` returns `false`.

`1` is truthy. `!1` returns `false`. `!false` returns `true`.

</p>
</details>

---

### Q. What does the `setInterval` method return in the browser?

```javascript
setInterval(() => console.log("Hi"), 1000);
```

- A: a unique id
- B: the amount of milliseconds specified
- C: the passed function
- D: `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

It returns a unique id. This id can be used to clear that interval with the `clearInterval()` function.

</p>
</details>

---

### Q. What does this return?

```javascript
[..."Jhone"];
```

- A: `["J", "h", "o", "n", "e"]`
- B: `["Jhone"]`
- C: `[[], "Jhone"]`
- D: `[["J", "h", "o", "n", "e"]]`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
A string is an iterable. The spread operator maps every character of an iterable to one element.

</p>
</details>

---

### Q. What is the output?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Regular functions cannot be stopped mid-way after invocation. However, a generator function can be "stopped" midway, and later continue from where it stopped. Every time a generator function encounters a `yield` keyword, the function yields the value specified after it. Note that the generator function in that case doesn’t _return_ the value, it _yields_ the value.

First, we initialize the generator function with `i` equal to `10`. We invoke the generator function using the `next()` method. The first time we invoke the generator function, `i` is equal to `10`. It encounters the first `yield` keyword: it yields the value of `i`. The generator is now "paused", and `10` gets logged.

Then, we invoke the function again with the `next()` method. It starts to continue where it stopped previously, still with `i` equal to `10`. Now, it encounters the next `yield` keyword, and yields `i * 2`. `i` is equal to `10`, so it returns `10 * 2`, which is `20`. This results in `10, 20`.

</p>
</details>

---

### Q. What does this return?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, "one");
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, "two");
});

Promise.race([firstPromise, secondPromise]).then((res) => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

When we pass multiple promises to the `Promise.race` method, it resolves/rejects the _first_ promise that resolves/rejects. To the `setTimeout` method, we pass a timer: 500ms for the first promise (`firstPromise`), and 100ms for the second promise (`secondPromise`). This means that the `secondPromise` resolves first with the value of `'two'`. `res` now holds the value of `'two'`, which gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
let person = { name: "Jhone" };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Jhone" }]`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

First, we declare a variable `person` with the value of an object that has a `name` property.

<img src="https://i.imgur.com/TML1MbS.png" width="200">

Then, we declare a variable called `members`. We set the first element of that array equal to the value of the `person` variable. Objects interact by _reference_ when setting them equal to each other. When you assign a reference from one variable to another, you make a _copy_ of that reference. (note that they don't have the _same_ reference!)

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

Then, we set the variable `person` equal to `null`.

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

We are only modifying the value of the `person` variable, and not the first element in the array, since that element has a different (copied) reference to the object. The first element in `members` still holds its reference to the original object. When we log the `members` array, the first element still holds the value of the object, which gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
const person = {
  name: "Jhone",
  age: 21,
};

for (const item in person) {
  console.log(item);
}
```

- A: `{ name: "Jhone" }, { age: 21 }`
- B: `"name", "age"`
- C: `"Jhone", 21`
- D: `["name", "Jhone"], ["age", 21]`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

With a `for-in` loop, we can iterate through object keys, in this case `name` and `age`. Under the hood, object keys are strings (if they're not a Symbol). On every loop, we set the value of `item` equal to the current key it’s iterating over. First, `item` is equal to `name`, and gets logged. Then, `item` is equal to `age`, which gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
console.log(3 + 4 + "5");
```

- A: `"345"`
- B: `"75"`
- C: `12`
- D: `"12"`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

Operator associativity is the order in which the compiler evaluates the expressions, either left-to-right or right-to-left. This only happens if all operators have the _same_ precedence. We only have one type of operator: `+`. For addition, the associativity is left-to-right.

`3 + 4` gets evaluated first. This results in the number `7`.

`7 + '5'` results in `"75"` because of coercion. JavaScript converts the number `7` into a string, see question 15. We can concatenate two strings using the `+`operator. `"7" + "5"` results in `"75"`.

</p>
</details>

---


### Q. What is the value of `num`?

```javascript
const num = parseInt("7*6", 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Only the first numbers in the string is returned. Based on the _radix_ (the second argument in order to specify what type of number we want to parse it to: base 10, hexadecimal, octal, binary, etc.), the `parseInt` checks whether the characters in the string are valid. Once it encounters a character that isn't a valid number in the radix, it stops parsing and ignores the following characters.

`*` is not a valid number. It only parses `"7"` into the decimal `7`. `num` now holds the value of `7`.

</p>
</details>

---

### Q. What is the output`?

```javascript
[1, 2, 3].map((num) => {
  if (typeof num === "number") return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

When mapping over the array, the value of `num` is equal to the element it’s currently looping over. In this case, the elements are numbers, so the condition of the if statement `typeof num === "number"` returns `true`. The map function creates a new array and inserts the values returned from the function.

However, we don’t return a value. When we don’t return a value from the function, the function returns `undefined`. For every element in the array, the function block gets called, so for each element we return `undefined`.

</p>
</details>

---

### Q. What is the output?

```javascript
function getInfo(member, year) {
  member.name = "Jhone";
  year = "1998";
}

const person = { name: "Sarah" };
const birthYear = "1997";

getInfo(person, birthYear);

console.log(person, birthYear);
```

- A: `{ name: "Jhone" }, "1997"`
- B: `{ name: "Sarah" }, "1998"`
- C: `{ name: "Jhone" }, "1998"`
- D: `{ name: "Sarah" }, "1997"`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

Arguments are passed by _value_, unless their value is an object, then they're passed by _reference_. `birthYear` is passed by value, since it's a string, not an object. When we pass arguments by value, a _copy_ of that value is created (see question 46).

The variable `birthYear` has a reference to the value `"1997"`. The argument `year` also has a reference to the value `"1997"`, but it's not the same value as `birthYear` has a reference to. When we update the value of `year` by setting `year` equal to `"1998"`, we are only updating the value of `year`. `birthYear` is still equal to `"1997"`.

The value of `person` is an object. The argument `member` has a (copied) reference to the _same_ object. When we modify a property of the object `member` has a reference to, the value of `person` will also be modified, since they both have a reference to the same object. `person`'s `name` property is now equal to the value `"Jhone"`

</p>
</details>

---

### Q. What is the output?

```javascript
function greeting() {
  throw "Hello world!";
}

function sayHi() {
  try {
    const data = greeting();
    console.log("It worked!", data);
  } catch (e) {
    console.log("Oh no an error:", e);
  }
}

sayHi();
```
- A: `It worked! Hello world!`
- B: `Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `Oh no an error: Hello world!`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>
With the `throw` statement, we can create custom errors. With this statement, you can throw exceptions. An exception can be a <b>string</b>, a <b>number</b>, a <b>boolean</b> or an <b>object</b>. In this case, our exception is the string `'Hello world!'`.

With the `catch` statement, we can specify what to do if an exception is thrown in the `try` block. An exception is thrown: the string `'Hello world!'`. `e` is now equal to that string, which we log. This results in `'Oh an error: Hello world!'`.
</p>
</details>

---

### Q. What is the output?

```javascript
function Car() {
  this.make = "Lamborghini";
  return { make: "Maserati" };
}

const myCar = new Car();
console.log(myCar.make);
```

- A: `"Lamborghini"`
- B: `"Maserati"`
- C: `ReferenceError`
- D: `TypeError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>
When you return a property, the value of the property is equal to the _returned_ value, not the value set in the constructor function. We return the string `"Maserati"`, so `myCar.make` is equal to `"Maserati"`.
</p>
</details>

---

### Q. What is the output?

```javascript
(() => {
  let x = (y = 10);
})();

console.log(typeof x);
console.log(typeof y);
```

- A: `"undefined", "number"`
- B: `"number", "number"`
- C: `"object", "number"`
- D: `"number", "undefined"`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
`let x = (y = 10);` is actually shorthand for:

```javascript
y = 10;
let x = y;
```

When we set `y` equal to `10`, we actually add a property `y` to the global object (`window` in browser, `global` in Node). In a browser, `window.y` is now equal to `10`.

Then, we declare a variable `x` with the value of `y`, which is `10`. Variables declared with the `let` keyword are _block scoped_, they are only defined within the block they're declared in; the immediately invoked function expression (IIFE) in this case. When we use the `typeof` operator, the operand `x` is not defined: we are trying to access `x` outside of the block it's declared in. This means that `x` is not defined. Values who haven't been assigned a value or declared are of type `"undefined"`. `console.log(typeof x)` returns `"undefined"`.

However, we created a global variable `y` when setting `y` equal to `10`. This value is accessible anywhere in our code. `y` is defined, and holds a value of type `"number"`. `console.log(typeof y)` returns `"number"`.

</p>
</details>

---


### Q. What is the output?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
}

Dog.prototype.bark = function () {
  console.log(`Woof I am ${this.name}`);
};

const pet = new Dog("Mara");

pet.bark();

delete Dog.prototype.bark;

pet.bark();
```
- A: `"Woof I am Mara"`, `TypeError`
- B: `"Woof I am Mara"`, `"Woof I am Mara"`
- C: `"Woof I am Mara"`, `undefined`
- D: `TypeError`, `TypeError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>
We can delete properties from objects using the `delete` keyword, also on the prototype. By deleting a property on the prototype, it is not available anymore in the prototype chain. In this case, the `bark` function is not available anymore on the prototype after `delete Dog.prototype.bark`, yet we still try to access it.

When we try to invoke something that is not a function, a `TypeError` is thrown. In this case `TypeError: pet.bark is not a function`, since `pet.bark` is `undefined`.
</p>
</details>

---

### Q. What is the output?

```javascript
const set = new Set([1, 1, 2, 3, 4]);

console.log(set);
```

- A: `[1, 1, 2, 3, 4]`
- B: `[1, 2, 3, 4]`
- C: `{1, 1, 2, 3, 4}`
- D: `{1, 2, 3, 4}`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>
The `Set` object is a collection of _unique_ values: a value can only occur once in a set.

We passed the iterable `[1, 1, 2, 3, 4]` with a duplicate value `1`. Since we cannot have two of the same values in a set, one of them is removed. This results in `{1, 2, 3, 4}`.
</p>
</details>

---

### Q. What is the output?

```javascript
// counter.js
let counter = 10;
export default counter;
```

```javascript
// index.js
import myCounter from "./counter";

myCounter += 1;

console.log(myCounter);
```

- A: `10`
- B: `11`
- C: `Error`
- D: `NaN`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>
An imported module is _read-only_: you cannot modify the imported module. Only the module that exports them can change its value.

When we try to increment the value of `myCounter`, it throws an error: `myCounter` is read-only and cannot be modified.
</p>
</details>

---

### Q. What is the output?

```javascript
const name = "Jhone";
age = 21;

console.log(delete name);
console.log(delete age);
```

- A: `false`, `true`
- B: `"Jhone"`, `21`
- C: `true`, `true`
- D: `undefined`, `undefined`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

The `delete` operator returns a boolean value: `true` on a successful deletion, else it'll return `false`. However, variables declared with the `var`, `const` or `let` keyword cannot be deleted using the `delete` operator.

The `name` variable was declared with a `const` keyword, so its deletion is not successful: `false` is returned. When we set `age` equal to `21`, we actually added a property called `age` to the global object. You can successfully delete properties from objects this way, also the global object, so `delete age` returns `true`.

</p>
</details>

---

### Q. What is the output?

```javascript
const numbers = [1, 2, 3, 4, 5];
const [y] = numbers;

console.log(y);
```

- A: `[[1, 2, 3, 4, 5]]`
- B: `[1, 2, 3, 4, 5]`
- C: `1`
- D: `[1]`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

We can unpack values from arrays or properties from objects through destructuring. For example:

```javascript
[a, b] = [1, 2];
```

<img src="https://i.imgur.com/ADFpVop.png" width="200">

The value of `a` is now `1`, and the value of `b` is now `2`. What we actually did in the question, is:

```javascript
[y] = [1, 2, 3, 4, 5];
```

<img src="https://i.imgur.com/NzGkMNk.png" width="200">

This means that the value of `y` is equal to the first value in the array, which is the number `1`. When we log `y`, `1` is returned.

</p>
</details>

---

### Q. What is the output?

```javascript
const user = { name: "Jhone", age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```

- A: `{ admin: true, user: { name: "Jhone", age: 21 } }`
- B: `{ admin: true, name: "Jhone", age: 21 }`
- C: `{ admin: true, user: ["Jhone", 21] }`
- D: `{ admin: true }`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

It's possible to combine objects using the spread operator `...`. It lets you create copies of the key/value pairs of one object, and add them to another object. In this case, we create copies of the `user` object, and add them to the `admin` object. The `admin` object now contains the copied key/value pairs, which results in `{ admin: true, name: "Jhone", age: 21 }`.

</p>
</details>

---

### Q. What is the output?

```javascript
const person = { name: "Jhone" };

Object.defineProperty(person, "age", { value: 21 });

console.log(person);
console.log(Object.keys(person));
```

- A: `{ name: "Jhone", age: 21 }`, `["name", "age"]`
- B: `{ name: "Jhone", age: 21 }`, `["name"]`
- C: `{ name: "Jhone"}`, `["name", "age"]`
- D: `{ name: "Jhone"}`, `["age"]`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

With the `defineProperty` method, we can add new properties to an object, or modify existing ones. When we add a property to an object using the `defineProperty` method, they are by default _not enumerable_. The `Object.keys` method returns all _enumerable_ property names from an object, in this case only `"name"`.

Properties added using the `defineProperty` method are immutable by default. You can override this behavior using the `writable`, `configurable` and `enumerable` properties. This way, the `defineProperty` method gives you a lot more control over the properties you're adding to an object.

</p>
</details>

---

### Q. What is the output?

```javascript
const settings = {
  username: "Jhonehallie",
  level: 19,
  health: 90,
};

const data = JSON.stringify(settings, ["level", "health"]);
console.log(data);
```

- A: `"{"level":19, "health":90}"`
- B: `"{"username": "Jhonehallie"}"`
- C: `"["level", "health"]"`
- D: `"{"username": "Jhonehallie", "level":19, "health":90}"`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

The second argument of `JSON.stringify` is the _replacer_. The replacer can either be a function or an array, and lets you control what and how the values should be stringified.

If the replacer is an _array_, only the property names included in the array will be added to the JSON string. In this case, only the properties with the names `"level"` and `"health"` are included, `"username"` is excluded. `data` is now equal to `"{"level":19, "health":90}"`.

If the replacer is a _function_, this function gets called on every property in the object you're stringifying. The value returned from this function will be the value of the property when it's added to the JSON string. If the value is `undefined`, this property is excluded from the JSON string.

</p>
</details>

---

### Q. What is the output?

```javascript
let num = 10;

const increaseNumber = () => num++;
const increasePassedNumber = (number) => number++;

const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);

console.log(num1);
console.log(num2);
```

- A: `10`, `10`
- B: `10`, `11`
- C: `11`, `11`
- D: `11`, `12`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

The unary operator `++` _first returns_ the value of the operand, _then increments_ the value of the operand. The value of `num1` is `10`, since the `increaseNumber` function first returns the value of `num`, which is `10`, and only increments the value of `num` afterwards.

`num2` is `10`, since we passed `num1` to the `increasePassedNumber`. `number` is equal to `10`(the value of `num1`. Again, the unary operator `++` _first returns_ the value of the operand, _then increments_ the value of the operand. The value of `number` is `10`, so `num2` is equal to `10`.

</p>
</details>

---

### Q. What is the output?

```javascript
const value = { number: 10 };

const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};

multiply();
multiply();
multiply(value);
multiply(value);
```

- A: `20`, `40`, `80`, `160`
- B: `20`, `40`, `20`, `40`
- C: `20`, `20`, `20`, `40`
- D: `NaN`, `NaN`, `20`, `40`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

In ES6, we can initialize parameters with a default value. The value of the parameter will be the default value, if no other value has been passed to the function, or if the value of the parameter is `"undefined"`. In this case, we spread the properties of the `value` object into a new object, so `x` has the default value of `{ number: 10 }`.

The default argument is evaluated at _call time_! Every time we call the function, a _new_ object is created. We invoke the `multiply` function the first two times without passing a value: `x` has the default value of `{ number: 10 }`. We then log the multiplied value of that number, which is `20`.

The third time we invoke multiply, we do pass an argument: the object called `value`. The `*=` operator is actually shorthand for `x.number = x.number * 2`: we modify the value of `x.number`, and log the multiplied value `20`.

The fourth time, we pass the `value` object again. `x.number` was previously modified to `20`, so `x.number *= 2` logs `40`.

</p>
</details>

---

### Q. What is the output?

```javascript
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```

- A: `1` `2` and `3` `3` and `6` `4`
- B: `1` `2` and `2` `3` and `3` `4`
- C: `1` `undefined` and `2` `undefined` and `3` `undefined` and `4` `undefined`
- D: `1` `2` and `undefined` `3` and `undefined` `4`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

The first argument that the `reduce` method receives is the _accumulator_, `x` in this case. The second argument is the _current value_, `y`. With the reduce method, we execute a callback function on every element in the array, which could ultimately result in one single value.

In this example, we are not returning any values, we are simply logging the values of the accumulator and the current value.

The value of the accumulator is equal to the previously returned value of the callback function. If you don't pass the optional `initialValue` argument to the `reduce` method, the accumulator is equal to the first element on the first call.

On the first call, the accumulator (`x`) is `1`, and the current value (`y`) is `2`. We don't return from the callback function, we log the accumulator and current value: `1` and `2` get logged.

If you don't return a value from a function, it returns `undefined`. On the next call, the accumulator is `undefined`, and the current value is `3`. `undefined` and `3` get logged.

On the fourth call, we again don't return from the callback function. The accumulator is again `undefined`, and the current value is `4`. `undefined` and `4` get logged.

</p>
</details>
  
---

### Q. With which constructor can we successfully extend the `Dog` class?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
}

class Labrador extends Dog {
  // 1
  constructor(name, size) {
    this.size = size;
  }
  // 2
  constructor(name, size) {
    super(name);
    this.size = size;
  }
  // 3
  constructor(size) {
    super(name);
    this.size = size;
  }
  // 4
  constructor(name, size) {
    this.name = name;
    this.size = size;
  }
}
```

- A: 1
- B: 2
- C: 3
- D: 4

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

In a derived class, you cannot access the `this` keyword before calling `super`. If you try to do that, it will throw a ReferenceError: 1 and 4 would throw a reference error.

With the `super` keyword, we call that parent class's constructor with the given arguments. The parent's constructor receives the `name` argument, so we need to pass `name` to `super`.

The `Labrador` class receives two arguments, `name` since it extends `Dog`, and `size` as an extra property on the `Labrador` class. They both need to be passed to the constructor function on `Labrador`, which is done correctly using constructor 2.

</p>
</details>

---

### Q. What is the output?

```javascript
// index.js
console.log("running index.js");
import { sum } from "./sum.js";
console.log(sum(1, 2));

// sum.js
console.log("running sum.js");
export const sum = (a, b) => a + b;
```

- A: `running index.js`, `running sum.js`, `3`
- B: `running sum.js`, `running index.js`, `3`
- C: `running sum.js`, `3`, `running index.js`
- D: `running index.js`, `undefined`, `running sum.js`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

With the `import` keyword, all imported modules are _pre-parsed_. This means that the imported modules get run _first_, the code in the file which imports the module gets executed _after_.

This is a difference between `require()` in CommonJS and `import`! With `require()`, you can load dependencies on demand while the code is being run. If we would have used `require` instead of `import`, `running index.js`, `running sum.js`, `3` would have been logged to the console.

</p>
</details>

---

### Q. What is the output?

```javascript
console.log(Number(2) === Number(2));
console.log(Boolean(false) === Boolean(false));
console.log(Symbol("foo") === Symbol("foo"));
```

- A: `true`, `true`, `false`
- B: `false`, `true`, `false`
- C: `true`, `false`, `true`
- D: `true`, `true`, `true`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

Every Symbol is entirely unique. The purpose of the argument passed to the Symbol is to give the Symbol a description. The value of the Symbol is not dependent on the passed argument. As we test equality, we are creating two entirely new symbols: the first `Symbol('foo')`, and the second `Symbol('foo')`. These two values are unique and not equal to each other, `Symbol('foo') === Symbol('foo')` returns `false`.

</p>
</details>

---

### Q. What is the output?

```javascript
const name = "Jhone Hallie";
console.log(name.padStart(13));
console.log(name.padStart(2));
```

- A: `"Jhone Hallie"`, `"Jhone Hallie"`
- B: `" Jhone Hallie"`, `" Jhone Hallie"` (`"[13x whitespace]Jhone Hallie"`, `"[2x whitespace]Jhone Hallie"`)
- C: `" Jhone Hallie"`, `"Jhone Hallie"` (`"[1x whitespace]Jhone Hallie"`, `"Jhone Hallie"`)
- D: `"Jhone Hallie"`, `"Lyd"`,

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

With the `padStart` method, we can add padding to the beginning of a string. The value passed to this method is the _total_ length of the string together with the padding. The string `"Jhone Hallie"` has a length of `12`. `name.padStart(13)` inserts 1 space at the start of the string, because 12 + 1 is 13.

If the argument passed to the `padStart` method is smaller than the length of the array, no padding will be added.

</p>
</details>

---

### Q. What is the output?

```javascript
console.log("🥑" + "💻");
```

- A: `"🥑💻"`
- B: `257548`
- C: A string containing their code points
- D: Error

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With the `+` operator, you can concatenate strings. In this case, we are concatenating the string `"🥑"` with the string `"💻"`, resulting in `"🥑💻"`.

</p>
</details>

---

### Q. How can we log the values that are commented out after the console.log statement?

```javascript
function* startGame() {
  const answer = yield "Do you love JavaScript?";
  if (answer !== "Yes") {
    return "Oh wow... Guess we're gone here";
  }
  return "JavaScript loves you back ❤️";
}

const game = startGame();
console.log(/* 1 */); // Do you love JavaScript?
console.log(/* 2 */); // JavaScript loves you back ❤️
```

- A: `game.next("Yes").value` and `game.next().value`
- B: `game.next.value("Yes")` and `game.next.value()`
- C: `game.next().value` and `game.next("Yes").value`
- D: `game.next.value()` and `game.next.value("Yes")`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

A generator function "pauses" its execution when it sees the `yield` keyword. First, we have to let the function yield the string "Do you love JavaScript?", which can be done by calling `game.next().value`.

Every line is executed, until it finds the first `yield` keyword. There is a `yield` keyword on the first line within the function: the execution stops with the first yield! _This means that the variable `answer` is not defined yet!_

When we call `game.next("Yes").value`, the previous `yield` is replaced with the value of the parameters passed to the `next()` function, `"Yes"` in this case. The value of the variable `answer` is now equal to `"Yes"`. The condition of the if-statement returns `false`, and `JavaScript loves you back ❤️` gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
console.log(String.raw`Hello\nworld`);
```

- A: `Hello world!`
- B: `Hello` <br />&nbsp; &nbsp; &nbsp;`world`
- C: `Hello\nworld`
- D: `Hello\n` <br /> &nbsp; &nbsp; &nbsp;`world`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

`String.raw` returns a string where the escapes (`\n`, `\v`, `\t` etc.) are ignored! Backslashes can be an issue since you could end up with something like:

`` const path = `C:\Documents\Projects\table.html` ``

Which would result in:

`"C:DocumentsProjects able.html"`

With `String.raw`, it would simply ignore the escape and print:

`C:\Documents\Projects\table.html`

In this case, the string is `Hello\nworld`, which gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
async function getData() {
  return await Promise.resolve("I made it!");
}

const data = getData();
console.log(data);
```

- A: `"I made it!"`
- B: `Promise {<resolved>: "I made it!"}`
- C: `Promise {<pending>}`
- D: `undefined`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

An async function always returns a promise. The `await` still has to wait for the promise to resolve: a pending promise gets returned when we call `getData()` in order to set `data` equal to it.

If we wanted to get access to the resolved value `"I made it"`, we could have used the `.then()` method on `data`:

`data.then(res => console.log(res))`

This would've logged `"I made it!"`

</p>
</details>

---

### Q. What is the output?

```javascript
function addToList(item, list) {
  return list.push(item);
}

const result = addToList("apple", ["banana"]);
console.log(result);
```

- A: `['apple', 'banana']`
- B: `2`
- C: `true`
- D: `undefined`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

The `.push()` method returns the _length_ of the new array! Previously, the array contained one element (the string `"banana"`) and had a length of `1`. After adding the string `"apple"` to the array, the array contains two elements, and has a length of `2`. This gets returned from the `addToList` function.

The `push` method modifies the original array. If you wanted to return the _array_ from the function rather than the _length of the array_, you should have returned `list` after pushing `item` to it.

</p>
</details>

---

### Q. What is the output?

```javascript
const box = { x: 10, y: 20 };

Object.freeze(box);

const shape = box;
shape.x = 100;

console.log(shape);
```

- A: `{ x: 100, y: 20 }`
- B: `{ x: 10, y: 20 }`
- C: `{ x: 100 }`
- D: `ReferenceError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

`Object.freeze` makes it impossible to add, remove, or modify properties of an object (unless the property's value is another object).

When we create the variable `shape` and set it equal to the frozen object `box`, `shape` also refers to a frozen object. You can check whether an object is frozen by using `Object.isFrozen`. In this case, `Object.isFrozen(shape)` returns true, since the variable `shape` has a reference to a frozen object.

Since `shape` is frozen, and since the value of `x` is not an object, we cannot modify the property `x`. `x` is still equal to `10`, and `{ x: 10, y: 20 }` gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
const { name: myName } = { name: "Jhone" };

console.log(name);
```

- A: `"Jhone"`
- B: `"myName"`
- C: `undefined`
- D: `ReferenceError`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

When we unpack the property `name` from the object on the right-hand side, we assign its value `"Jhone"` to a variable with the name `myName`.

With `{ name: myName }`, we tell JavaScript that we want to create a new variable called `myName` with the value of the `name` property on the right-hand side.

Since we try to log `name`, a variable that is not defined, a ReferenceError gets thrown.

</p>
</details>

---

### Q. Is this a pure function?

```javascript
function sum(a, b) {
  return a + b;
}
```

- A: Yes
- B: No

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

A pure function is a function that _always_ returns the same result, if the same arguments are passed.

The `sum` function always returns the same result. If we pass `1` and `2`, it will _always_ return `3` without side effects. If we pass `5` and `10`, it will _always_ return `15`, and so on. This is the definition of a pure function.

</p>
</details>

---

### Q. What is the output?

```javascript
const add = () => {
  const cache = {};
  return (num) => {
    if (num in cache) {
      return `From cache! ${cache[num]}`;
    } else {
      const result = num + 10;
      cache[num] = result;
      return `Calculated! ${result}`;
    }
  };
};

const addFunction = add();
console.log(addFunction(10));
console.log(addFunction(10));
console.log(addFunction(5 * 2));
```

- A: `Calculated! 20` `Calculated! 20` `Calculated! 20`
- B: `Calculated! 20` `From cache! 20` `Calculated! 20`
- C: `Calculated! 20` `From cache! 20` `From cache! 20`
- D: `Calculated! 20` `From cache! 20` `Error`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The `add` function is a _memoized_ function. With memoization, we can cache the results of a function in order to speed up its execution. In this case, we create a `cache` object that stores the previously returned values.

If we call the `addFunction` function again with the same argument, it first checks whether it has already gotten that value in its cache. If that's the case, the caches value will be returned, which saves on execution time. Else, if it's not cached, it will calculate the value and store it afterwards.

We call the `addFunction` function three times with the same value: on the first invocation, the value of the function when `num` is equal to `10` isn't cached yet. The condition of the if-statement `num in cache` returns `false`, and the else block gets executed: `Calculated! 20` gets logged, and the value of the result gets added to the cache object. `cache` now looks like `{ 10: 20 }`.

The second time, the `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

The third time, we pass `5 * 2` to the function which gets evaluated to `10`. The `cache` object contains the value that gets returned for `10`. The condition of the if-statement `num in cache` returns `true`, and `'From cache! 20'` gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
const myLifeSummedUp = ["☕", "💻", "🍷", "🍫"];

for (let item in myLifeSummedUp) {
  console.log(item);
}

for (let item of myLifeSummedUp) {
  console.log(item);
}
```

- A: `0` `1` `2` `3` and `"☕"` ` "💻"` `"🍷"` `"🍫"`
- B: `"☕"` ` "💻"` `"🍷"` `"🍫"` and `"☕"` ` "💻"` `"🍷"` `"🍫"`
- C: `"☕"` ` "💻"` `"🍷"` `"🍫"` and `0` `1` `2` `3`
- D: `0` `1` `2` `3` and `{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

With a _for-in_ loop, we can iterate over **enumerable** properties. In an array, the enumerable properties are the "keys" of array elements, which are actually their indexes. You could see an array as:

`{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

Where the keys are the enumerable properties. `0` `1` `2` `3` get logged.

With a _for-of_ loop, we can iterate over **iterables**. An array is an iterable. When we iterate over the array, the variable "item" is equal to the element it's currently iterating over, `"☕"` `"💻"` `"🍷"` `"🍫"` get logged.

</p>
</details>

---

### Q. What is the output?

```javascript
const list = [1 + 2, 1 * 2, 1 / 2];
console.log(list);
```

- A: `["1 + 2", "1 * 2", "1 / 2"]`
- B: `["12", 2, 0.5]`
- C: `[3, 2, 0.5]`
- D: `[1, 1, 1]`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Array elements can hold any value. Numbers, strings, objects, other arrays, null, boolean values, undefined, and other expressions such as dates, functions, and calculations.

The element will be equal to the returned value. `1 + 2` returns `3`, `1 * 2` returns `2`, and `1 / 2` returns `0.5`.

</p>
</details>

---

### Q. What is the output?

```javascript
function sayHi(name) {
  return `Hi there, ${name}`;
}

console.log(sayHi());
```

- A: `Hi there, `
- B: `Hi there, undefined`
- C: `Hi there, null`
- D: `ReferenceError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

By default, arguments have the value of `undefined`, unless a value has been passed to the function. In this case, we didn't pass a value for the `name` argument. `name` is equal to `undefined` which gets logged.

In ES6, we can overwrite this default `undefined` value with default parameters. For example:

`function sayHi(name = "Jhone") { ... }`

In this case, if we didn't pass a value or if we passed `undefined`, `name` would always be equal to the string `Jhone`

</p>
</details>

---

### Q. What is the output?

```javascript
var status = "😎";

setTimeout(() => {
  const status = "😍";

  const data = {
    status: "🥑",
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());
  console.log(data.getStatus.call(this));
}, 0);
```

- A: `"🥑"` and `"😍"`
- B: `"🥑"` and `"😎"`
- C: `"😍"` and `"😎"`
- D: `"😎"` and `"😎"`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

The value of the `this` keyword is dependent on where you use it. In a **method**, like the `getStatus` method, the `this` keyword refers to _the object that the method belongs to_. The method belongs to the `data` object, so `this` refers to the `data` object. When we log `this.status`, the `status` property on the `data` object gets logged, which is `"🥑"`.

With the `call` method, we can change the object to which the `this` keyword refers. In **functions**, the `this` keyword refers to the _the object that the function belongs to_. We declared the `setTimeout` function on the _global object_, so within the `setTimeout` function, the `this` keyword refers to the _global object_. On the global object, there is a variable called _status_ with the value of `"😎"`. When logging `this.status`, `"😎"` gets logged.

</p>
</details>

---

### Q. What is the output?

```javascript
const person = {
  name: "Jhone",
  age: 21,
};

let city = person.city;
city = "Amsterdam";

console.log(person);
```

- A: `{ name: "Jhone", age: 21 }`
- B: `{ name: "Jhone", age: 21, city: "Amsterdam" }`
- C: `{ name: "Jhone", age: 21, city: undefined }`
- D: `"Amsterdam"`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

We set the variable `city` equal to the value of the property called `city` on the `person` object. There is no property on this object called `city`, so the variable `city` has the value of `undefined`.

Note that we are _not_ referencing the `person` object itself! We simply set the variable `city` equal to the current value of the `city` property on the `person` object.

Then, we set `city` equal to the string `"Amsterdam"`. This doesn't change the person object: there is no reference to that object.

When logging the `person` object, the unmodified object gets returned.

</p>
</details>

---

### Q. What is the output?

```javascript
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }

  return message;
}

console.log(checkAge(21));
```

- A: `"Sorry, you're too young."`
- B: `"Yay! You're old enough!"`
- C: `ReferenceError`
- D: `undefined`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Variables with the `const` and `let` keyword are _block-scoped_. A block is anything between curly brackets (`{ }`). In this case, the curly brackets of the if/else statements. You cannot reference a variable outside of the block it's declared in, a ReferenceError gets thrown.

</p>
</details>

---

### Q. What kind of information would get logged?

```javascript
fetch("https://www.website.com/api/user/1")
  .then((res) => res.json())
  .then((res) => console.log(res));
```

- A: The result of the `fetch` method.
- B: The result of the second invocation of the `fetch` method.
- C: The result of the callback in the previous `.then()`.
- D: It would always be undefined.

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The value of `res` in the second `.then` is equal to the returned value of the previous `.then`. You can keep chaining `.then`s like this, where the value is passed to the next handler.

</p>
</details>

---

### Q. Which option is a way to set `hasName` equal to `true`, provided you cannot pass `true` as an argument?

```javascript
function getName(name) {
  const hasName = //
}
```

- A: `!!name`
- B: `name`
- C: `new Boolean(name)`
- D: `name.length`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

With `!!name`, we determine whether the value of `name` is truthy or falsy. If name is truthy, which we want to test for, `!name` returns `false`. `!false` (which is what `!!name` practically is) returns `true`.

By setting `hasName` equal to `name`, you set `hasName` equal to whatever value you passed to the `getName` function, not the boolean value `true`.

`new Boolean(true)` returns an object wrapper, not the boolean value itself.

`name.length` returns the length of the passed argument, not whether it's `true`.

</p>
</details>

---

### Q. What is the output?

```javascript
console.log("I want pizza"[0]);
```

- A: `"""`
- B: `"I"`
- C: `SyntaxError`
- D: `undefined`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

In order to get an character on a specific index in a string, you can use bracket notation. The first character in the string has index 0, and so on. In this case we want to get the element which index is 0, the character `"I'`, which gets logged.

Note that this method is not supported in IE7 and below. In that case, use `.charAt()`

</p>
</details>

---

### Q. What is the output?

```javascript
function sum(num1, num2 = num1) {
  console.log(num1 + num2);
}

sum(10);
```

- A: `NaN`
- B: `20`
- C: `ReferenceError`
- D: `undefined`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

You can set a default parameter's value equal to another parameter of the function, as long as they've been defined _before_ the default parameter. We pass the value `10` to the `sum` function. If the `sum` function only receives 1 argument, it means that the value for `num2` is not passed, and the value of `num1` is equal to the passed value `10` in this case. The default value of `num2` is the value of `num1`, which is `10`. `num1 + num2` returns `20`.

If you're trying to set a default parameter's value equal to a parameter which is defined _after_ (to the right), the parameter's value hasn't been initialized yet, which will throw an error.

</p>
</details>

---

### Q. What is the output?

```javascript
// module.js
export default () => "Hello world";
export const name = "Jhone";

// index.js
import * as data from "./module";

console.log(data);
```

- A: `{ default: function default(), name: "Jhone" }`
- B: `{ default: function default() }`
- C: `{ default: "Hello world", name: "Jhone" }`
- D: Global object of `module.js`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

With the `import * as name` syntax, we import _all exports_ from the `module.js` file into the `index.js` file as a new object called `data` is created. In the `module.js` file, there are two exports: the default export, and a named export. The default export is a function which returns the string `"Hello World"`, and the named export is a variable called `name` which has the value of the string `"Jhone"`.

The `data` object has a `default` property for the default export, other properties have the names of the named exports and their corresponding values.

</p>
</details>

---

### Q. What is the output?

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

const member = new Person("John");
console.log(typeof member);
```

- A: `"class"`
- B: `"function"`
- C: `"object"`
- D: `"string"`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Classes are syntactical sugar for function constructors. The equivalent of the `Person` class as a function constructor would be:

```javascript
function Person() {
  this.name = name;
}
```

Calling a function constructor with `new` results in the creation of an instance of `Person`, `typeof` keyword returns `"object"` for an instance. `typeof member` returns `"object"`.

</p>
</details>

---

### Q. What is the output?

```javascript
let newList = [1, 2, 3].push(4);

console.log(newList.push(5));
```

- A: `[1, 2, 3, 4, 5]`
- B: `[1, 2, 3, 5]`
- C: `[1, 2, 3, 4]`
- D: `Error`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

The `.push` method returns the _new length_ of the array, not the array itself! By setting `newList` equal to `[1, 2, 3].push(4)`, we set `newList` equal to the new length of the array: `4`.

Then, we try to use the `.push` method on `newList`. Since `newList` is the numerical value `4`, we cannot use the `.push` method: a TypeError is thrown.

</p>
</details>

---

### Q. What is the output?

```javascript
function giveJhonePizza() {
  return "Here is pizza!";
}

const giveJhoneChocolate = () =>
  "Here's chocolate... now go hit the gym already.";

console.log(giveJhonePizza.prototype);
console.log(giveJhoneChocolate.prototype);
```

- A: `{ constructor: ...}` `{ constructor: ...}`
- B: `{}` `{ constructor: ...}`
- C: `{ constructor: ...}` `{}`
- D: `{ constructor: ...}` `undefined`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

Regular functions, such as the `giveJhonePizza` function, have a `prototype` property, which is an object (prototype object) with a `constructor` property. Arrow functions however, such as the `giveJhoneChocolate` function, do not have this `prototype` property. `undefined` gets returned when trying to access the `prototype` property using `giveJhoneChocolate.prototype`.

</p>
</details>

---

### Q. What is the output?

```javascript
const person = {
  name: "Jhone",
  age: 21,
};

for (const [x, y] of Object.entries(person)) {
  console.log(x, y);
}
```

- A: `name` `Jhone` and `age` `21`
- B: `["name", "Jhone"]` and `["age", 21]`
- C: `["name", "age"]` and `undefined`
- D: `Error`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

`Object.entries(person)` returns an array of nested arrays, containing the keys and objects:

`[ [ 'name', 'Jhone' ], [ 'age', 21 ] ]`

Using the `for-of` loop, we can iterate over each element in the array, the subarrays in this case. We can destructure the subarrays instantly in the for-of loop, using `const [x, y]`. `x` is equal to the first element in the subarray, `y` is equal to the second element in the subarray.

The first subarray is `[ "name", "Jhone" ]`, with `x` equal to `"name"`, and `y` equal to `"Jhone"`, which get logged.
The second subarray is `[ "age", 21 ]`, with `x` equal to `"age"`, and `y` equal to `21`, which get logged.

</p>
</details>

---

### Q. What is the output?

```javascript
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

- A: `["banana", "apple", "pear", "orange"]`
- B: `[["banana", "apple"], "pear", "orange"]`
- C: `["banana", "apple", ["pear"], "orange"]`
- D: `SyntaxError`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

`...args` is a rest parameter. The rest parameter's value is an array containing all remaining arguments, **and can only be the last parameter**! In this example, the rest parameter was the second parameter. This is not possible, and will throw a syntax error.

```javascript
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit];
}

getItems(['banana', 'apple'], 'pear', 'orange');
```

The above example works. This returns the array `[ 'banana', 'apple', 'orange', 'pear' ]`

</p>
</details>

---

### Q. What is the output?

```javascript
function nums(a, b) {
  if (a > b) console.log("a is bigger");
  else console.log("b is bigger");
  return;
  a + b;
}

console.log(nums(4, 2));
console.log(nums(1, 2));
```

- A: `a is bigger`, `6` and `b is bigger`, `3`
- B: `a is bigger`, `undefined` and `b is bigger`, `undefined`
- C: `undefined` and `undefined`
- D: `SyntaxError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

In JavaScript, we don't _have_ to write the semicolon (`;`) explicitly, however the JavaScript engine still adds them after statements. This is called **Automatic Semicolon Insertion**. A statement can for example be variables, or keywords like `throw`, `return`, `break`, etc.

Here, we wrote a `return` statement, and another value `a + b` on a _new line_. However, since it's a new line, the engine doesn't know that it's actually the value that we wanted to return. Instead, it automatically added a semicolon after `return`. You could see this as:

```javascript
return;
a + b;
```

This means that `a + b` is never reached, since a function stops running after the `return` keyword. If no value gets returned, like here, the function returns `undefined`. Note that there is no automatic insertion after `if/else` statements!

</p>
</details>

---

### Q. What is the output?

```javascript
class Person {
  constructor() {
    this.name = "Jhone";
  }
}

Person = class AnotherPerson {
  constructor() {
    this.name = "Sarah";
  }
};

const member = new Person();
console.log(member.name);
```

- A: `"Jhone"`
- B: `"Sarah"`
- C: `Error: cannot redeclare Person`
- D: `SyntaxError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

We can set classes equal to other classes/function constructors. In this case, we set `Person` equal to `AnotherPerson`. The name on this constructor is `Sarah`, so the name property on the new `Person` instance `member` is `"Sarah"`.

</p>
</details>

---

### Q. What is the output?

```javascript
const info = {
  [Symbol("a")]: "b",
};

console.log(info);
console.log(Object.keys(info));
```

- A: `{Symbol('a'): 'b'}` and `["{Symbol('a')"]`
- B: `{}` and `[]`
- C: `{ a: "b" }` and `["a"]`
- D: `{Symbol('a'): 'b'}` and `[]`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

A Symbol is not _enumerable_. The Object.keys method returns all _enumerable_ key properties on an object. The Symbol won't be visible, and an empty array is returned. When logging the entire object, all properties will be visible, even non-enumerable ones.

This is one of the many qualities of a symbol: besides representing an entirely unique value (which prevents accidental name collision on objects, for example when working with 2 libraries that want to add properties to the same object), you can also "hide" properties on objects this way (although not entirely. You can still access symbols using the `Object.getOwnPropertySymbols()` method).

</p>
</details>

---

### Q. What is the output?

```javascript
const getList = ([x, ...y]) => [x, y]
const getUser = user => { name: user.name, age: user.age }

const list = [1, 2, 3, 4]
const user = { name: "Jhone", age: 21 }

console.log(getList(list))
console.log(getUser(user))
```

- A: `[1, [2, 3, 4]]` and `undefined`
- B: `[1, [2, 3, 4]]` and `{ name: "Jhone", age: 21 }`
- C: `[1, 2, 3, 4]` and `{ name: "Jhone", age: 21 }`
- D: `Error` and `{ name: "Jhone", age: 21 }`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

The `getList` function receives an array as its argument. Between the parentheses of the `getList` function, we destructure this array right away. You could see this as:

`[x, ...y] = [1, 2, 3, 4]`

With the rest parameter `...y`, we put all "remaining" arguments in an array. The remaining arguments are `2`, `3` and `4` in this case. The value of `y` is an array, containing all the rest parameters. The value of `x` is equal to `1` in this case, so when we log `[x, y]`, `[1, [2, 3, 4]]` gets logged.

The `getUser` function receives an object. With arrow functions, we don't _have_ to write curly brackets if we just return one value. However, if you want to return an _object_ from an arrow function, you have to write it between parentheses, otherwise no value gets returned! The following function would have returned an object:

`const getUser = user => ({ name: user.name, age: user.age })`

Since no value gets returned in this case, the function returns `undefined`.

</p>
</details>

---

### Q. What is the output?

```javascript
const name = "Jhone";

console.log(name());
```

- A: `SyntaxError`
- B: `ReferenceError`
- C: `TypeError`
- D: `undefined`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The variable `name` holds the value of a string, which is not a function, thus cannot invoke.

TypeErrors get thrown when a value is not of the expected type. JavaScript expected `name` to be a function since we're trying to invoke it. It was a string however, so a TypeError gets thrown: name is not a function!

SyntaxErrors get thrown when you've written something that isn't valid JavaScript, for example when you've written the word `return` as `retrun`.
ReferenceErrors get thrown when JavaScript isn't able to find a reference to a value that you're trying to access.

</p>
</details>

---

### Q. What is the value of output?

```javascript
// 🎉✨ This is my 100th question! ✨🎉

const output = `${[] && "Im"}possible!
You should${"" && `n't`} see a therapist after so much JavaScript lol`;
```

- A: `possible! You should see a therapist after so much JavaScript lol`
- B: `Impossible! You should see a therapist after so much JavaScript lol`
- C: `possible! You shouldn't see a therapist after so much JavaScript lol`
- D: `Impossible! You shouldn't see a therapist after so much JavaScript lol`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

`[]` is a truthy value. With the `&&` operator, the right-hand value will be returned if the left-hand value is a truthy value. In this case, the left-hand value `[]` is a truthy value, so `"Im'` gets returned.

`""` is a falsy value. If the left-hand value is falsy, nothing gets returned. `n't` doesn't get returned.

</p>
</details>

---

### Q. What is the value of output?

```javascript
const one = false || {} || null;
const two = null || false || "";
const three = [] || 0 || true;

console.log(one, two, three);
```

- A: `false` `null` `[]`
- B: `null` `""` `true`
- C: `{}` `""` `[]`
- D: `null` `null` `true`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

With the `||` operator, we can return the first truthy operand. If all values are falsy, the last operand gets returned.

`(false || {} || null)`: the empty object `{}` is a truthy value. This is the first (and only) truthy value, which gets returned. `one` is equal to `{}`.

`(null || false || "")`: all operands are falsy values. This means that the last operand, `""` gets returned. `two` is equal to `""`.

`([] || 0 || "")`: the empty array`[]` is a truthy value. This is the first truthy value, which gets returned. `three` is equal to `[]`.

</p>
</details>

---

### Q. What is the value of output?

```javascript
const myPromise = () => Promise.resolve("I have resolved!");

function firstFunction() {
  myPromise().then((res) => console.log(res));
  console.log("second");
}

async function secondFunction() {
  console.log(await myPromise());
  console.log("second");
}

firstFunction();
secondFunction();
```

- A: `I have resolved!`, `second` and `I have resolved!`, `second`
- B: `second`, `I have resolved!` and `second`, `I have resolved!`
- C: `I have resolved!`, `second` and `second`, `I have resolved!`
- D: `second`, `I have resolved!` and `I have resolved!`, `second`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

With a promise, we basically say _I want to execute this function, but I'll put it aside for now while it's running since this might take a while. Only when a certain value is resolved (or rejected), and when the call stack is empty, I want to use this value._

We can get this value with both `.then` and the `await` keyword in an `async` function. Although we can get a promise's value with both `.then` and `await`, they work a bit differently.

In the `firstFunction`, we (sort of) put the myPromise function aside while it was running, but continued running the other code, which is `console.log('second')` in this case. Then, the function resolved with the string `I have resolved`, which then got logged after it saw that the callstack was empty.

With the await keyword in `secondFunction`, we literally pause the execution of an async function until the value has been resolved before moving to the next line.

This means that it waited for the `myPromise` to resolve with the value `I have resolved`, and only once that happened, we moved to the next line: `second` got logged.

</p>
</details>

---

### Q. What is the value of output?

```javascript
const set = new Set();

set.add(1);
set.add("Jhone");
set.add({ name: "Jhone" });

for (let item of set) {
  console.log(item + 2);
}
```

- A: `3`, `NaN`, `NaN`
- B: `3`, `7`, `NaN`
- C: `3`, `Jhone2`, `[Object object]2`
- D: `"12"`, `Jhone2`, `[Object object]2`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

The `+` operator is not only used for adding numerical values, but we can also use it to concatenate strings. Whenever the JavaScript engine sees that one or more values are not a number, it coerces the number into a string.

The first one is `1`, which is a numerical value. `1 + 2` returns the number 3.

However, the second one is a string `"Jhone"`. `"Jhone"` is a string and `2` is a number: `2` gets coerced into a string. `"Jhone"` and `"2"` get concatenated, which results in the string `"Jhone2"`.

`{ name: "Jhone" }` is an object. Neither a number nor an object is a string, so it stringifies both. Whenever we stringify a regular object, it becomes `"[object Object]"`. `"[object Object]"` concatenated with `"2"` becomes `"[object Object]2"`.

</p>
</details>

---

### Q. What is its value?

```javascript
Promise.resolve(5);
```

- A: `5`
- B: `Promise {<pending>: 5}`
- C: `Promise {<resolved>: 5}`
- D: `Error`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

We can pass any type of value we want to `Promise.resolve`, either a promise or a non-promise. The method itself returns a promise with the resolved value (`<fulfilled>`). If you pass a regular function, it'll be a resolved promise with a regular value. If you pass a promise, it'll be a resolved promise with the resolved value of that passed promise.

In this case, we just passed the numerical value `5`. It returns a resolved promise with the value `5`.

</p>
</details>

---

### Q. What is its value?

```javascript
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log("Not the same!");
  } else {
    console.log("They are the same!");
  }
}

const person = { name: "Jhone" };

compareMembers(person);
```

- A: `Not the same!`
- B: `They are the same!`
- C: `ReferenceError`
- D: `SyntaxError`

**Answer: B**

<details><summary><b>Answer</b></summary>
<p>

Objects are passed by reference. When we check objects for strict equality (`===`), we're comparing their references.

We set the default value for `person2` equal to the `person` object, and passed the `person` object as the value for `person1`.

This means that both values have a reference to the same spot in memory, thus they are equal.

The code block in the `else` statement gets run, and `They are the same!` gets logged.

</p>
</details>

---

### Q. What is its value?

```javascript
const colorConfig = {
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false,
};

const colors = ["pink", "red", "blue"];

console.log(colorConfig.colors[1]);
```

- A: `true`
- B: `false`
- C: `undefined`
- D: `TypeError`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

In JavaScript, we have two ways to access properties on an object: bracket notation, or dot notation. In this example, we use dot notation (`colorConfig.colors`) instead of bracket notation (`colorConfig["colors"]`).

With dot notation, JavaScript tries to find the property on the object with that exact name. In this example, JavaScript tries to find a property called `colors` on the `colorConfig` object. There is no property called `colors`, so this returns `undefined`. Then, we try to access the value of the first element by using `[1]`. We cannot do this on a value that's `undefined`, so it throws a `TypeError`: `Cannot read property '1' of undefined`.

JavaScript interprets (or unboxes) statements. When we use bracket notation, it sees the first opening bracket `[` and keeps going until it finds the closing bracket `]`. Only then, it will evaluate the statement. If we would've used `colorConfig[colors[1]]`, it would have returned the value of the `red` property on the `colorConfig` object.

</p>
</details>

---

### Q. What is its value?

```javascript
console.log("❤️" === "❤️");
```

- A: `true`
- B: `false`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

Under the hood, emojis are unicodes. The unicodes for the heart emoji is `"U+2764 U+FE0F"`. These are always the same for the same emojis, so we're comparing two equal strings to each other, which returns true.

</p>
</details>

---

### Q. Which of these methods modifies the original array?

```javascript
const emojis = ["✨", "🥑", "😍"];

emojis.map((x) => x + "✨");
emojis.filter((x) => x !== "🥑");
emojis.find((x) => x !== "🥑");
emojis.reduce((acc, cur) => acc + "✨");
emojis.slice(1, 2, "✨");
emojis.splice(1, 2, "✨");
```

- A: `All of them`
- B: `map` `reduce` `slice` `splice`
- C: `map` `slice` `splice`
- D: `splice`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

With `splice` method, we modify the original array by deleting, replacing or adding elements. In this case, we removed 2 items from index 1 (we removed `'🥑'` and `'😍'`) and added the ✨ emoji instead.

`map`, `filter` and `slice` return a new array, `find` returns an element, and `reduce` returns a reduced value.

</p>
</details>

---

### Q. What is the output?

```javascript
const food = ["🍕", "🍫", "🥑", "🍔"];
const info = { favoriteFood: food[0] };

info.favoriteFood = "🍝";

console.log(food);
```

- A: `['🍕', '🍫', '🥑', '🍔']`
- B: `['🍝', '🍫', '🥑', '🍔']`
- C: `['🍝', '🍕', '🍫', '🥑', '🍔']`
- D: `ReferenceError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

We set the value of the `favoriteFood` property on the `info` object equal to the string with the pizza emoji, `'🍕'`. A string is a primitive data type. In JavaScript, primitive data types don't interact by reference.

In JavaScript, primitive data types (everything that's not an object) interact by _value_. In this case, we set the value of the `favoriteFood` property on the `info` object equal to the value of the first element in the `food` array, the string with the pizza emoji in this case (`'🍕'`). A string is a primitive data type, and interact by value (see my [blogpost](https://www.theavocoder.com/complete-javascript/2018/12/21/by-value-vs-by-reference) if you're interested in learning more)

Then, we change the value of the `favoriteFood` property on the `info` object. The `food` array hasn't changed, since the value of `favoriteFood` was merely a _copy_ of the value of the first element in the array, and doesn't have a reference to the same spot in memory as the element on `food[0]`. When we log food, it's still the original array, `['🍕', '🍫', '🥑', '🍔']`.

</p>
</details>

---


### Q. What does this method do?

```javascript
JSON.parse();
```

- A: Parses JSON to a JavaScript value
- B: Parses a JavaScript object to JSON
- C: Parses any JavaScript value to JSON
- D: Parses JSON to a JavaScript object only

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

With the `JSON.parse()` method, we can parse JSON string to a JavaScript value.

```javascript
// Stringifying a number into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonNumber = JSON.stringify(4); // '4'
JSON.parse(jsonNumber); // 4

// Stringifying an array value into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonArray = JSON.stringify([1, 2, 3]); // '[1, 2, 3]'
JSON.parse(jsonArray); // [1, 2, 3]

// Stringifying an object  into valid JSON, then parsing the JSON string to a JavaScript value:
const jsonArray = JSON.stringify({ name: 'Jhone' }); // '{"name":"Jhone"}'
JSON.parse(jsonArray); // { name: 'Jhone' }
```

</p>
</details>

---

### Q. What is the output?

```javascript
let name = "Jhone";

function getName() {
  console.log(name);
  let name = "Sarah";
}

getName();
```

- A: Jhone
- B: Sarah
- C: `undefined`
- D: `ReferenceError`

**Answer: D**

<details><summary><b>Answer</b></summary>
<p>

Each function has its own _execution context_ (or _scope_). The `getName` function first looks within its own context (scope) to see if it contains the variable `name` we're trying to access. In this case, the `getName` function contains its own `name` variable: we declare the variable `name` with the `let` keyword, and with the value of `'Sarah'`.

Variables with the `let` keyword (and `const`) are hoisted, but unlike `var`, don't get <i>initialized</i>. They are not accessible before the line we declare (initialize) them. This is called the "temporal dead zone". When we try to access the variables before they are declared, JavaScript throws a `ReferenceError`.

If we wouldn't have declared the `name` variable within the `getName` function, the javascript engine would've looked down the _scope chain_. The outer scope has a variable called `name` with the value of `Jhone`. In that case, it would've logged `Jhone`.

```javascript
let name = 'Jhone';

function getName() {
  console.log(name);
}

getName(); // Jhone
```

</p>
</details>

---

### Q. What is the output?

```javascript
function* generatorOne() {
  yield ["a", "b", "c"];
}

function* generatorTwo() {
  yield* ["a", "b", "c"];
}

const one = generatorOne();
const two = generatorTwo();

console.log(one.next().value);
console.log(two.next().value);
```

- A: `a` and `a`
- B: `a` and `undefined`
- C: `['a', 'b', 'c']` and `a`
- D: `a` and `['a', 'b', 'c']`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

With the `yield` keyword, we `yield` values in a generator function. With the `yield*` keyword, we can yield values from another generator function, or iterable object (for example an array).

In `generatorOne`, we yield the entire array `['a', 'b', 'c']` using the `yield` keyword. The value of `value` property on the object returned by the `next` method on `one` (`one.next().value`) is equal to the entire array `['a', 'b', 'c']`.

```javascript
console.log(one.next().value); // ['a', 'b', 'c']
console.log(one.next().value); // undefined
```

In `generatorTwo`, we use the `yield*` keyword. This means that the first yielded value of `two`, is equal to the first yielded value in the iterator. The iterator is the array `['a', 'b', 'c']`. The first yielded value is `a`, so the first time we call `two.next().value`, `a` is returned.

```javascript
console.log(two.next().value); // 'a'
console.log(two.next().value); // 'b'
console.log(two.next().value); // 'c'
console.log(two.next().value); // undefined
```

</p>
</details>

---

### Q. What is the output?

```javascript
console.log(`${((x) => x)("I love")} to program`);
```

- A: `I love to program`
- B: `undefined to program`
- C: `${(x => x)('I love') to program`
- D: `TypeError`

**Answer: A**

<details><summary><b>Answer</b></summary>
<p>

Expressions within template literals are evaluated first. This means that the string will contain the returned value of the expression, the immediately invoked function `(x => x)('I love')` in this case. We pass the value `'I love'` as an argument to the `x => x` arrow function. `x` is equal to `'I love'`, which gets returned. This results in `I love to program`.

</p>
</details>

---

### Q. What will happen?

```javascript
let config = {
  alert: setInterval(() => {
    console.log("Alert!");
  }, 1000),
};

config = null;
```

- A: The `setInterval` callback won't be invoked
- B: The `setInterval` callback gets invoked once
- C: The `setInterval` callback will still be called every second
- D: We never invoked `config.alert()`, config is `null`

**Answer: C**

<details><summary><b>Answer</b></summary>
<p>

Normally when we set objects equal to `null`, those objects get _garbage collected_ as there is no reference anymore to that object. However, since the callback function within `setInterval` is an arrow function (thus bound to the `config` object), the callback function still holds a reference to the `config` object. As long as there is a reference, the object won't get garbage collected. Since it's not garbage collected, the `setInterval` callback function will still get invoked every 1000ms (1s).

</p>
</details>

---

### Q. Which method(s) will return the value `'Hello world!'`?

```javascript
const myMap = new Map();
const myFunc = () => "greeting";

myMap.set(myFunc, "Hello world!");

//1
myMap.get("greeting");
//2
myMap.get(myFunc);
//3
myMap.get(() => "greeting");
```

- A: 1
- B: 2
- C: 2 and 3
- D: All of them

**Answer: B**
<details><summary><b>Answer</b></summary>
<p>
When adding a key/value pair using the `set` method, the key will be the value of the first argument passed to the `set` function, and the value will be the second argument passed to the `set` function. The key is the _function_ `() => 'greeting'` in this case, and the value `'Hello world'`. `myMap` is now `{ () => 'greeting' => 'Hello world!' }`.

1 is wrong, since the key is not `'greeting'` but `() => 'greeting'`.
3 is wrong, since we're creating a new function by passing it as a parameter to the `get` method. Object interact by _reference_. Functions are objects, which is why two functions are never strictly equal, even if they are identical: they have a reference to a different spot in memory.
</p>
</details>
---

### Q. What is the output?

```javascript
const person = {
  name: "Jhone",
  age: 21,
};

const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
  x.age += 1;
  x.name = "Sarah";
};

changeAge(person);
changeAgeAndName();

console.log(person);
```

- A: `{name: "Sarah", age: 22}`
- B: `{name: "Sarah", age: 23}`
- C: `{name: "Jhone", age: 22}`
- D: `{name: "Jhone", age: 23}`

**Answer: C**
<details><summary><b>Answer</b></summary>
<p>
Both the `changeAge` and `changeAgeAndName` functions have a default parameter, namely a _newly_ created object `{ ...person }`. This object has copies of all the key/values in the `person` object.

First, we invoke the `changeAge` function and pass the `person` object as its argument. This function increases the value of the `age` property by 1. `person` is now `{ name: "Jhone", age: 22 }`.

Then, we invoke the `changeAgeAndName` function, however we don't pass a parameter. Instead, the value of `x` is equal to a _new_ object: `{ ...person }`. Since it's a new object, it doesn't affect the values of the properties on the `person` object. `person` is still equal to `{ name: "Jhone", age: 22 }`.
</p>
</details>

---

### Q. Predict the output

```js
if(2 == true) // returns false

if(2 == false) // returns false
```

---









###### 117. Which of the following options will return `6`?

```javascript
function sumValues(x, y, z) {
  return x + y + z;
}
```

- A: `sumValues([...1, 2, 3])`
- B: `sumValues([...[1, 2, 3]])`
- C: `sumValues(...[1, 2, 3])`
- D: `sumValues([1, 2, 3])`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the spread operator `...`, we can _spread_ iterables to individual elements. The `sumValues` function receives three arguments: `x`, `y` and `z`. `...[1, 2, 3]` will result in `1, 2, 3`, which we pass to the `sumValues` function.

</p>
</details>

---

###### 118. What's the output?

```javascript
let num = 1;
const list = ['🥳', '🤠', '🥰', '🤪'];

console.log(list[(num += 1)]);
```

- A: `🤠`
- B: `🥰`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `+=` operand, we're incrementing the value of `num` by `1`. `num` had the initial value `1`, so `1 + 1` is `2`. The item on the second index in the `list` array is 🥰, `console.log(list[2])` prints 🥰.

</p>
</details>

---

###### 119. What's the output?

```javascript
const person = {
  firstName: 'Jhone',
  lastName: 'Hallie',
  pet: {
    name: 'Mara',
    breed: 'Dutch Tulip Hound',
  },
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
};

console.log(person.pet?.name);
console.log(person.pet?.family?.name);
console.log(person.getFullName?.());
console.log(member.getLastName?.());
```

- A: `undefined` `undefined` `undefined` `undefined`
- B: `Mara` `undefined` `Jhone Hallie` `ReferenceError`
- C: `Mara` `null` `Jhone Hallie` `null`
- D: `null` `ReferenceError` `null` `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the optional chaining operator `?.`, we no longer have to explicitly check whether the deeper nested values are valid or not. If we're trying to access a property on an `undefined` or `null` value (_nullish_), the expression short-circuits and returns `undefined`.

`person.pet?.name`: `person` has a property named `pet`: `person.pet` is not nullish. It has a property called `name`, and returns `Mara`.
`person.pet?.family?.name`: `person` has a property named `pet`: `person.pet` is not nullish. `pet` does _not_ have a property called `family`, `person.pet.family` is nullish. The expression returns `undefined`.
`person.getFullName?.()`: `person` has a property named `getFullName`: `person.getFullName()` is not nullish and can get invoked, which returns `Jhone Hallie`.
`member.getLastName?.()`: `member` is not defined: `member.getLastName()` is nullish. The expression returns `undefined`.

</p>
</details>

---

###### 120. What's the output?

```javascript
const groceries = ['banana', 'apple', 'peanuts'];

if (groceries.indexOf('banana')) {
  console.log('We have to buy bananas!');
} else {
  console.log(`We don't have to buy bananas!`);
}
```

- A: We have to buy bananas!
- B: We don't have to buy bananas
- C: `undefined`
- D: `1`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We passed the condition `groceries.indexOf("banana")` to the if-statement. `groceries.indexOf("banana")` returns `0`, which is a falsy value. Since the condition in the if-statement is falsy, the code in the `else` block runs, and `We don't have to buy bananas!` gets logged.

</p>
</details>

---

###### 121. What's the output?

```javascript
const config = {
  languages: [],
  set language(lang) {
    return this.languages.push(lang);
  },
};

console.log(config.language);
```

- A: `function language(lang) { this.languages.push(lang }`
- B: `0`
- C: `[]`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `language` method is a `setter`. Setters don't hold an actual value, their purpose is to _modify_ properties. When calling a `setter` method, `undefined` gets returned.

</p>
</details>

---

###### 122. What's the output?

```javascript
const name = 'Jhone Hallie';

console.log(!typeof name === 'object');
console.log(!typeof name === 'string');
```

- A: `false` `true`
- B: `true` `false`
- C: `false` `false`
- D: `true` `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

`typeof name` returns `"string"`. The string `"string"` is a truthy value, so `!typeof name` returns the boolean value `false`. `false === "object"` and `false === "string"` both return`false`.

(If we wanted to check whether the type was (un)equal to a certain type, we should've written `!==` instead of `!typeof`)

</p>
</details>

---

###### 123. What's the output?

```javascript
const add = x => y => z => {
  console.log(x, y, z);
  return x + y + z;
};

add(4)(5)(6);
```

- A: `4` `5` `6`
- B: `6` `5` `4`
- C: `4` `function` `function`
- D: `undefined` `undefined` `6`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `add` function returns an arrow function, which returns an arrow function, which returns an arrow function (still with me?). The first function receives an argument `x` with the value of `4`. We invoke the second function, which receives an argument `y` with the value `5`. Then we invoke the third function, which receives an argument `z` with the value `6`. When we're trying to access the value `x`, `y` and `z` within the last arrow function, the JS engine goes up the scope chain in order to find the values for `x` and `y` accordingly. This returns `4` `5` `6`.

</p>
</details>

---

###### 124. What's the output?

```javascript
async function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield Promise.resolve(i);
  }
}

(async () => {
  const gen = range(1, 3);
  for await (const item of gen) {
    console.log(item);
  }
})();
```

- A: `Promise {1}` `Promise {2}` `Promise {3}`
- B: `Promise {<pending>}` `Promise {<pending>}` `Promise {<pending>}`
- C: `1` `2` `3`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The generator function `range` returns an async object with promises for each item in the range we pass: `Promise{1}`, `Promise{2}`, `Promise{3}`. We set the variable `gen` equal to the async object, after which we loop over it using a `for await ... of` loop. We set the variable `item` equal to the returned Promise values: first `Promise{1}`, then `Promise{2}`, then `Promise{3}`. Since we're _awaiting_ the value of `item`, the resolved promsie, the resolved _values_ of the promises get returned: `1`, `2`, then `3`.

</p>
</details>

---

###### 125. What's the output?

```javascript
const myFunc = ({ x, y, z }) => {
  console.log(x, y, z);
};

myFunc(1, 2, 3);
```

- A: `1` `2` `3`
- B: `{1: 1}` `{2: 2}` `{3: 3}`
- C: `{ 1: undefined }` `undefined` `undefined`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`myFunc` expects an object with properties `x`, `y` and `z` as its argument. Since we're only passing three separate numeric values (1, 2, 3) instead of one object with properties `x`, `y` and `z` ({x: 1, y: 2, z: 3}), `x`, `y` and `z` have their default value of `undefined`.

</p>
</details>

---

###### 126. What's the output?

```javascript
function getFine(speed, amount) {
  const formattedSpeed = new Intl.NumberFormat('en-US', {
    style: 'unit',
    unit: 'mile-per-hour'
  }).format(speed);

  const formattedAmount = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(amount);

  return `The driver drove ${formattedSpeed} and has to pay ${formattedAmount}`;
}

console.log(getFine(130, 300))
```

- A: The driver drove 130 and has to pay 300
- B: The driver drove 130 mph and has to pay \$300.00
- C: The driver drove undefined and has to pay undefined
- D: The driver drove 130.00 and has to pay 300.00

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `Intl.NumberFormat` method, we can format numeric values to any locale. We format the numeric value `130` to the `en-US` locale as a `unit` in `mile-per-hour`, which results in `130 mph`. The numeric value `300` to the `en-US` locale as a `currency` in `USD` results in `$300.00`.

</p>
</details>

---

###### 127. What's the output?

```javascript
const spookyItems = ['👻', '🎃', '🕸'];
({ item: spookyItems[3] } = { item: '💀' });

console.log(spookyItems);
```

- A: `["👻", "🎃", "🕸"]`
- B: `["👻", "🎃", "🕸", "💀"]`
- C: `["👻", "🎃", "🕸", { item: "💀" }]`
- D: `["👻", "🎃", "🕸", "[object Object]"]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

By destructuring objects, we can unpack values from the right-hand object, and assign the unpacked value to the value of the same property name on the left-hand object. In this case, we're assigning the value "💀" to `spookyItems[3]`. This means that we're modifying the `spookyItems` array, we're adding the "💀" to it. When logging `spookyItems`, `["👻", "🎃", "🕸", "💀"]` gets logged.

</p>
</details>

---

###### 128. What's the output?

```javascript
const name = 'Jhone Hallie';
const age = 21;

console.log(Number.isNaN(name));
console.log(Number.isNaN(age));

console.log(isNaN(name));
console.log(isNaN(age));
```

- A: `true` `false` `true` `false`
- B: `true` `false` `false` `false`
- C: `false` `false` `true` `false`
- D: `false` `true` `false` `true`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the `Number.isNaN` method, you can check if the value you pass is a _numeric value_ and equal to `NaN`. `name` is not a numeric value, so `Number.isNaN(name)` returns `false`. `age` is a numeric value, but is not equal to `NaN`, so `Number.isNaN(age)` returns `false`.

With the `isNaN` method, you can check if the value you pass is not a number. `name` is not a number, so `isNaN(name)` returns true. `age` is a number, so `isNaN(age)` returns `false`.

</p>
</details>

---

###### 129. What's the output?

```javascript
const randomValue = 21;

function getInfo() {
  console.log(typeof randomValue);
  const randomValue = 'Jhone Hallie';
}

getInfo();
```

- A: `"number"`
- B: `"string"`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

Variables declared with the `const` keyword are not referencable before their initialization: this is called the _temporal dead zone_. In the `getInfo` function, the variable `randomValue` is scoped in the functional scope of `getInfo`. On the line where we want to log the value of `typeof randomValue`, the variable `randomValue` isn't initialized yet: a `ReferenceError` gets thrown! The engine didn't go down the scope chain since we declared the variable `randomValue` in the `getInfo` function.

</p>
</details>

---

###### 130. What's the output?

```javascript
const myPromise = Promise.resolve('Woah some cool data');

(async () => {
  try {
    console.log(await myPromise);
  } catch {
    throw new Error(`Oops didn't work`);
  } finally {
    console.log('Oh finally!');
  }
})();
```

- A: `Woah some cool data`
- B: `Oh finally!`
- C: `Woah some cool data` `Oh finally!`
- D: `Oops didn't work` `Oh finally!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

In the `try` block, we're logging the awaited value of the `myPromise` variable: `"Woah some cool data"`. Since no errors were thrown in the `try` block, the code in the `catch` block doesn't run. The code in the `finally` block _always_ runs, `"Oh finally!"` gets logged.

</p>
</details>

---

###### 131. What's the output?

```javascript
const emojis = ['🥑', ['✨', '✨', ['🍕', '🍕']]];

console.log(emojis.flat(1));
```

- A: `['🥑', ['✨', '✨', ['🍕', '🍕']]]`
- B: `['🥑', '✨', '✨', ['🍕', '🍕']]`
- C: `['🥑', ['✨', '✨', '🍕', '🍕']]`
- D: `['🥑', '✨', '✨', '🍕', '🍕']`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

With the `flat` method, we can create a new, flattened array. The depth of the flattened array depends on the value that we pass. In this case, we passed the value `1` (which we didn't have to, that's the default value), meaning that only the arrays on the first depth will be concatenated. `['🥑']` and `['✨', '✨', ['🍕', '🍕']]` in this case. Concatenating these two arrays results in `['🥑', '✨', '✨', ['🍕', '🍕']]`.

</p>
</details>

---

###### 132. What's the output?

```javascript
class Counter {
  constructor() {
    this.count = 0;
  }

  increment() {
    this.count++;
  }
}

const counterOne = new Counter();
counterOne.increment();
counterOne.increment();

const counterTwo = counterOne;
counterTwo.increment();

console.log(counterOne.count);
```

- A: `0`
- B: `1`
- C: `2`
- D: `3`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

`counterOne` is an instance of the `Counter` class. The counter class contains a `count` property on its constructor, and an `increment` method. First, we invoked the `increment` method twice by calling `counterOne.increment()`. Currently, `counterOne.count` is `2`.

<img src="https://i.imgur.com/KxLlTm9.png" width="400">

Then, we create a new variable `counterTwo`, and set it equal to `counterOne`. Since objects interact by reference, we're just creating a new reference to the same spot in memory that `counterOne` points to. Since it has the same spot in memory, any changes made to the object that `counterTwo` has a reference to, also apply to `counterOne`. Currently, `counterTwo.count` is `2`.

We invoke the `counterTwo.increment()`, which sets the `count` to `3`. Then, we log the count on `counterOne`, which logs `3`.

<img src="https://i.imgur.com/BNBHXmc.png" width="400">

</p>
</details>

---

###### 133. What's the output?

```javascript
const myPromise = Promise.resolve(Promise.resolve('Promise!'));

function funcOne() {
  myPromise.then(res => res).then(res => console.log(res));
  setTimeout(() => console.log('Timeout!', 0));
  console.log('Last line!');
}

async function funcTwo() {
  const res = await myPromise;
  console.log(await res);
  setTimeout(() => console.log('Timeout!', 0));
  console.log('Last line!');
}

funcOne();
funcTwo();
```

- A: `Promise! Last line! Promise! Last line! Last line! Promise!`
- B: `Last line! Timeout! Promise! Last line! Timeout! Promise!`
- C: `Promise! Last line! Last line! Promise! Timeout! Timeout!`
- D: `Last line! Promise! Promise! Last line! Timeout! Timeout!`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

First, we invoke `funcOne`. On the first line of `funcOne`, we call the `myPromise` promise, which is an _asynchronous_ operation. While the engine is busy completing the promise, it keeps on running the function `funcOne`. The next line is the _asynchronous_ `setTimeout` function, from which the callback is sent to the Web API. (see my article on the event loop here.)

Both the promise and the timeout are asynchronous operations, the function keeps on running while it's busy completing the promise and handling the `setTimeout` callback. This means that `Last line!` gets logged first, since this is not an asynchonous operation. This is the last line of `funcOne`, the promise resolved, and `Promise!` gets logged. However, since we're invoking `funcTwo()`, the call stack isn't empty, and the callback of the `setTimeout` function cannot get added to the callstack yet.

In `funcTwo` we're, first _awaiting_ the myPromise promise. With the `await` keyword, we pause the execution of the function until the promise has resolved (or rejected). Then, we log the awaited value of `res` (since the promise itself returns a promise). This logs `Promise!`.

The next line is the _asynchronous_ `setTimeout` function, from which the callback is sent to the Web API.

We get to the last line of `funcTwo`, which logs `Last line!` to the console. Now, since `funcTwo` popped off the call stack, the call stack is empty. The callbacks waiting in the queue (`() => console.log("Timeout!")` from `funcOne`, and `() => console.log("Timeout!")` from `funcTwo`) get added to the call stack one by one. The first callback logs `Timeout!`, and gets popped off the stack. Then, the second callback logs `Timeout!`, and gets popped off the stack. This logs `Last line! Promise! Promise! Last line! Timeout! Timeout!`

</p>
</details>

---

###### 134. How can we invoke `sum` in `sum.js` from `index.js?`

```javascript
// sum.js
export default function sum(x) {
  return x + x;
}

// index.js
import * as sum from './sum';
```

- A: `sum(4)`
- B: `sum.sum(4)`
- C: `sum.default(4)`
- D: Default aren't imported with `*`, only named exports

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With the asterisk `*`, we import all exported values from that file, both default and named. If we had the following file:

```javascript
// info.js
export const name = 'Jhone';
export const age = 21;
export default 'I love JavaScript';

// index.js
import * as info from './info';
console.log(info);
```

The following would get logged:

```javascript
{
  default: "I love JavaScript",
  name: "Jhone",
  age: 21
}
```

For the `sum` example, it means that the imported value `sum` looks like this:

```javascript
{ default: function sum(x) { return x + x } }
```

We can invoke this function, by calling `sum.default`

</p>
</details>

---

###### 135. What's the output?

```javascript
const handler = {
  set: () => console.log('Added a new property!'),
  get: () => console.log('Accessed a property!'),
};

const person = new Proxy({}, handler);

person.name = 'Jhone';
person.name;
```

- A: `Added a new property!`
- B: `Accessed a property!`
- C: `Added a new property!` `Accessed a property!`
- D: Nothing gets logged

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

With a Proxy object, we can add custom behavior to an object that we pass to it as the second argument. In this case, we pass the `handler` object which contained to properties: `set` and `get`. `set` gets invoked whenever we _set_ property values, `get` gets invoked whenever we _get_ (access) property values.

The first argument is an empty object `{}`, which is the value of `person`. To this object, the custom behavior specified in the `handler` object gets added. If we add a property to the `person` object, `set` will get invoked. If we access a property on the `person` object, `get` gets invoked.

First, we added a new property `name` to the proxy object (`person.name = "Jhone"`). `set` gets invoked, and logs `"Added a new property!"`.

Then, we access a property value on the proxy object, the `get` property on the handler object got invoked. `"Accessed a property!"` gets logged.

</p>
</details>

---

###### 136. Which of the following will modify the `person` object?

```javascript
const person = { name: 'Jhone Hallie' };

Object.seal(person);
```

- A: `person.name = "Evan Bacon"`
- B: `person.age = 21`
- C: `delete person.name`
- D: `Object.assign(person, { age: 21 })`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

With `Object.seal` we can prevent new properies from being _added_, or existing properties to be _removed_.

However, you can still modify the value of existing properties.

</p>
</details>

---

###### 137. Which of the following will modify the `person` object?

```javascript
const person = {
  name: 'Jhone Hallie',
  address: {
    street: '100 Main St',
  },
};

Object.freeze(person);
```

- A: `person.name = "Evan Bacon"`
- B: `delete person.address`
- C: `person.address.street = "101 Main St"`
- D: `person.pet = { name: "Mara" }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `Object.freeze` method _freezes_ an object. No properties can be added, modified, or removed.

However, it only _shallowly_ freezes the object, meaning that only _direct_ properties on the object are frozen. If the property is another object, like `address` in this case, the properties on that object aren't frozen, and can be modified.

</p>
</details>

---

###### 138. What's the output?

```javascript
const add = x => x + x;

function myFunc(num = 2, value = add(num)) {
  console.log(num, value);
}

myFunc();
myFunc(3);
```

- A: `2` `4` and `3` `6`
- B: `2` `NaN` and `3` `NaN`
- C: `2` `Error` and `3` `6`
- D: `2` `4` and `3` `Error`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

First, we invoked `myFunc()` without passing any arguments. Since we didn't pass arguments, `num` and `value` got their default values: num is `2`, and `value` the returned value of the function `add`. To the `add` function, we pass `num` as an argument, which had the value of `2`. `add` returns `4`, which is the value of `value`.

Then, we invoked `myFunc(3)` and passed the value `3` as the value for the argument `num`. We didn't pass an argument for `value`. Since we didn't pass a value for the `value` argument, it got the default value: the returned value of the `add` function. To `add`, we pass `num`, which has the value of `3`. `add` returns `6`, which is the value of `value`.

</p>
</details>

---

###### 139. What's the output?

```javascript
class Counter {
  #number = 10

  increment() {
    this.#number++
  }

  getNum() {
    return this.#number
  }
}

const counter = new Counter()
counter.increment()

console.log(counter.#number)
```

- A: `10`
- B: `11`
- C: `undefined`
- D: `SyntaxError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

In ES2020, we can add private variables in classes by using the `#`. We cannot access these variables outside of the class. When we try to log `counter.#number`, a SyntaxError gets thrown: we cannot acccess it outside the `Counter` class!

</p>
</details>

---

###### 140. What's missing?

```javascript
const teams = [
  { name: 'Team 1', members: ['Paul', 'Lisa'] },
  { name: 'Team 2', members: ['Laura', 'Tim'] },
];

function* getMembers(members) {
  for (let i = 0; i < members.length; i++) {
    yield members[i];
  }
}

function* getTeams(teams) {
  for (let i = 0; i < teams.length; i++) {
    // ✨ SOMETHING IS MISSING HERE ✨
  }
}

const obj = getTeams(teams);
obj.next(); // { value: "Paul", done: false }
obj.next(); // { value: "Lisa", done: false }
```

- A: `yield getMembers(teams[i].members)`
- B: `yield* getMembers(teams[i].members)`
- C: `return getMembers(teams[i].members)`
- D: `return yield getMembers(teams[i].members)`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

In order to iterate over the `members` in each element in the `teams` array, we need to pass `teams[i].members` to the `getMembers` generator function. The generator function returns a generator object. In order to iterate over each element in this generator object, we need to use `yield*`.

If we would've written `yield`, `return yield`, or `return`, the entire generator function would've gotten returned the first time we called the `next` method.

</p>
</details>

---

###### 141. What's the output?

```javascript
const person = {
  name: 'Jhone Hallie',
  hobbies: ['coding'],
};

function addHobby(hobby, hobbies = person.hobbies) {
  hobbies.push(hobby);
  return hobbies;
}

addHobby('running', []);
addHobby('dancing');
addHobby('baking', person.hobbies);

console.log(person.hobbies);
```

- A: `["coding"]`
- B: `["coding", "dancing"]`
- C: `["coding", "dancing", "baking"]`
- D: `["coding", "running", "dancing", "baking"]`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `addHobby` function receives two arguments, `hobby` and `hobbies` with the default value of the `hobbies` array on the `person` object.

First, we invoke the `addHobby` function, and pass `"running"` as the value for `hobby` and an empty array as the value for `hobbies`. Since we pass an empty array as the value for `y`, `"running"` gets added to this empty array.

Then, we invoke the `addHobby` function, and pass `"dancing"` as the value for `hobby`. We didn't pass a value for `hobbies`, so it gets the default value, the `hobbies` property on the `person` object. We push the hobby `dancing` to the `person.hobbies` array.

Last, we invoke the `addHobby` function, and pass `"baking"` as the value for `hobby`, and the `person.hobbies` array as the value for `hobbies`. We push the hobby `baking` to the `person.hobbies` array.

After pushing `dancing` and `baking`, the value of `person.hobbies` is `["coding", "dancing", "baking"]`

</p>
</details>

---

###### 142. What's the output?

```javascript
class Bird {
  constructor() {
    console.log("I'm a bird. 🦢");
  }
}

class Flamingo extends Bird {
  constructor() {
    console.log("I'm pink. 🌸");
    super();
  }
}

const pet = new Flamingo();
```

- A: `I'm pink. 🌸`
- B: `I'm pink. 🌸` `I'm a bird. 🦢`
- C: `I'm a bird. 🦢` `I'm pink. 🌸`
- D: Nothing, we didn't call any method

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

We create the variable `pet` which is an instance of the `Flamingo` class. When we instantiate this instance, the `constructor` on `Flamingo` gets called. First, `"I'm pink. 🌸"` gets logged, after which we call `super()`. `super()` calls the constructor of the parent class, `Bird`. The constructor in `Bird` gets called, and logs `"I'm a bird. 🦢"`.

</p>
</details>

---

###### 143. Which of the options result(s) in an error?

```javascript
const emojis = ['🎄', '🎅🏼', '🎁', '⭐'];

/* 1 */ emojis.push('🦌');
/* 2 */ emojis.splice(0, 2);
/* 3 */ emojis = [...emojis, '🥂'];
/* 4 */ emojis.length = 0;
```

- A: 1
- B: 1 and 2
- C: 3 and 4
- D: 3

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `const` keyword simply means we cannot _redeclare_ the value of that variable, it's _read-only_. However, the value itself isn't immutable. The properties on the `emojis` array can be modified, for example by pushing new values, splicing them, or setting the length of the array to 0.

</p>
</details>

---

###### 144. What do we need to add to the `person` object to get `["Jhone Hallie", 21]` as the output of `[...person]`?

```javascript
const person = {
  name: "Jhone Hallie",
  age: 21
}

[...person] // ["Jhone Hallie", 21]
```

- A: Nothing, object are iterable by default
- B: `*[Symbol.iterator]() { for (let x in this) yield* this[x] }`
- C: `*[Symbol.iterator]() { yield* Object.values(this) }`
- D: `*[Symbol.iterator]() { for (let x in this) yield this }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

Objects aren't iterable by default. An iterable is an iterable if the iterator protocol is present. We can add this manually by adding the iterator symbol `[Symbol.iterator]`, which has to return a generator object, for example by making it a generator function `*[Symbol.iterator]() {}`. This generator function has to yield the `Object.values` of the `person` object if we want it to return the array `["Jhone Hallie", 21]`: `yield* Object.values(this)`.

</p>
</details>

---

###### 145. What's the output?

```javascript
let count = 0;
const nums = [0, 1, 2, 3];

nums.forEach(num => {
	if (num) count += 1
})

console.log(count)
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `if` condition within the `forEach` loop checks whether the value of `num` is truthy or falsy. Since the first number in the `nums` array is `0`, a falsy value, the `if` statement's code block won't be executed. `count` only gets incremented for the other 3 numbers in the `nums` array, `1`, `2` and `3`. Since `count` gets incremented by `1` 3 times, the value of `count` is `3`.

</p>
</details>

---

###### 146. What's the output?

```javascript
function getFruit(fruits) {
	console.log(fruits?.[1]?.[1])
}

getFruit([['🍊', '🍌'], ['🍍']])
getFruit()
getFruit([['🍍'], ['🍊', '🍌']])
```

- A: `null`, `undefined`, 🍌
- B: `[]`, `null`, 🍌
- C: `[]`, `[]`, 🍌
- D: `undefined`, `undefined`, 🍌

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `?` allows us to optionally access deeper nested properties within objects. We're trying to log the item on index `1` within the subarray that's on index `1` of the `fruits` array. If the subarray on index `1` in the `fruits` array doesn't exist, it'll simply return `undefined`. If the subarray on index `1` in the `fruits` array exists, but this subarray doesn't have an item on its `1` index, it'll also return `undefined`. 

First, we're trying to log the second item in the `['🍍']` subarray of `[['🍊', '🍌'], ['🍍']]`. This subarray only contains one item, which means there is no item on index `1`, and returns `undefined`.

Then, we're invoking the `getFruits` function without passing a value as an argument, which means that `fruits` has a value of `undefined` by default. Since we're conditionally chaining the item on index `1` of`fruits`, it returns `undefined` since this item on index `1` does not exist. 

Lastly, we're trying to log the second item in the `['🍊', '🍌']` subarray of `['🍍'], ['🍊', '🍌']`. The item on index `1` within this subarray is `🍌`, which gets logged.

</p>
</details>

---

###### 147. What's the output?

```javascript
class Calc {
	constructor() {
		this.count = 0 
	}

	increase() {
		this.count ++
	}
}

const calc = new Calc()
new Calc().increase()

console.log(calc.count)
```

- A: `0`
- B: `1`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

We set the variable `calc` equal to a new instance of the `Calc` class. Then, we instantiate a new instance of `Calc`, and invoke the `increase` method on this instance. Since the count property is within the constructor of the `Calc` class, the count property is not shared on the prototype of `Calc`. This means that the value of count has not been updated for the instance calc points to, count is still `0`.

</p>
</details>

---

###### 148. What's the output?

```javascript
const user = {
	email: "e@mail.com",
	password: "12345"
}

const updateUser = ({ email, password }) => {
	if (email) {
		Object.assign(user, { email })
	}

	if (password) {
		user.password = password
	}

	return user
}

const updatedUser = updateUser({ email: "new@email.com" })

console.log(updatedUser === user)
```

- A: `false`
- B: `true`
- C: `TypeError`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The `updateUser` function updates the values of the `email` and `password` properties on user, if their values are passed to the function, after which the function returns the `user` object. The returned value of the `updateUser` function is the `user` object, which means that the value of updatedUser is a reference to the same `user` object that `user` points to. `updatedUser === user` equals `true`.

</p>
</details>

---

###### 149. What's the output?

```javascript
const fruit = ['🍌', '🍊', '🍎']

fruit.slice(0, 1)
fruit.splice(0, 1)
fruit.unshift('🍇')

console.log(fruit)
```

- A: `['🍌', '🍊', '🍎']`
- B: `['🍊', '🍎']`
- C: `['🍇', '🍊', '🍎']`
- D: `['🍇', '🍌', '🍊', '🍎']`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

First, we invoke the `slice` method on the fruit array. The slice method does not modify the original array, but returns the value that it sliced off the array: the banana emoji.
Then, we invoke the `splice` method on the fruit array. The splice method does modify the original array, which means that the fruit array now consists of `['🍊', '🍎']`.
At last, we invoke the `unshift` method on the `fruit` array, which modifies the original array by adding the provided value, ‘🍇’ in this case,  as the first element in the array.  The fruit array now consists of `['🍇', '🍊', '🍎']`.

</p>
</details>

---

###### 150. What's the output?

```javascript
const animals = {};
let dog = { emoji: '🐶' }
let cat = { emoji: '🐈' }

animals[dog] = { ...dog, name: "Mara" }
animals[cat] = { ...cat, name: "Sara" }

console.log(animals[dog])
```

- A: `{ emoji: "🐶", name: "Mara" }`
- B: `{ emoji: "🐈", name: "Sara" }`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

Object keys are converted to strings. 

Since the value of  `dog` is an object,  `animals[dog]` actually means that we’re creating a new property called `"object Object"` equal to the new object. `animals["object Object"]` is now equal to `{ emoji: "🐶", name: "Mara"}`.

`cat` is also an object, which means that `animals[cat]` actually means that we’re overwriting the value of  `animals[``"``object Object``"``]` with the new cat properties. 

Logging `animals[dog]`, or actually `animals["object Object"]` since converting the `dog` object to a string results `"object Object"`, returns the `{ emoji: "🐈", name: "Sara" }`.

</p>
</details>

---

###### 151. What's the output?

```javascript
const user = {
	email: "my@email.com",
	updateEmail: email => {
		this.email = email
	}
}

user.updateEmail("new@email.com")
console.log(user.email)
```

- A: `my@email.com`
- B: `new@email.com`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: A

The `updateEmail` function is an arrow function, and is not bound to the `user` object. This means that the `this` keyword is not referring to the `user` object, but refers to  the global scope in this case. The value of `email` within the `user` object does not get updated. When logging the value of `user.email`, the original value of `my@email.com` gets returned. 

</p>
</details>

---

###### 152. What's the output?

```javascript
const promise1 = Promise.resolve('First')
const promise2 = Promise.resolve('Second')
const promise3 = Promise.reject('Third')
const promise4 = Promise.resolve('Fourth')

const runPromises = async () => {
	const res1 = await Promise.all([promise1, promise2])
	const res2  = await Promise.all([promise3, promise4])
	return [res1, res2]
}

runPromises()
	.then(res => console.log(res))
	.catch(err => console.log(err))
```

- A: `[['First', 'Second'], ['Fourth']]`
- B: `[['First', 'Second'], ['Third', 'Fourth']]`
- C: `[['First', 'Second']]`
- D: `'Third'`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: D

The `Promise.all` method runs the passed promises in parallel. If one promise fails, the `Promise.all` method _rejects_ with the value of the rejected promise. In this case, `promise3` rejected with the value `"Third"`. We’re catching the rejected value in the chained `catch` method on the `runPromises` invocation to catch any errors  within the `runPromises` function. Only `"Third"` gets logged, since `promise3` rejected with this value.

</p>
</details>

---

###### 153. What should the value of `method` be to log `{ name: "Jhone", age: 22 }`? 

```javascript
const keys = ["name", "age"]
const values = ["Jhone", 22]

const method = /* ?? */
Object[method](keys.map((_, i) => {
	return [keys[i], values[i]]
})) // { name: "Jhone", age: 22 }
```

- A: `entries`
- B: `values`
- C: `fromEntries`
- D: `forEach`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The `fromEntries` method turns a 2d array into an object. The first element in each subarray will be the key, and the second element in each subarray will be the value. In this case, we’re mapping over the `keys` array, which returns an array which first element is the item on the key array on the current index, and the second element is the item of the values array on the current index. 

This creates an array of subarrays containing the correct keys and values, which results in `{ name: "Jhone", age: 22 }`

</p>
</details>

---

###### 154. What's the output?

```javascript
const createMember = ({ email, address = {}}) => {
	const validEmail = /.+\@.+\..+/.test(email)
	if (!validEmail) throw new Error("Valid email pls")

	return {
		email,
		address: address ? address : null
	}
}

const member = createMember({ email: "my@email.com" })
console.log(member)
```

- A: `{ email: "my@email.com", address: null }`
- B: `{ email: "my@email.com" }`
- C: `{ email: "my@email.com", address: {} }`
- D: `{ email: "my@email.com", address: undefined }`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: C

The default value of `address` is an empty object `{}`. When we set the variable `member` equal to the object returned by the `createMember` function, we didn't pass a value for address, which means that the value of address is the default empty object `{}`. An empty object is a truthy value, which means that the condition of the `address ? address : null` conditional returns `true`. The value of address is the empty object `{}`.

</p>
</details>

---

###### 155. What's the output?

```javascript
let randomValue = { name: "Jhone" }
randomValue = 23

if (!typeof randomValue === "string") {
	console.log("It's not a string!")
} else {
	console.log("Yay it's a string!")
}
```

- A: `It's not a string!`
- B: `Yay it's a string!`
- C: `TypeError`
- D: `undefined`

<details><summary><b>Answer</b></summary>
<p>

#### Answer: B

The condition within the `if` statement checks whether the value of `!typeof randomValue` is equal to `"string"`. The `!` operator converts the value to a boolean value. If the value is truthy, the returned value will be `false`, if the value is falsy, the returned value will be `true`. In this case, the returned value of `typeof randomValue` is the truthy value `"number"`, meaning that the value of `!typeof randomValue` is the boolean value `false`.

`!typeof randomValue === "string"` always returns false, since we're actually checking `false === "string"`. Since the condition returned `false`, the code block of the `else` statement gets run, and `Yay it's a string!` gets logged.

</p>
</details>

---

### Q. How to do Javascript file size and extension validation before upload?

```html
<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-type" content="text/html;charset=UTF-8" />
    <title>Show File Data</title>
    <script type="text/javascript">
      function showFileSize() {
        var input, file, extension;

        // (Can't use `typeof FileReader === "function"` because apparently
        // it comes back as "object" on some browsers. So just see if it's there
        // at all.)
        if (!window.FileReader) {
          bodyAppend("p", "The file API isn't supported on this browser yet.");
          return;
        }

        input = document.getElementById("fileinput");
        if (!input) {
          bodyAppend("p", "Um, couldn't find the fileinput element.");
        } else if (!input.files) {
          bodyAppend(
            "p",
            "This browser doesn't seem to support the `files` property of file inputs."
          );
        } else if (!input.files[0]) {
          bodyAppend("p", "Please select a file before clicking 'Load'");
        } else {
          file = input.files[0];
          extension = file.name.substring(file.name.lastIndexOf(".") + 1);
          bodyAppend(
            "p",
            "File Name: " +
              file.name +
              "<br/>File Size: " +
              file.size +
              " bytes <br/>File Extension: " +
              extension
          );
        }
      }

      function bodyAppend(tagName, innerHTML) {
        var elm;

        elm = document.createElement(tagName);
        elm.innerHTML = innerHTML;
        document.body.appendChild(elm);
      }
    </script>
  </head>
  <body>
    <form action="#" onsubmit="return false;">
      <input type="file" id="fileinput" />
      <input
        type="button"
        id="btnLoad"
        value="Load"
        onclick="showFileSize();"
      />
    </form>
  </body>
</html>
```

---

### Q. How to create captcha using javascript?

```html
<!DOCTYPE html>
<html>
  <head>
    <title>JavaScript Captcha Example</title>
  </head>
  <script>
    var captcha;

    function generateCaptcha() {
      var a = Math.floor(Math.random() * 10);
      var b = Math.floor(Math.random() * 10);
      var c = Math.floor(Math.random() * 10);
      var d = Math.floor(Math.random() * 10);

      captcha = a.toString() + b.toString() + c.toString() + d.toString();
      document.getElementById("captcha").value = captcha;
    }

    function check() {
      var input = document.getElementById("inputText").value;

      if (input == captcha) {
        alert("Valid Captcha");
      } else {
        alert("Invalid Captcha");
      }
    }
  </script>
  <body onload="generateCaptcha()">
    <input type="text" id="captcha" disabled /><br /><br />
    <input type="text" id="inputText" /><br /><br />
    <button onclick="generateCaptcha()">Refresh</button>
    <button onclick="check()">Submit</button>
  </body>
</html>
```

---

### Q. Create a Stopwatch program in javascript.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Stopwatch Example</title>
  </head>
  <body>
    <form action="" method="post">
      <h4>Simple stopwatch made in JavaScript</h4>
      <input type="button" onclick="startWatch()" value="START" />
      <input type="button" onclick="stopWatch()" value="STOP" />
      <input type="button" onclick="resetWatch()" value="ZERO" />
    </form>
    <p id="res">
      <span id="min">0</span> : <span id="sec">00</span> :
      <span id="msec">000</span>
    </p>
    <p>
      In this example Date() methods co-operate with timing function
      setInterval().
    </p>

    <script type="text/javascript">
      var timer = null;
      var min_txt = document.getElementById("min");
      var min = Number(min_txt.innerHTML);
      var sec_txt = document.getElementById("sec");
      var sec = Number(sec_txt.innerHTML);
      var msec_txt = document.getElementById("msec");
      var msec = Number(msec_txt.innerHTML);
      function stopTimeMilliseconds(timer) {
        if (timer) {
          clearInterval(timer);
          return timer;
        } else return timer;
      }
      function startTimeMilliseconds() {
        var currDate = new Date();
        return currDate.getTime();
      }
      function getElapsedTimeMilliseconds(startMilliseconds) {
        if (startMilliseconds > 0) {
          var currDate = new Date();
          elapsedMilliseconds = currDate.getTime() - startMilliseconds;
          return elapsedMilliseconds;
        } else {
          return (elapsedMilliseconds = 0);
        }
      }
      function startWatch() {
        // START TIMER
        timer = stopTimeMilliseconds(timer);
        var startMilliseconds = startTimeMilliseconds();
        timer = setInterval(function () {
          var elapsedMilliseconds = getElapsedTimeMilliseconds(
            startMilliseconds
          );
          if (msec < 10) {
            msec_txt.innerHTML = "00" + msec;
          } else if (msec < 100) {
            msec_txt.innerHTML = "0" + msec;
          } else {
            msec_txt.innerHTML = msec;
          }
          if (sec < 10) {
            sec_txt.innerHTML = "0" + sec;
          } else {
            sec_txt.innerHTML = sec;
          }
          min_txt.innerHTML = min;
          msec = elapsedMilliseconds;
          if (min >= 59 && sec >= 59 && msec > 900) {
            timer = stopTimeMilliseconds(timer);
            return true;
          }
          if (sec > 59) {
            sec = 0;
            min++;
          }
          if (msec > 999) {
            msec = 0;
            sec++;
            startWatch();
          }
        }, 10);
      }
      function stopWatch() {
        // STOP TIMER
        timer = stopTimeMilliseconds(timer);
        return true;
      }
      function resetWatch() {
        // REZERO TIMER
        timer = stopTimeMilliseconds(timer);
        msec_txt.innerHTML = "000";
        msec = 0;
        sec_txt.innerHTML = "00";
        sec = 0;
        min_txt.innerHTML = "0";
        min = 0;
        return true;
      }
    </script>
  </body>
</html>
```

---
