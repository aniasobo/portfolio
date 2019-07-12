# Week 7 08-14.07.2019

## Goals:

- [ ] Build a front-end app in Javascript
- [ ] Work competently in Javascript
- [ ] Reason about asynchronous behaviour in Javascript
- [ ] Write a front-end, single-application app using only pure JS

---

## Practice

Date | Project | progress
--- | --- | ---
08-09.07 | [Notes App](https://github.com/rachjgriff/note-app) | [progress note]()
10-12.07 | [Notes App - Phase 2](https://github.com/aniasobo/notes-app) | [progress note]()



## JS module pattern

Similar to an IIFE but with export code around:

```
(function(exports) {
  var EXCLAMATION_MARK_COUNT = 5

  function exclaim(string) {
    return string + "!".repeat(EXCLAMATION_MARK_COUNT);
  };

  exports.exclaim = exclaim;
})(this);
```

the above module would be used like this:

```
(function(exports) {
  var EXCLAMATION_MARK_COUNT = 5

  function exclaim(string) {
    return string + "!".repeat(EXCLAMATION_MARK_COUNT);
  };

  exports.exclaim = exclaim;
})(this);

// prints "hi!!!!!"
console.log(exclaim("hi"));

// throws a ReferenceError
console.log(EXCLAMATION_MARK_COUNT);
```

The value of `this` in the export code is `window`, the place where all globals are stored.

The variables that don't get included in the exports stay hidden/private.

**in Node.js**

> The values of `this` in the browser (`window`) and `this` in Node.js (`exports`) are different. But they are similar enough that they can both be massaged by this pattern to let us write code that will work in both environments.


[This keyword explainer](https://itnext.io/the-this-keyword-in-javascript-demystified-c389c92de26d)


## Promises tutorial

`try-catch` = equivalent of Ruby `begin-rescue` - not a good way to handle errors; better - using JS promises:

```
$.ajax('file.json').done(function(){
	console.log('success');
	return $.ajax('file2.json')
	
}).done(function(){
	console.log('second success');
	return $.ajax('file3.json');
	
}).done(function(){
	console.log('third success');
	
	}).fail(function(){
	console.error('some error');
});
```


`$.ajax('file.json', {})` - AJAX request

[https://promisesaplus.com](https://promisesaplus.com)  

**keyword `then`**

`then` is the method that denotes that the function is a promise; first argument is the success, second is the fail. Called on a new Promise() object. (does it have to be created each time??)

[Promises: states and fates](https://github.com/domenic/promises-unwrapping/blob/master/docs/states-and-fates.md):  

**The possible states (mutually exclusive):**

1. fulfilled
2. rejected
3. pending  

**The possible fates (mutually exclusive):**

1. resolved
2. unresolved

> A promise's state is reflected in its `[[PromiseState]]` internal slot.

> A promise's fate is stored implicitly as part of its "resolving functions."


### Reading beyond your level practical:

**Steps to understand documentation:**

1. Make a list of concepts that have to be understood first, to make the target concept understandable
2. If those concepts have other concepts that have to be understood first, add those to your list

**Example - keyword `new`**

- sets the context of `this` to the object created
- links the constructor of the object created to its instances
- the defined object's functions won't be accessible without an instance created with `new`

**Example - JS closures**


## JS error handling

in a `try-catch` block, the `catch` takes a parameter which stores the exception/error thrown;
to make a multi-level `try-catch` block, use `try-catch-finally` (also possible to just use `try-finally`); 
with a single `catch`, the `catch` becomes unconditional and it executes when any exception is thrown;   
the caught `exception` is an object with the following (likely) properties:  
.name  
.message  
.stack  

a `try-catch` block with a `catch` for different types of errors:

```
try {
  myroutine(); // may throw three types of exceptions
  testSuccessMessage();
} catch (e if e instanceof TypeError) {
  // statements to handle TypeError exceptions
} catch (e if e instanceof RangeError) {
  // statements to handle RangeError exceptions
} catch (e if e instanceof EvalError) {
  // statements to handle EvalError exceptions
} catch (e) {
  // statements to handle any unspecified exceptions
  logMyErrors(e); // pass exception object to error handler
}
```

same code but ES6:

```
try {
  myroutine(); // may throw three types of exceptions
} catch (e) {
  if (e instanceof TypeError) {
    // statements to handle TypeError exceptions
  } else if (e instanceof RangeError) {
    // statements to handle RangeError exceptions
  } else if (e instanceof EvalError) {
    // statements to handle EvalError exceptions
  } else {
    // statements to handle any unspecified exceptions
    logMyErrors(e); // pass exception object to error handler
  }
}
```

the `finally` clause executes whether or not an exception is thrown!
 
 
## Arrow functions:

```
var funcName = (params) => params + 2
funcName(2);
// 4
```

if only one parameter:

```
var double = num => num * 2
```

syntax:

```
(parameters) => { statements }
```

syntax for no parameters:

```
() => { statements }
```

syntax for a single parameter:

```
parameters => { statements }
```

if only returning an expression, remove the curly bracket:

```
parameters => expression
// is equivalent to:
function (parameters){
  return expression;
}
```

**arrow functions do not bind `this`**

instead, `this` keeps its meaning from the original context (its lexical binding).

example of this. changing context to window:

```
function Counter() {
  this.num = 0;
  this.timer = setInterval(function add() {
    this.num++;
    console.log(this.num);
  }, 1000);
}
```

same function, refactored to work due to keeping the scope of this:

```
function Counter() {
  this.num = 0;
  this.timer = setInterval(() => {
    this.num++;
    console.log(this.num);
  }, 1000);
}
```

[preventDefault() on MDN](https://developer.mozilla.org/en-US/docs/Web/API/Event/preventDefault)
