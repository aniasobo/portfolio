# Week five 24-30.06.2019

## Goals:

- [x] Test drive a simple front-end web app with Javascript
- [x] Follow an effective process for learning a new language

---

## Practice

Date | Project | progress
--- | --- | ---
25.06 | [FizzBuzz in JS](https://github.com/aniasobo/fizzbuzzjs) | completed
26.06 | [Airport App in JS](https://github.com/aniasobo/Airport-JS) | part done
26-28.06 | [Thermostat](https://github.com/aniasobo/thermostat) | [part done](https://github.com/aniasobo/portfolio/blob/master/challenges/thermostat.md)
29-30.06 | [Bowling](https://github.com/aniasobo/bowling-challenge) | [progress note](https://github.com/aniasobo/portfolio/blob/master/challenges/bowling.md)


## Code review:

- Rakefile should be used for db setup/destruction (when DataMapper or another ORM is not being used??)

```
# in Rakefile:

task :setup do
  # Set up development and test databases
end

task :teardown do
  # Destroy development and test databases
end

task :seed do
  # Add some dummy data to the development database
end
```

- The Rakefile (automation tool) makes it simpler to run common tasks where your code runs remotely. For instance: as part of deployment to Heroku and Continuous Integration ('CI'). tasks can be scheduled to run automatically (db clears, migrations etc); define executable commands for command line
- to fix the Travis CI issue that can't execute bundle:

```
before_install:
- sudo apt-get update -qq
- sudo apt-get install -qq postgresql-server-dev-9.3
- gem update --system  # added this line
- gem install bundler  # added this line
```

^ still failed because some tests aren't passing but seems to be executing some stuff correctly - can't find table relations though

---

## Encapsulation in JavaScript workshop

- constructor function vs prototype
- to define methods:

```
SomeShit.prototype.methname = function() {returns something};
```

- private method is denoted by _ before the ._name
- this._count responds to Class but not to instance; define prototype method to send messages to instances


---

## Count app

- exemplar for how to make Ajax requests, test frontend code and separate frontend into model, view, controller

## JS basics:

### Debugging: 

- JavaScript REPL: Chrome console
- using a debugger:

```
function sayHi() {
  debugger;
  console.log("hi!");
};

sayHi();
// open in Sources tab in chrome dev tools
```

- when using debugger, hover over variables to see their values
- looking at the value of 'this' in different parts of the code with 'console.log(this);'
- am I using the correct function? 

```
'console.log(airport.land);'
```

- what is this function returning? 

```
'console.log(airport.land());'
```

- what does this parameter contain? 

```
Airport.prototype.land = function(plane) {
  console.log(plane);
}
```

### Misc:

- boolean methods - isMethod (similar to Ruby methods?)

```
# ruby:
class Dog
  def purebreed?
    true
  end
end

# JS:
Dog.prototype.isPurebreed = function() {
  return true;
}
```

- private methods are prefixed by underscore _myPrivateMethod
- study the [AirBnB JS style guide](https://github.com/airbnb/javascript)
- objects are used like hashes ion Ruby
- dot notation - access stuff inside the object 
- loop with an incremented/counter:

```
for (var i = 0; i < 10; i++) {  
console.log(i)  
}  
```

- functions/methods

```
function example (x) {  // def methodname (arg)  
	return x * 2;         // return statement
}                       // end

```

- [good explainer](https://medium.com/@vvkchandra/essential-javascript-mastering-immediately-invoked-function-expressions-67791338ddc6) on JS immediately invoked function expression, aka IIFE

```
var msg = "Hello, World!";
var sayHi = function() {  // no function name = IIFE
    alert(msg);
};

sayHi();
```

- anonymous function:

```
!function() {   // the ! tells JS that what comes after is
	alert("yo");  // an expression (not a function)
 }();
 
 // alternative syntax:
void function() {
 alert("yo");
}();            // the () is what calls the function!!
```

- this function can only be invoked once
- invoking an anonymous function:

```
(function() {
	alert("yo");
});             // does not get executed
// but these do:
// Variation 1
(function() {
  alert("yo");
}());          // the final () executes the function?
							 // or the () around function? both?

// Variation 2 - preferred
(function() {
	alert("yo");
})();         // the () executes the function...?
```

- parentheses around/outside of the (function) - indicate that it's an expression, NOT a definition 

> Next time whenever you are creating a bunch of variables and functions in global scope that no one uses outside your code, just wrap all of that in an IIFE and get a lot of good JavaScript karma for doing that. Your code will continue to work, but now you are not polluting global scope. Also you are shielding your code from someone who may change your globals accidentally, or sometimes intentionally!

- IIFE with params:

```
(function IIFE(msg, times) {
	for (var i = 1; i <= times; i++) {
	console.log(msg);
	}
}("Hello!", 5));  // args get passed too the IIFE
```

- reusable function that removes specific item from array:

```
function arrayRemove(arr, value) {
  return arr.filter(function(ele){
      return ele != value;
  });
}
```

#### Prototypes vs Constructors in JS:

- prototype is an internal property of all objects
- prototype refers to other objects & contains common attributes and properties of its heirs
- constructor functions can be called with the keyword 'new' to create instances
- [good examples here](https://medium.com/backticks-tildes/javascript-prototypes-ee46810e4866)
- 'Object.create(thing)' is used to create an object that inherits from thing but is not a prototype (& thing is not a function but an object); it's better practice to use prototypical inheritance though, starting with a function with prototype functions used as method creators, then creating heirs with the keyword 'new'

#### Useful libraries of utility functions:

1. Lodash
2. Underscore
3. Ramda (for functional programming)
4. JQuery


### JQuery:

1. download the script or grab one off a CDN. Load it in index.html.

Download:

```
<script src="js/jquery.min.js"></script>
```

CDN:

```
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
```

2. only execute functions when the DOM is loaded:

```
$(document).ready(function() { })
```

this wraps the JQuery document.

3. JQuery selector with an event listener:

```
$('element').on('event', function() {

})

// Or:

$('element').click(function() { })

// also callbacks:

$('#some-heading').click(function() {
  // this function is the callback!
})
```

events can be clicks, scrolls, typing and other forms of interaction within the browser.

4. Set a new object:

```
var thermostat = new Thermostat();
```

5. to DRY out the code:

```
function updateTemperature() {
  $('#h1').text(`Current temperature: ${term._temperature}`);
}

// to call it:

$(document).ready(function() {
  var thermostat = new Thermostat();
  updateTemperature();

  $('#temp-up').click(function() {
    thermostat.increaseTemperature();
    updateTemperature();
  });
  
  function updateTemperature() {
    $('#temperature').text(thermostat.temperature);
  };
});
```

### Closures:

```
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

add5 and add10 are closures - they share the same function body definition but store different lexical environments.

In add5's lexical environment x is 5; in add10's, it's 10.

Closures let you associate some data (ie the lexical environment) with a function that makes an operation on it.

Closure can be used analogously to OO-style Object with only a single method (the add5 object only adds integers to 5).

Closures are useful for event-based functions, such as this one that converts rem/em font sizes to pixel sizes:

```
function makeSizer(size) {
  return function() {
    document.body.style.fontSize = size + 'px';
  };
}

var size12 = makeSizer(12);
var size14 = makeSizer(14);
var size16 = makeSizer(16);

document.getElementById('size-12').onclick = size12;
document.getElementById('size-14').onclick = size14;
document.getElementById('size-16').onclick = size16;
```

One way to make a method private in JS is to put it in a closure.