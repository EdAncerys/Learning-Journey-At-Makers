# Week 5 Goals 

#### By the end of the week all developers can:

- Test drive a simple front-end web app with Javascript
- Follow an effective process for learning a new language

## Daily Goals 
### Monday 04 of May 2020

## Morning Goals 

- Code Review for the weekend challenge.
- Attend week 5 *kick off*. Introduction to **Java Script** work shop. 
- Set a working plan for the new week

##### Plan:

- Review weekend challenge in pair
- Set goals for the new week
  
**Process:** 

Main focuses for this week

- Learn and understand new language - **JS**
- Learn a programming construct by exploring and reasoning about examples.
- Go through weekly practicals.
- understand the rules that govern the behavior of the this keyword.
- Ajax request and response.
- Rewrite fizz buzz and the airport challenge in JS.

### `function` in JavaScript

The `function` keyword in JavaScript creates an object that can be **called**.  (We say _call_ in JavaScript, but that will make for confusing reading since 'call' has lots of meanings in English; let's use _invoke_ instead).

## The anatomy of `function`

In Ruby with _literals_.  These are expressions that directly create a new object whenever they are evaluated:

```ruby
"Ben"  # creates a new String object
[]  # creates a new Array object
{}  # creates a new Hash object
```
The `function` keyword in JavaScript creates a new Function object (i.e. an object that can be invoked):

```javascript
var bark = function() {
  return 'Woof';
}

bark();  //invoking the function will return 'Woof'
```
You must include the parentheses when invoking a function, even if there are no arguments.  Can you reason why?  What is `bark;` on its own with no parentheses?

You can declare arguments in functions, as you would expect:

```javascript
var bark = function(name) {
  return name + ' says Woof';
}

bark('Barney');  //will return 'Barney says Woof'
```
> If you want to return a value from a JavaScript function, you must explicitly use `return`, otherwise it will just return `undefined`.

## `function` is like a block

In Ruby, we can pass a block to another method like so:

```ruby
['one', 'two', 'three'].each do |number|
  puts number
end
```
In JavaScript, we can do a very similar thing by passing an **anonymous function**.

> An **anonymous** function is a function without a name.

```javascript
['one', 'two', 'three'].forEach(function(number) {
  console.log(number);
});
```
But don't allow the syntax to confuse you; what are we actually passing to the `forEach` function?  It's just a Function object.  The following is exactly the same:

```javascript
var callback = function(arg) {
  console.log(arg);
};

['one', 'two', 'three'].forEach(callback);
```
> It's common to refer to this use of a function as a **callback**.

**What I've Learned:**

> As a language, JavaScript is fundamentally different to Ruby

> **Objects.** Most things in JavaScript (other than primitives) are objects.
```
var myObject = {} // you can make empty objects
var myOtherObject = {
                      some: 'stuff',
                      goes: 'in',
                      here: 123,
                      arrays: ['woah', 'check', 'it'],
                      nestedObject: {another: 'object'},
                      functionsToo: function(foo) { return foo }
                    }
```

## Afternoon Challenges  

*Practice pairing and test drive a simple front-end web app with Javascript*  

**Plan:** Pair with Hesam and keep working on the afternoon challenge for the week - *"Thermostat".*

**Process:**

#### Setting up Jasmine and getting started with FizzBuzz in JS

Today's challenge is about setting up Jasmine to test JavaScript and re write our old project 'FizzBuzz' into this new language.

- Jasmine is the testing framework for JS, I downloaded [here](https://github.com/jasmine/jasmine/releases). After download of the latest version in to my Mac do the following:
    - To use Jasmine in your own project we need to create a new directory with the appropriate name, e.g. FizzBuzz and transfer over the lib directory intact.
```
cp -r ~/Downloads/jasmine-standalone-3.5.0/lib .
```
- Now we need to create a test file, and a **JS** file for our code: `spec/FizzbuzzSpec.js` and `src/Fizzbuzz.js`. **Note that spec file goes in to src directory.**

- To finish setting up Jasmine we need to create a file at our root directory `SpecRunner.html` with the following code that links spec and source files:
```html
<!-- include source files here... -->
  <script type="text/javascript" src="src/Fizzbuzz.js"></script>

  <!-- include spec files here... -->
  <script type="text/javascript" src="spec/FizzbuzzSpec.js"></script>
```
#### We are now ready to start testing!

- Main structure for testing in Jasmine/JS: Function {} acts like Ruby's do/end
```javascript
describe('', function() {

//method statements go here

});
```
- Our first test should look something like this:
```javascript
describe('FizzBuzz', function() {

  var fizzbuzz;
  
  beforeEach(function() {
    fizzbuzz = new FizzBuzz();
  });

  describe('multiples of 3', function() {
    it('fizzes for 3', function() {
      expect(fizzbuzz.play(3)).toEqual('Fizz');
    });

  });

});
```
- Let's split it up:
  - We give our described method a name 'FizzBuzz' (like the file we created, something like a class name in ruby)
  - Declare a variable inside the function block. It will be a local variable and it's only available withing the nearest {}. _If not declared it will look in every parent function and if still can't find any it will create it for you in the top level, but it will be a global variable, which is not a good practice_.
```javascript
var fizzbuzz;
```
  - Jasmine has no context blocks but we can open a new `describe` function with an `it`.
  - We then need an instance of FizzBuzz to test against so we create it inside the block: _when we are instantiating our version of the class - we MUST add the `();`_
  ```javascript
   fizzbuzz = new FizzBuzz();
  ```
  - Now we just need an expectation withing our it block:
  ```javascript
  expect(fizzbuzz.play(3)).toEqual('Fizz');
  ```
- Our test is ready, but notice the methods are named with CamelCase in Javascript convention.
- Let's move into the code to make it pass: _this is the code for the App. It creates a first function `FizzBuzz` (in ruby this would be the class) and then two other functions depending on it (methods in ruby)._

```javascript
function FizzBuzz() {
}

FizzBuzz.prototype.play = function(number) {
  if (this._isDivisibleBy(15, number)) {
    return 'FizzBuzz';
  } else if (this._isDivisibleBy(5, number)) {
    return 'Buzz';
  } else if (this._isDivisibleBy(3, number)) {
    return 'Fizz';
  } else {
    return number;
  }
}

FizzBuzz.prototype._isDivisibleBy = function(divisor, number) {
  return number % divisor === 0;
}
```

**What I've Learned:**

> - **Jasmine** is a testing framework to test JS. It runs in a browser and syntax is similar or close to **RSpec** 

- In JavaScript we do use functions as a convenient way to instantiate objects that share behaviour.

```javascript
function Dog(name) {
  this.name = name;
}

var barney = new Dog('Barney');
```
- Anonymous functions work similar as blocks: _This is normally called a callback_

```javascript
var callback = function(arg) {
  console.log(arg);
};

['one', 'two', 'three'].forEach(callback);
```
- Function to define methods:

```javascript
function Dog(name) {
  this.name = name
}

Dog.prototype.bark = function() {
  console.log(this.name + ' says Woof!')
};

# We can call bark in any instance of Dog

fido = new Dog('fido');
fido.bark();
```
_It's easy to think of bark as being a method of Dog. But it isn't. Objects in JavaScript are just bags of properties. So fido is just a bag of properties, some of which it inherits from the prototype of Dog. And bark is just a property that happens to contain a Function object. It behaves like a method because of the way it is invoked_

<br>

## Daily Goals 
### Tuesday 12 of May 2020

## Morning Goals 

#### Attend workshop *"Following the flow and getting visibility in JavaScript"*.

**Plan:**

- Learning to build new skills that let you learn a new language and its patterns.
- Practice a bunch of different ways of following the flow and getting visibility in JavaScript.
  
**Process:** 

#### Following the flow

Understanding which parts of your code are running and in which order.

Very similar to tightening the loop, but with a different goal.  Instead of trying to narrow in on one buggy line of code, you're just trying to understand what happens when a piece of code runs.

#### Getting visibility

Looking at the data contained in the variables in the code you're trying to understand.

#### Ways of following the flow

##### console.logging recognisable strings

A great way of following the flow is to `console.log()` little strings that you recognise.  You can see which ones are printed in which order to figure out what code is running and in which order.

```javascript
Airport.prototype.land = function(plane) {
  if (plane.isLanded()) {
    console.log("hello1");
  } else if (this.weather.isStormy()) {
    console.log("hello2");
  } else {
    console.log("hello3");
  }
}
```

#### Using a step debugger

A debugger is a program that runs your program and lets you step through your program line by line.  Some people really love using a debugger.  Others don't.  Give one a try and see how you feel.

Add `debugger;` to a line in your program that you **know** runs e.g.:

```javascript
function sayHi() {
  debugger;
  console.log("hi!");
};

sayHi();
```
Run the program and go to the Sources tab of the Chrome dev tools.  To move through your code line by line, click on the Step Over, Step Into and Step Out Of buttons on the far right hand side (they look like little arrows).

#### Ways of getting visibility

#### `console.log()`

##### `this`

Really handy to know what value `this` has in a piece of code.  It changes!

```javascript
console.log(this);
```

##### Variables

Does this variable contain what I expect?

```javascript
console.log(airport);
```
##### Functions

Am I calling the right function?

```javascript
console.log(airport.land);
```

##### Function return values

Is this function returning what I expect?

```javascript
console.log(airport.land());
```

##### Function parameters

Does this parameter contain what I expect? What does this parameter even contain?

```javascript
Airport.prototype.land = function(plane) {
  console.log(plane);
}
```
**What I've Learned:**

> We can debug an app build in **JS** by tightening the loop and getting visibility by `console.log();` values as we go down the stream of the code.  

> We can as well use **debugger**. When you run a debugger, you can hover over variables to see their values at any given point of line execution.

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"FizzBuzz in JavaScript"**](https://github.com/EdAncerys/Airport-Challenge-in-JavaScript)

**Plan:** Pair with Lizzie and keep working on the afternoon challenges for the week - *"FizzBuzz in JavaScript".*

**Process:**

#### Let's start with a user story to drive a feature test:

```
As an air traffic controller
To get passengers to a destination
I want to instruct a plane to land at
  an airport and confirm that it has landed
```

#### To create the feature test in `spec/featureSpec.js`

```javascript
// spec/featureSpec.js
'use strict';

describe('Feature Test:', function(){
  var plane;
  var airport;

  beforeEach(function(){
    plane = new Plane();
    airport = new Airport();
  });

  it('planes can be instructed to land at an airport', function(){
    plane.land(airport);
    expect(airport.planes()).toContain(plane);
  });
});
```

#### We then create a unit test for a Plane:

```javascript
// spec/planeSpec.js
'use strict';

describe('Plane',function(){
  var plane;
  beforeEach(function(){
    plane = new Plane();
  });
  it('can land at an airport', function(){
    expect(plane.land).not.toBeUndefined()
  });
});
```

#### To define our Plane class:

```javascript
// src/plane.js
'use strict';

class Plane {
    land(){};
}
```

#### To create an Airport spec:

```javascript
// spec/airportSpec.js
'use strict';

describe('Airport', function(){
  var airport;
  beforeEach(function(){
    airport = new Airport();
  });
  it('has no planes by default', function(){
    expect(airport.planes()).toEqual([]);
  });
});
```

So now we have unit test failures that match our feature test failures.

```
Airport has no planes by default
  ReferenceError: Airport is not defined
  TypeError: Cannot read property 'planes' of undefined
```

So let's create an airport:

```javascript
// src/airport.js
'use strict';

class Airport{};
```

which drops us to a single matching unit and feature failure:

```
Feature Test: planes can be instructed to land at an airport
  TypeError: airport.planes is not a function
Airport has no planes by default
  TypeError: Cannot read property 'planes' of undefined
```

```javascript
// src/airport.js
'use strict';

class Airport{
  planes() {
    return [];
  };
};
```

which finally takes us to the final part of the feature test, with this failure:

```javascript
Feature Test: planes can be instructed to land at an airport
  Expected [  ] to contain Plane({  }).
```

So we need our plane object to interact with our airport object.  It's tempting here just to implement the final step, but if we're careful with our London style unit testing we want to stub the interaction in the plane unit test like so:

```javascript
// spec/planeSpec.js
'use strict';

describe('Plane',function(){
  var plane;
  var airport;
  beforeEach(function(){
    plane = new Plane();
    airport = jasmine.createSpyObj('airport',['clearForLanding']);
  });
  it('can land at an airport', function(){
    plane.land(airport);
    expect(airport.clearForLanding).toHaveBeenCalledWith(plane);
  });
});
```

where spys are Jasmine's equivalent of doubles.  Notice we've dropped the now redundant check that plane.land is defined, and now this test gives us the following unit test level failure:

```
Plane can land at an airport
  Expected spy airport.clearForLanding to have been called with [ Plane({  }) ] but it was never called.
```

We're using Sandi Metz's space capsule technique, stubbing the outgoing interaction from plane to airport.  Let's have the plane talk to the airport to ask to land:

```javascript
class Plane {
    land(airport){
      airport.clearForLanding(this)
    };
};
```

which satisfies out unit test, but our feature test now fails with:

```
Feature Test: planes can be instructed to land at an airport
  TypeError: airport.clearForLanding is not a function
```

Plane is doing everything it needs to, but now we need Airport to play its part, so a unit test for Airport is in order to make sure it stores a reference to the incoming plane after clearForLanding is called.  To move a little faster let's skip the trivial test that clearForLanding is defined, and go straight to making a spy that we can check has been landed correctly.

```javascript
'use strict';

describe('Airport', function(){
  var airport;
  var plane;
  beforeEach(function(){
    airport = new Airport();
    plane = jasmine.createSpy('plane',['land']);
  });
  it('has no planes by default', function(){
    expect(airport.planes()).toEqual([]);
  });
  it('can clear planes for landing', function(){
    airport.clearForLanding(plane);
    expect(airport.planes()).toEqual([plane]);
  });
});
```

which gives is a similar unit and feature test failure:

```
Airport can clear planes for landing
  TypeError: airport.clearForLanding is not a function
Feature Test: planes can be instructed to land at an airport
  TypeError: airport.clearForLanding is not a function
```

Definitely time to get that clearForLanding method in there:

```javascript
// src/airport.js
'use strict';

class Airport{
  planes() {
    return [];
  }

  clearForLanding(plane) {};
};
```

Remember each step we are doing the absolute minimum of work to change the error message(s).  We're trying to write the leanest code possible; we want every line of code to actually be necessary.  Now we get:

```
Airport can clear planes for landing
  Expected [  ] to equal [ spy on plane ].
Feature Test: planes can be instructed to land at an airport
  Expected [  ] to contain Plane({  }).
```

So finally time to get this method to work for a living; and Airport will need some state too:

```javascript
// src/airport.js
'use strict';

class Airport{
  constructor() {
    this._hangar = []
  }
  planes() {
    return this._hangar;
  }
  clearForLanding(plane) {
    this._hangar.push(plane);
  };
};
```

And we are all green!  Note our use of underscore as a prefix to the _hangar variable to indicate that this state should be private.

So our feature is now complete and we have a couple of London style unit tests looking after our models.

**What I've Learned:**

>**Jasmine Spies:** Jasmine has test double functions called spies. A spy can stub any function and tracks calls to it and all arguments. A spy only exists in the describe or it block in which it is defined, and will be removed after each spec. There are special matchers for interacting with spies: `toHaveBeenCalled`, `and.callThrough`, `and.returnValue`, `and.throwError`...

>**Create Spy Object** we use this function in Jasmine when we want to test dependencies that are not available within the actual context, like for creating doubles of other classes. _In the example, while testing Plane we make a 'double' of Airport that takes a function (method) 'clearForLanding' and 'clearForTakeoff._
```javascript
describe('Plane',function(){
  var plane;
  var airport;
  beforeEach(function(){
    plane = new Plane();
    airport = jasmine.createSpyObj('airport',['clearForLanding','clearForTakeOff']);
  });
```

<br>

## Daily Goals 
### Wednesday 13 of May 2020

## Morning Goals 

#### Rules that govern the behavior of the this keyword..

**Plan:**

- Perform research online individually.  
- Describe what **keyword this** used for in **JS**. 
- Summarize and give some practical example. 
  
**Process:** 

A function's this keyword behaves a little differently in JavaScript compared to other languages. It also has some differences between strict mode and non-strict mode.

In most cases, the value of this is determined by how a function is called (runtime binding). It can't be set by assignment during execution, and it may be different each time the function is called. ES5 introduced the bind() method to set the value of a function's this regardless of how it's called, and ES2015 introduced arrow functions which don't provide their own this binding (it retains the this value of the enclosing lexical context).

```javascript
class Cat {
  constructor(legs){
    this.legs = legs;
  }
  
  speak() {
    return "I have " + this.legs + " legs! Meow!";
  }
}
```

#### `this` refers to the context of an executing function.

- When you call a method of an object, JavaScript sets this to the object that owns the method. See the following car object:
```javascript
let car = {
    brand: 'Honda',
    getBrand: function () {
        return this.brand;
    }
}
console.log(car.getBrand()); // Honda
```

In this example, the this object in the getBrand() method references the car object.

Since a method is a property of an object which is a value, you can store it in a variable.
```javascript
let brand = car.getBrand;
And then call the method via the variable

console.log(brand()); // undefined
```
You get undefined instead of "Honda" because when you call a method without specifying its object, JavaScript sets this to the global object in strict mode and undefined in the non-strict mode.

To fix this issue, you use the bind() method of the Function.prototype object. The bind() method creates a new function with the this keyword is set to a specified value.

```javascript
let brand = car.getBrand.bind(car);
console.log(brand()); // Honda
```

In this example, when you call the brand() method, the this keyword is bound to the car object. For example:

```javascript
let car = {
    brand: 'Honda',
    getBrand: function () {
        return this.brand;
    }
}

let bike = {
    brand: 'Harley Davidson'
}

let brand = car.getBrand.bind(bike);
console.log(brand()); // Output: Harley Davidson
```

**What I've Learned:**

> - The this references the object of which the function is a property. In other words, the this reference the object that is currently calling the function.



