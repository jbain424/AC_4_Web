# Functions & Scope

## Goals 
* Know how to declare and write a function
* Know some of the key differences between ES5 and ES6 syntax
* Have an understanding of scope. 

## Vocabulary

* Function Definition
* Function Call
* *Function Expression* syntax
* *Function Declaration* syntax
* Global variable scope
* Local variable scope (function scope)

## Lesson

We use functions to store code that we want to re-use. 
Let's pretend we have two arrays: array1 = [1, 2, 3, 4, 5] and array2 = [11, 12, 13, 14, 15]. In previous lessons if we wanted to 
log to the console all the elements in the first array and then all the elements in the second array
we would have to write code that looked something like: 
```js
let array1 = [1, 2, 3, 4, 5] 

for(let i = 0; i < array1.length; i++) {
  console.log(array1[i]
}

let array2 = [11, 12, 13, 14, 15]

for(let i = 0; i < array1.length; i++) {
  console.log(array1[i]
}

```

This doesn't look too bad, but what if we were given another 5 arrays, 10 arrays? 
Pretty soon we would be writing a lot of the same loop.
What about if we didn't know what was going to be in the array? How would we write that? 
In programming we like to keep out code **DRY**. This stands for Don't Repeat Yourself. 
So instead of writing a bunch of loops each time, we can write one function that will loop through any array. That way, 
whenever we are given a new array that we want to log it elements to the console, we can just call our function 
instead of re-writing the same loop. 

![functions](../assets/function_composition.png)

 * The above syntax is called **function expression**. 
The word `function` tells JS that we are **declaring** a function. Just like const lets JS know we are about to declare a variable.

 * squareNumber is the **name** of the function. Not all functions need a name. Some functions are annonymous and don't have a name. But for now, we will be dealing with functions that do have name. 

* Inside the parenthesis are **parameters** which are used to define a function. When we call a function we replace parameters with **arguments**. Arguments are the real values that are passed into a function. Often the words parameters, and arguments are used interchangably. Also, some functions don't require any arguments. For example: 

```js 
  function sayHello() {
    return "Hello"
  }

```

* The opening curly brace, { , indicates the start of the function. The closing curly brace, } , indicates the end of the function. 

* Between the braces, is the code that makes up the function. **return** is the result (what we get back) after we've called the function. If there is no __return__ statement, the function will return `undefined`. 


There are a couple different ways to __declare__ a function. The first way is to simple write `function` like this:

```js
function printArray(arr) {
  for(let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
  }
}
```
This is a function called printArray written in ES5 syntax. It takes in one __argument__ (the array), and then loops through it. 
Now if we wanted to print our arrays as before we could call the function and pass it the array like this: 

``` js
  let array1 = [1, 2, 3, 4, 5];
  let array2 = [11, 12, 13, 14, 15];
  
  printArray(array1);
  printArray(array2);
```
See how much prettier that is? 

To write that same function in ES6 is just a little bit different. First we declare the function like a variable that won't change using the const declaration. 
We then state the name of our function and assign it to our arguments, a fat-arrow, and then curly braces. Like this:

```js 
  const printArray = (arr) => {
    for(let i = 0; i < arr.length; i++) {
      console.log(arr[i]);
    } 
  }

```

Both printArray functions will be treated the same. 

## Invoking a Function
We invoke a function by saying the function's name and passing in any necessary arguments. If we wanted to call our sayHello funtion we would do it as so: `sayHello()`. Because sayHello takes in zero arguments we wrote nothing in between the parenthesis. If we wanted to call printArray we would do it as so: `printArray([1, 2, 3])`. 

If we changed our sayHello to accept an argument it would look like this: 

```js
   function sayHello(name) {
    return "Hello " + name
  }

  sayHello()
```

What do you think would happen if we didn't pass in any arguments into sayHello? 



Let's write a function that doubles a number.

```js
function doubleNumber(num) { 
  return num + num;
}

const doubleNumber2 = (num) => {
  return num + num;
}
```



### Functions as Values

Before we can begin using the above function, we need to store it somewhere. In JavaScript, a function is a value, just like numbers and string, and like other values, it can be assigned to a variable:

```js
var double = function (num) { return num + num }
```

Now that we have store the function into a variable called `double`, we can pass some input into the function and observe the output. We do this by writing the name of the variable to which the function is assigned (`double` in this case), followed by parentheses, in which we write the input for the function.

```js
double(5)
```

The input values we provide to a function are also called **arguments**. When you open a node REPL, write the function definition and call the function as we did above, you will see the output right away.

```js
> var double = function (num) {
... return num + num
... }
> double(5)
10
```

When we write programs, however, we will want to use the output in some way. For example, we may want to log the output.

```js
var double = function (num) {
  return num + num
}

console.log(double(3))
```

Once the `return` statement is reaches inside a function, the function is execution is over, and we return to the point at which we called the function. The code `double(3)` will then be replaced by the value that was returned by the function. As far as `console.log`, what is being passed to it is the value `9`. It knows nothing about `double`.

