## What is JS?

JS is a single-threaded, multi-paradigm, high level, dynamically typed, prototypal-inheritence object-oriented, garbage collected and Just-in-time compiled language.

## Programming Paradigm for JS

JS supports both the prototypal-inheritance object oriented and functional programming paradigms.

- #### Functional Programming
  - Functional programming produces programs by composing mathematical functions and avoids shared state & mutable data.
  - #### Why functional Programming?
    - Pure Functions
    - Avoiding Side effects
    - Simple function composition
    - Helpful feature of FP - first class function, Higher Order function, passing function as args/values

## Hoisting and TDZ (Temporal Dead Zone)

[Temporal Dead Zone and Hoisting](https://www.freecodecamp.org/news/javascript-temporal-dead-zone-and-hoisting-explained/)

Hoisting refers to JavaScript giving higher precedence to the declaration of variables, classes, and functions during a program’s execution.

Hoisting makes types of variables accessible/usable in the code before they are actually declared. "Variables are lifted to the top of their scope."

A TDZ is the area of the block where a variable is inaccessible until that variable is completely initialized.

```javascript
test(); // Hello

function test() {
  console.log("Hello");
}
```

### Why it's possible?

JavaScript engine scans the code before executing it and creates a property for each variable or function in the code in variable environment object.
For normal variables, it assigns an undefined value, and for functions it assigns a reference to that function in memory.
That's why we can call a function, but if we try to access a variable, we will get undefined.

```javascript
{
  // bestFood’s TDZ starts here (at the beginning of this block’s local scope)
  // bestFood’s TDZ continues here
  console.log(bestFood); // returns ReferenceError because bestFood’s TDZ continues here
  // bestFood’s TDZ continues here
  let bestFood = "Vegetable Fried Rice"; // bestFood’s TDZ ends here
  // bestFood’s TDZ does not exist here
}
```

```javascript
{
  // TDZ starts here (at the beginning of this block’s local scope)
  // bestFood’s TDZ continues here
  // bestFood’s TDZ continues here
  let bestFood = "Vegetable Fried Rice"; // bestFood’s TDZ ends here
  console.log(bestFood); // returns "Vegetable Fried Rice" because bestFood’s TDZ does not exist here
  // bestFood’s TDZ does not exist here
}
```

```javascript
{
  // TDZ starts here (at the beginning of this block’s local scope)
  // bestFood’s TDZ continues here
  // bestFood’s TDZ continues here
  let bestFood; // bestFood’s TDZ ends here
  console.log(bestFood); // returns undefined because bestFood’s TDZ does not exist here
  bestFood = "Vegetable Fried Rice"; // bestFood’s TDZ does not exist here
  console.log(bestFood); // returns "Vegetable Fried Rice" because bestFood’s TDZ does not exist here
}
```

```javascript
{
  // bestFood’s TDZ starts and ends here
  console.log(bestFood); // returns undefined because bestFood’s TDZ does not exist here
  var bestFood = "Vegetable Fried Rice"; // bestFood’s TDZ does not exist here
  console.log(bestFood); // returns "Vegetable Fried Rice" because bestFood’s TDZ does not exist here
  // bestFood’s TDZ does not exist here
}
```

Similarly for below code,

```javascript
function scope() {
  console.log(var1); // undefined
  console.log(var2); // undefined

  var var1 = "Hello";
  var var2 = "Hi";
}
```

| Syntax                         | Hoisted                               | Initial Value           | Scope    |
| ------------------------------ | ------------------------------------- | ----------------------- | -------- |
| functional declarations        | ✅                                    | actual function         | Block    |
| var variables                  | ✅                                    | undefined               | function |
| let and const variables        | 🚫                                    | `<uninitialized>` / TDZ | Block    |
| function expression and arrows | Depends on if we are using var or let |

### Why Hoisting and TDZ?

- ### Hoisting
  - Using function before actual declaration.
- ### TDZ
  - Makes it easier to avoid and catch errors: accessing var before declaration should be avoided.

```javascript
// Hoisting and TDZ in Practice

// Variables
console.log(me); // undefined Why?? -> variables declared with var are actually hoisted, but they are hoisted to the value of undefined.
console.log(job); // Reference Error -> Why?? Because the job variable is still in temporal dead zone the temporal dead zone of a variable declared with a let or const, starts from the beginning of the current scope and so that's basically here, so in this case, it's the global scope. So from the beginning of the scope until the point of the code where it is defined and so here.
console.log(year); // Reference Error -> year is not defined
var me = "Jonas";
let job = "teacher";
const year = 1991;

// Functions
console.log(addDecl(2, 3));
console.log(addExpr(2, 3)); // We get the error here
// Because the function is now a const variable and so now the addExpr (74) is in the temporal dead zone.
// Here you can see this will return is undefined.
console.log(addArrow);
// Any variable declared with var will be hoisted and set to undefined.
// Here (67) we are trying to call undefined. We are doing the same as undefined(2, 3) in console and get the same error.
// console.log(addArrow(2, 3));
// function declaration
function addDecl(a, b) {
  return a + b;
}
// We are simply assigning a function value to this variable. And since the variable was assigned with const it is now in a temporal dead zone.
// function expression
const addExpr = function (a, b) {
  return a + b;
};

// arrow function
var addArrow = (a, b) => a + b;
// Example
// console.log(undefined);

//It is happening because of hoisting because numProducts value is not 10 but undefined. Since undefined is a falsy value. And the below block will run and thus deleteShoppingCart() function is called. Use const and let all the time and not to use var
if (!numProducts) {
  deleteShoppingCart();
}

var numProducts = 10;
function deleteShoppingCart() {
  console.log("All products deleted!");
}

// Variables declared with let and const donot create properties on the window object.
var x = 1;
let y = 2;
const z = 3;
console.log(x === window.x); // true
console.log(y === window.y); // false
console.log(z === window.z); // false
```

| Syntax    | Description |
| --------- | ----------- |
| Header    | Title       |
| Paragraph | Text        |
