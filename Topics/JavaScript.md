# JavaScript<!-- omit in toc -->

JavaScript is an interpreted programming language and it is dynamically typed.

## Table of contents<!-- omit in toc -->

- [Introduction](#introduction)
- [Hello world](#hello-world)
- [Variables](#variables)
- [Constants](#constants)
- [Comments](#comments)
- [Data types](#data-types)
  - [Value types](#value-types)
  - [Reference types](#reference-types)
- [Boolean properties, logic, and loops](#boolean-properties-logic-and-loops)
  - [Comparison operators](#comparison-operators)
  - [Logical operators](#logical-operators)
  - [Equality and strict equality](#equality-and-strict-equality)
  - [If/else statements](#ifelse-statements)
  - [For loops](#for-loops)
  - [While loops](#while-loops)
  - [Break keyword](#break-keyword)
- [Functions](#functions)
  - [Arrow functions](#arrow-functions)
    - [Implicit returns](#implicit-returns)
    - [This keyword behavior](#this-keyword-behavior)
- [Arrays](#arrays)
- [Objects](#objects)
- [Spread operator](#spread-operator)
- [Rest operator](#rest-operator)
- [Destructuring](#destructuring)
  - [Destructuring arrays](#destructuring-arrays)
  - [Destructuring objects](#destructuring-objects)

## Introduction

There is no "official" JavaScript release, all features are individually implemented and supported by different browsers.

To execute a `.js` file, a web browser is required; import the script file within an html script tag and specify the path. To execute the code outside a browser, use a runtime environment such as [Node.js](https://nodejs.org).

## Hello world

Program output is sent to the web browser's console:

File: `hello_world.js`

Code:

```js
console.log("Hello world!");
```

You can highlight errors in the console:

```js
console.error("An error has occurred!");
```

## Variables

JavaScript variables are declared with the `let` keyword.

Variable names can contain only letters, numbers, and `_` or `$` symbols. The variable name must begin with a letter.

By convention, variables names are written in `camelCase`.

Example:

```js
let userName = "Player1";
```

Note: declaring variables with the `var` keyword has not been deprecated but its older and arguably less common. The differences of using either declaration are in the scope of the variable.

```js
var score = 100;
```

## Constants

Constants are declared with the `const` keyword:

```js
const daysInWeek = 7;
```

## Comments

Single line comments:

```JavaScript
// Single line comment
```

Multi-line comments:

```js
/* This
is
a
multi-line
comment */
```

## Data types

JavaScript has dynamic typing.

### Value types

Primitive data types are value types. The most commonly used types are:

- Number
- String
- Boolean
- Null
- Undefined

The `typeof` operator can be used to determine the type of its argument and it will always be returned as a string.

```js
typeof 0; // "number"
typeof false; // "boolean"
typeof "abc" === "string"; // true
```

### Reference types

Arrays, functions, and objects are reference types.

Note: we can use `const` when declaring reference types to avoid changing the type but still modify the content.

## Boolean properties, logic, and loops

### Comparison operators

Javascript supports all the standard comparison operations (`==`, `!=`, `<`, `>`, `<=`, `>=`).

### Logical operators

Boolean expressions can be written with the logical operators (`&&`, `||`, `!`).

### Equality and strict equality

You can check the equality of values using the equality operator `==`.

```js
3 == 3; // true
1 != 1; // false
```

Note: determine equality can entail type coercion:

```js
5 == "5"; // true
```

To avoid type coercion, use the strict equality operator `===`:

```js
5 === "5"; // false
5 !== "5"; // true
```

Some non-boolean values can return `false` when performing boolean operations, these include:

- 0 (the number zero)
- "" (an empty string)
- null
- undefined
- NaN (not a number)

All other values return true.

```js
// true expression
if (2) {
  // code here executes
}

// false expression
if ("") {
  // code here does not execute
}
```

### If/else statements

If/else syntax example:

```js
if (2 == 3) {
  console.log("unexpected!");
} else if (3 == 3) {
  console.log("expected");
} else {
  console.log("what now?");
}
```

### For loops

For loop syntax:

```js
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

Use for..of loops to iterate over arrays (or any iterable object).

For-in loop syntax:

```js
for (key in object) {
  console.log(key);
}
```

Use a for..in loop to iterate over the keys in an object.

For-in loop syntax:

```js
for (thing in iterable) {
  console.log(thing);
}
```

### While loops

While loop syntax:

```js
let i = 0;
while (i < 10) {
  console.log(i);
  i++;
}
```

Do-while loop syntax:

```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 10);
```

### Break keyword

Use `break;` to end execution of for or while loops.

## Functions

Functions are declared with the function keyword:

```js
function greet(){
  console.log(“hello”);
}
```

You can specify parameter names in the function declaration.

```js
function greetPerson(name) {
  console.log(`hello ${name}!`);
}
```

You can also specify default values:

```js
function greetPerson(name = "friend") {
  console.log(`hello ${name}!`);
}
```

### Arrow functions

Arrow functions work slightly different to regular functions. Arrow functions can be defined without using the `function` keyword.

Arrow function syntax example:

```js
// Standard function
const square = function (x) {
  return x * x;
};

// Arrow function
const square = (x) => {
  return x * x;
};
```

When the arrow function has a single parameter, the parentheses can be omitted.

```js
const square = (x) => {
  return x * x;
};
```

#### Implicit returns

Arrow functions that return a single expression can omit the return keyword, the expression must use parentheses instead of curly braces.

```js
const square = x => (
  x * x;
)
```

If the expression can fit on the same line, you can omit the parentheses.

```js
const square = (x) => x * x;
```

#### This keyword behavior

Arrow functions establish the `this` keyword based on the scope the arrow function is defined within.

## Arrays

Arrays are reference types, they can be of the same type or non-homogenous.

```js
const colors = ["green", "orange", "purple"];

const listOfStuff = [4, "tree", false, null];
```

## Objects

Objects are also reference types.

In JavaScript, objects are a collection of properties that are denoted by key-value pairs.

Example user object:

```js
const player = {
  userName: "jane21",
  highScore: 150,
};
```

Object key names are stored as strings;

```js
const person = {
  name: "ben",
  "last name": "smith",
};

person.name; // returns "ben"
person["name"]; // returns "ben"
person["last name"]; // returns "smith"
```

You can modify or even add additional properties to objects after they have been initialized.

```js
const tvChannels = {
  1: "tv guide"
  2: "local news"
}

tvChannels.3 = "sports"
```

## Spread operator

The spread operator `...` lets you expand arrays, or any iterable object, as well as key-value pairs.

Array example:

```js
let fruits = ["apple", "orange"];
let treats = ["cookies", "candy"];

let allSnacks = [...fruits, ...treats];
// allSnacks = ["apple", "orange", "cookies", "candy"]
```

Object example:

```js
let janesPC = {
  cpu: "quad core",
  gpu: "none",
  ram: "8gb",
  storage: "2tb",
};

let janesUpgradedPC = {
  ...janesPC,
  gpu: "8gb graphics card",
  ram: "32gb",
};
```

## Rest operator

The rest operator `...` lets you collect function arguments into a single array.

Example:

```js
function addAll(...numbers) {
  return numbers.reduce((total, currentVal) => {
    return total + currentVal;
  });
}

const result = addAll(2, 10, 1, 4);
// result = 17
```

## Destructuring

Destructuring is extracting, or unpacking, certain data.

### Destructuring arrays

When you destructure an array, you extract values from the array into distinct variables.

```js
const toDoList ["withdraw cash", "visit farmers market", "buy ingredients", "cook dinner"];

const [firstTask] = toDoList;
const [first, second, , fourth] = toDoList;
const [firstToDo, ...remainingTasks] = toDoList;
```

### Destructuring objects

When you destructure an object, you extract properties from the object into distinct variables.

```js
const pet = {
  kind: "dog",
  name: "Fido",
  color: "black",
};

const { name, color } = pet;
const { name: petName, color: petColor } = pet;
const { name, ...other } = pet;
```