As you may have realized, `console.log`, is also a function - one that is provided for us. The dot in it's name is meaningful, and will be discussed at a later point. `console.log` differs from out `double` function in two other ways:

1. It does not produce an output.
2. It leads to something else happening - the value passed to it being logged to the screen.

The first part is easy to replicate. All we need to do is write a function without a `return` keyword:

```js
var noReturn = function (num){
  num + num
}
```

The function above takes a number as argument, doubles it, and does nothing with the result. We can test this:

```js
> var result = noReturn(2)
> console.log(result)
undefined
```

In JavaScript, a function that does not have a return statement will return the value `undefined`.

### Side-effects

The second aspect of `console.log` - a value being logged to the screen, is not something we can replicate. However, this is part of a larger aspect of functions called a *side effect*. A *side effect* is anything that happens inside a function which result in changes to the outside world. One side effect that we *can* create is changing the value of a variable that was defined outside the function.

```js
var myNumber = 2
var sideEffect = function(){
  myNumber += 1
}

sideEffect()
console.log(myNumber)
```

The function `sideEffect` above takes no arguments, and has a single side-effect, adding `1` to the value of the variable `myNumber`.

> Ex. Call `sideEffect` multiple times, and then log myNumber. What is the result?
> Ex. Put a call to the `sideEffects` function as an argument to `console.log`: ```js console.log(sideEffects())```. What is logged? Why?
> Ex. Writing a function that produces side effects *and* has a return value.

### Function shorthand syntax

There is a shorter way to write `var dobule = function…`: start with the `function` keyword, followed by the function name.

```js
function double(num){
  return num + 1
}
```


The above syntax is called **function declaration**. `double` is a still a variable in both cases, one whose value is a function.


### Function Hoisting

The only substantial difference is that function declarations are hoisted. This means that you can call a function before it is defined:

```js
console.log(sayHelloDec) // logs: [Function: sayHelloDec]
sayHelloDec(); // logs "hello"

function sayHelloDec() {
  console.log('hello');
}
```

A function defined with the expression syntax will be assigned to a variable, and any variable used before it is defined will have the value `undefined`

```js
console.log(sayHelloExp) // logs: undefined
sayHelloExp(); // TypeError: sayHelloExp is not a function

var sayHelloExp = function() {
  console.log('hello');
}
```

### Functions as Mini-Programs

A function is like a mini-program inside our main program. Whenever the code inside it is done running, we return to the line from which we called the function. A variable defined inside a function will be forgotten when the function is done running. Every time we call the function `logPets` below, the variables will be created anew.

```js
// This function will print 'cat' and then print 'dog'
function logPets(){
  var pet = 'cat'
  console.log(pet)
  pet = 'dog'
  console.log(pet)
}
// logNumbers will do the same thing every time we call it
logPets()
logPets()
```

### Variable Scope

The variables defined inside a function simply do not exist outside of it.

```js
function hello(){
  var greeting = 'hello'
  console.log(greeting)
}

console.log(greeting) // ReferenceError: greeting is not defined
```

Variables declared outside a function are called `global` and they can be accessed and modified from any function.

```js
var greeting = 'hi'

// This function changes the global variable `greeting`
function hello(){
  greeting = 'hello'
  console.log(greeting)
}
hello()

console.log(greeting) // logs: 'hello'
```

A commonly used term for this is **scope**: a variable inside a function has local scope, and a variables not inside any function has global scope. If we create a variable inside a function with the same name as a global variable - the function will only be aware of the local one. This, however, will not change the value of the global variable.

```js
var greeting = 'hello'

function hello(){
  var greeting = 'what\'s up?'
  console.log(greeting) // logs: 'what's up?'
}


console.log(greeting) // logs: 'hello'
```

### Functions in English

One way we often discuss functions is by stating what they do. For example: function `add` adds two numbers and returns the result. When talking of functions this way, it is usually assumed that the variables (in this case the two numbers), will be provided as arguments to the function.

```js
function add(num1, num2){
  return num1 + num2
}

var num1 = 2
var num2 = 3
// adding num1 and num2
var sum = add(num1, num2)

console.log(sum) // logs: 5
```

Note that we are not changing the values of `num1` and `num2`.

> Ex 1. Write a function that takes a number as argument and returns the number to the power of 2

### Calling functions from other functions

We can call functions from other functions, in the same way we would call them from our main code.

```js
// Returns the square of a number
function square(num){
  return num * num
}

// Returns the sum of the squares of two numbers
function addSquares(num1, num2){
  return square(num1) + square(num2)
}

// Adding the squares of 2 and 3
var sum = addSquares(2, 3)

console.log(sum)
```

Be careful when two function call each other. The following code will never stop running:

```js


function chicken(){
    // call egg
    egg()
}

function egg(){
    // call chicken
    chicken()
}

egg()
```

One way to imagine the code above is as a stack of functions calls - each time we call a new function, it gets put on the stack. The function is put out of the stack only when it is done running. In the code above, we keep piling `chicken` and `egg` functions, and never takes them off - until the computer runs out of memory.

## Resources

* [mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
* [Eloquent Javascript - Functions](http://eloquentjavascript.net/03_functions.html)