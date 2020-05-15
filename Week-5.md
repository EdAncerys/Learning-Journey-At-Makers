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

> - The this references the object of which the function is a property. In other words, the **this** reference the object that is currently calling the function.

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Thermostat App"**](https://github.com/EdAncerys/Thermostat-Java-Script)

**Plan:** Pair with Marija and keep working on the afternoon challenge for the week - *"Thermostat App".*

**Process:**

So let's start with the customer's requirements:

1. Thermostat starts at 20 degrees
2. You can increase the temp with an up function
3. You can decrease the temp with a down function
4. The minimum temperature is 10 degrees
5. If power saving mode is on, the maximum temperature is 25 degrees
6. If power saving mode is off, the maximum temperature is 32 degrees
7. Power saving mode is on by default
8. You can reset the temperature to 20 with a reset function
9. You can ask about the thermostat's current energy usage: < 18 is `low-usage`, < 25 is `medium-usage`, anything else is `high-usage`.
10. (In the challenges where we add an interface, low-usage will be indicated with green, medium-usage indicated with black, high-usage indicated with red.)

#### The First Test

Setting up directory with all needed requirements to use [**Jasmine**](https://github.com/jasmine/jasmine) and start TDD approach by writing first test:

```javascript
// spec/thermostatSpec.js

'use strict';

describe('Thermostat', function() {

  var thermostat;

  beforeEach(function() {
    thermostat = new Thermostat();
  });

  it('starts at 20 degrees', function() {
    expect(thermostat.temperature).toEqual(20);
  });
});
```

We're going to use **strict mode**, which you can read up on here: [MDN - Strict Mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode). To invoke strict mode, place this at the top of your files:

```javascript
'use strict';
```
This is purely to encourage us to write a higher standard of JavaScript.

So our expectation here, is that upon creation, our `thermostat` will default to a `temperature` of 20.

```javascript
// src/thermostat.js

class Thermostat {
  constructor() {
    this.temperature = 20;
  }
}
```
Re factor our test and code a little to allow for this.

```javascript
// spec/thermostatSpec.js

  it('starts at 20 degrees', function() {
    expect(thermostat.getCurrentTemperature()).toEqual(20);
  });
```

We place parenthesis at the end. This is to communicate to the JavaScript interpreter that we want it to execute this function, as opposed to returning the function itself.

#### Creating a method

```javascript
class Thermostat {
  constructor() {
    this.temperature = 20;
  }
  getCurrentTemperature() {
  }
}
```

Now, we want `getCurrentTemperature()` to return the current temperature of Thermostat, and we achieve this using the following:

```javascript

class Thermostat {
  constructor() {
    this.temperature = 20;
  }
  getCurrentTemperature() {
    return this.temperature;
  }
};
```

#### It's getting hot in here

So the only sensible thing to do now is to turn the temperature up! Let's write a test:

```javascript
// spec/thermostatSpec.js

  it('increases in temperature with up()', function() {
    thermostat.up();
    expect(thermostat.getCurrentTemperature()).toEqual(21);
  });
```

Now, at this point we need to write a method which increases the value of `thermostat.temperature` each time we run it. So with that in mind, I'm going to lay the solution out for your reference:

```javascript
class Thermostat {
  constructor() {
    this.temperature = 20;
  }
  getCurrentTemperature() {
    return this.temperature;
  }
  up() {
    this.temperature += 1
  }
}
```

And so by that logic, decreasing the temperature:

```javascript
// spec/thermostatSpec.js

it('decreases in temperature with down()', function() {
  thermostat.down();
  expect(thermostat.getCurrentTemperature()).toEqual(19);
});
```

Our implementation should follow that of our `up()` function:

```javascript
class Thermostat {
  constructor() {
    this.temperature = 20;
  }
  getCurrentTemperature() {
    return this.temperature;
  }
  up() {
    this.temperature += 1
  }
  down() {
    this.temperature -= 1
  }
}
```

#### Limiting the temperature

Our client has chosen 10 degrees as the minimum temperature our users should be able to set the Thermostat to.

```javascript
// spec/thermostatSpec.js

it('has a minimum of 10 degrees', function() {
  for (var i = 0; i < 11; i++) {
    thermostat.down();
  }
  expect(thermostat.getCurrentTemperature()).toEqual(10);
});
```

Now given that our `thermostat` has a default `temperature` of 20, and we want to test that we can't go more than 10 degrees below that default, here we employ a loop to handle the cumbersome test setup of calling `thermostat.down` eleven times.

It's at this point we have a good case for adding another property to our object constructor function:

```javascript
// src/thermostat.js

'use strict';

constructor() {
    this.MINIMUM_TEMPERATURE = 10;
    this.temperature = 20;
  }
```

Notice how I'm using capital letters for the property name? As you might probably have realised, I intend this value to be a constant, and am marking that intention in the use of capitalization. 

```javascript
// src/thermostat.js
  isMinimumTemperature() {
    return this.temperature === this.MINIMUM_TEMPERATURE;
  }
```

And now let's edit our `down()` function to take advantage of this new temperature check:

```javascript
// src/thermostat.js

down() {
    if (this.isMinimumTemperature()) {
      return;
    }
    this.temperature -= 1
  }
```

So now we have a kind of guard condition before we are allowed to decrease our temperature!

#### Power Saving Mode

Now our spec says that PSM should be activated by default, so let's go ahead and write a test for this:

```javascript
// spec/thermostatSpec.js

it('has power saving mode on by default', function() {
  expect(thermostat.isPowerSavingModeOn()).toBe(true);
});
```

Which leads us to the understanding that we will require a new property, and a new getter method to read that property:

```javascript
// src/thermostat.js

'use strict';

constructor() {
  // Other properties omitted for brevity
  this.powerSavingMode = true;
}
```

and our getter method:

```javascript
// src/thermostat.js
isPowerSavingModeOn() {
    return this.powerSavingMode === true;
}
```
Now in order to make this PSM business a viable proposition, we need the ability to switch it on and off. Since it's on by default, let's make our next step to turn it off:

```javascript
// spec/thermostatSpec.js

it('can switch PSM off', function() {
  thermostat.switchPowerSavingModeOff();
  expect(thermostat.isPowerSavingModeOn()).toBe(false);
});
```

Since we already have the `powerSavingMode` property to work with, lets get straight to our function:

```javascript
// src/thermostat.js

switchPowerSavingModeOff() {
    this.powerSavingMode = false;
  }
```

Reverse and test for both conditions `switchPowerSavingModeOn` method:

```javascript
// spec/thermostatSpec.js

it('can switch PSM back on', function() {
  thermostat.switchPowerSavingModeOff();
  expect(thermostat.isPowerSavingModeOn()).toBe(false);
  thermostat.switchPowerSavingModeOn();
  expect(thermostat.isPowerSavingModeOn()).toBe(true);
});
```

And so goes our function:

```javascript
// src/thermostat.js

switchPowerSavingModeOn() {
  this.powerSavingMode = true;
}
```

#### The Upper limits

So if we refer back to our client's wishes, we are required to limit the temperature as follows:

* To 25 degrees when PSM is activated
* to 32 degrees when PSM is off

So we are going to revisit our incremental function `up()`. Test for that would be as follows:

```javascript
// spec/thermostatSpec.js

describe('when power saving mode is on', function() {
  it('has a maximum temperature of 25 degrees', function() {
    for (var i = 0; i < 6; i++) {
      thermostat.up();
    }
    expect(thermostat.getCurrentTemperature()).toEqual(25);
  });
});
```

We use nested `describe()` blocks. In Jasmine there is no equivalent to RSpec's `context()` so we have to use nested describe block. So, let's make sure our test setup cannot increase the temperature to 26 when PSM is off:

```javascript
// src/thermostat.js

up() {
  if (this.isMaximumTemperature()) {
    return;
  }
  this.temperature += 1;
}
```

We are going to need a couple of extra properties in our object constructor function:

```javascript
// src/thermostat.js

'use strict';

function Thermostat() {
  // Other properties omitted for brevity
  this.MAX_LIMIT_PSM_ON = 25;
  this.MAX_LIMIT_PSM_OFF = 32;
}
```

```javascript
// src/thermostat.js

isMaximumTemperature() {
  if (this.isPowerSavingModeOn() === false) {
    return this.temperature === this.MAX_LIMIT_PSM_OFF;
  }
  return this.temperature === this.MAX_LIMIT_PSM_ON;
}
```

To make sure our logic is sound, let us write a counter test to make double-sure:

```javascript
// spec/thermostatSpec.js

describe('when power saving mode is off', function() {
  it('has a maximum temperature of 32 degrees', function() {
    thermostat.switchPowerSavingModeOff();
    for (var i = 0; i < 13; i++) {
      thermostat.up();
    }
    expect(thermostat.getCurrentTemperature()).toEqual(32);
  });
});
```

### Reset!

Client wanted us to have a reset method to bring us back to the default temperature:

```javascript
// spec/thermostatSpec.js

it('can be reset to the default temperature', function() {
  for (var i = 0; i < 6; i++) {
    thermostat.up();
  }
  thermostat.resetTemperature();
  expect(thermostat.getCurrentTemperature()).toEqual(20);
});
```

In this situation we could create a method that does the following:

```javascript
// src/thermostat.js

resetTemperature() {
  this.temperature = 20;
}
```
Let's  go back to our object constructor function and do a little re-factor:

```javascript
// src/thermostat.js

constructor {
  // Other properties omitted for brevity
  this.DEFAULT_TEMPERATURE = 20;
  this.temperature = this.DEFAULT_TEMPERATURE;
}
```

This means we can tidy up our `resetTemperature()` function:

```javascript
// src/thermostat.js

resetTemperature() {
  this.temperature = this.DEFAULT_TEMPERATURE;
}
```

#### Energy usage

The last requirement our client has given us, is that we should be able to demonstrate to our user where their energy usage sits.  We are going to have a function that outputs `high-usage`, `medium-usage` or `low-usage`.

With that, let's write our final tests:

```javascript
// spec/thermostatSpec.js

describe('displaying usage levels', function() {
  describe('when the temperature is below 18 degrees', function() {
    it('it is considered low-usage', function() {
      for (var i = 0; i < 3; i++) {
        thermostat.down();
      }
      expect(thermostat.energyUsage()).toEqual('low-usage');
    });
  });

  describe('when the temperature is between 18 and 25 degrees', function() {
    it('it is considered medium-usage', function() {
      expect(thermostat.energyUsage()).toEqual('medium-usage');
    });
  });

  describe('when the temperature is anything else', function() {
    it('it is considered high-usage', function() {
      thermostat.powerSavingMode = false;
      for (var i = 0; i < 6; i++) {
        thermostat.up();
      }
      expect(thermostat.energyUsage()).toEqual('high-usage');
    });
  });
});
```

`MEDIUM_ENERGY_USAGE_LIMIT`

```javascript
// src/thermostat.js

constructor {
  // Other properties omitted for brevity
  this.MEDIUM_ENERGY_USAGE_LIMIT = 18;
}
```

Function `energyUsage()` now can be re-factor as accordingly:

```javascript
// src/thermostat.js

energyUsage() {
  if (this.temperature < this.MEDIUM_ENERGY_USAGE_LIMIT) {
    return 'low-usage';
  }
  if (this.temperature >= this.MEDIUM_ENERGY_USAGE_LIMIT && this.temperature <= this.MAX_LIMIT_PSM_ON) {
    return 'medium-usage';
  }
  return 'high-usage';
}
```

**What I've Learned:**

> Strict Mode it makes us write higher standard JS as converts mistakes (that could be passed by without strict mode) into errors, so we can fix them in the moment instead of risking them causing problems in a future when it would be more difficult to find them. For example, it is impossible to create global variables by mistake in strict mode (if you mistype a variable in sloppy mode JS will just create that new object and keep working, but functionality might be affected).

## Daily Goals 
### Thursday 14 of May 2020

## Morning Goals 

#### Attend Callbacks and following the flow of control workshop.

**Plan:**

- Describe "the flow of control of a program" as "the order in which the parts of the code are executed".
- Explain the process you use to follow the flow of control.
- Follow the flow of control to help you understand how callbacks work.
  
**Process:** 

#### Following the flow of control

Imagine you want to follow the flow of control in this code.  That is, you want to understand what parts run and in what order they run.

```js
document.addEventListener('click', function() {
  console.log("click!");
});

```

1. Before running the code, add some `console.log`s.  Log `console.log(1)` in the bit of code you think will get run first, `console.log(2)` in the bit of code you think will get run second, and so on. For example:

```js
console.log(1);

document.addEventListener('click', function() {
  console.log(2);
  console.log("click!");
  console.log(3);
});

console.log(4);
```

2. Run the code to see if the numbers get printed in order (1, 2, 3 etc.).  If they do, your prediction is correct.

3. If your prediction is incorrect, examine the code and experiment with it to try to figure out why.  Once you have more information, update your `console.log`s to reflect your prediction and return to step 2.

#### Following the flow fast

A developer constantly analyses the flow of control of their code.  Keep trying to improve this skill.  The more adept you are at reading the flow of control without running the code, the faster you'll be.  Build this intuition by making predictions and checking if your prediction is right.

**What I've Learned:**

> - A callback function is a function that is passed as an argument to another function, to be “called back” at a later time. A function that accepts other functions as arguments is called a higher-order function, which contains the logic for when the callback function gets executed. It’s the combination of these two that allow us to extend our functionality. Callback, also known as a higher-order function.

> Consider this common use of a callback function in jQuery:

```javascript
//Note that the item in the click method's parameter is a function, not a variable.
//The item is a callback function
$("#btn_1").click(function() {
  alert("Btn 1 Clicked");
});
```

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Thermostat App"**](https://github.com/EdAncerys/Thermostat-Java-Script)

**Plan:** Pair with Zsofia and keep working on the afternoon challenge for the week - *"Thermostat App".*

**Process:**

#### jQuery

- Use jQuery to build interactive functionality into a webpage
- Understand some things about how jQuery uses the technique of callbacks

Can enable **jQuery** by linking external *src* file **CDN** (content delivery service):

```html
<script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
```

Call back function representation with **jQuery**:

#### $(document).ready(function() { })

This utility function translates to "only execute the function when the document is ready", i.e. when the DOM is loaded. This is a good idea because it's difficult (but not impossible!) to attach an event listener to something that isn't there. Forgetting to wrap jQuery code in this is a common source of bugs.

#### jQuery selector

The jQuery selector generally works like this:

```javascript
$('element')
```

where `element` is a CSS selector, or a tag name. Chrome Dev Tools actually comes with a very similar feature, so you can try it out on any page. Try selecting some `.classes`, `#ids` and HTML tags.

#### Event listeners

In longhand, these usually look like

```javascript
$('element').on('event', function() {

})
```

where `event` is an action you would like to listen for on the page. Popular events include clicks, scrolls, typing and generally any kind of page interaction. The most popular ones generally have convenient shortcut functions, so you can write `$('element').click(function() { })`, for example.

#### Callbacks

The callback is the anonymous function passed as last argument to the event handler:

```javascript
$('#some-heading').click(function() {
  // this function is the callback!
})
```

In this case, the callback is the function passed to the `click` function, that executes at some point in the future. The plain English translation would be "when there is a click on the element with the ID `some-heading`, run the function".

```javascript
// console
$('#temperature').text('hello jQuery world!');
```

Now we can put this in our actual interface file, wrapped in a `$(document).ready(function() {})`, so that it only triggers when the DOM has finished loading.

```javascript
// interface.js
$(document).ready(function() {
  var thermostat = new Thermostat();
  $('#temperature').text(thermostat.temperature);
})
```

Flow of what happens when a user interaction happens:

**user input -> event listener -> update model -> update view to reflect change in model**

In code:

```javascript
$('#temperature-up').on('click', function() { // event listener
  thermostat.up(); // update model
  $('#temperature').text(thermostat.temperature); // update view
})
```

And the same again for decreasing the temperature:

```javascript
$('#temperature-down').click(function() { // this is an alternate version of .on('click'), with a sprinkle of jQuery syntactic sugar
  thermostat.down();
  $('#temperature').text(thermostat.temperature);
})
```

Re-factor updating the temperature to its own clearly-named function:

```javascript
function updateTemperature() {
  $('#temperature').text(thermostat.temperature);
}
```

Hooking the other buttons up should be relatively straightforward, resulting in something like this:

```javascript
// interface.js
$(document).ready(function() {
  var thermostat = new Thermostat();
  updateTemperature();

  $('#temperature-up').click(function() {
    thermostat.up();
    updateTemperature();
  });

  $('#temperature-down').click(function() {
    thermostat.down();
    updateTemperature();
  });

  $('#temperature-reset').click(function() {
    thermostat.resetTemperature();
    updateTemperature();
  });

  $('#powersaving-on').click(function() {
    thermostat.switchPowerSavingModeOn();
    $('#power-saving').text('on')
    updateTemperature();
  })

  $('#powersaving-off').click(function() {
    thermostat.switchPowerSavingModeOff();
    $('#power-saving').text('off')
    updateTemperature();
  })

  function updateTemperature() {
    $('#temperature').text(thermostat.temperature);
  };
});
```

We can delegating to the CSS itself to change color value(and/or other if needed) by just changing the class so that the CSS can decide how to handle colors:

```javascript
function updateTemperature() {
  $('#temperature').text(thermostat.temperature);
  $('#temperature').attr('class', thermostat.energyUsage());
}
```

And now the CSS can handle colors (we just need to place this in its own file and link it in with the appropriate tag):

```css
.low-usage {
  color: green;
}

.medium-usage {
  color: black;
}

.high-usage {
  color: red;
}
```

**What I've Learned:**

> - jQuery is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers. 

> - jQuery takes a lot of common tasks that require many lines of JavaScript code to accomplish, and wraps them into methods that you can call with a single line of code.

## Daily Goals 
### Friday 15 of May 2020

## Morning Goals 

#### Closures and Prototypes in JS.

**Plan:**

- Perform research online individually.  
- Describe what **closers and prototypes are in JS ** and it's usages. 
- Summarize and give some practical example. 
  
**Process:** 

Closures in JavaScript are one of those concepts that many struggle to get their heads around. In the following article, I will explain in clear terms what a closure is, and I’ll drive the point home using simple code examples.

#### What is a closures in JS?

A closure is a feature in JavaScript where an inner function has access to the outer (enclosing) function’s variables — a scope chain.

The closure has three scope chains:

- it has access to its own scope — variables defined between its curly brackets
- it has access to the outer function’s variables
- it has access to the global variables

Let’s look at a simple closure example in JavaScript:

```js
function outer() {
   var b = 10;
   function inner() {
        
         var a = 20; 
         console.log(a+b);
    }
   return inner;
}
```

Here we have two functions:

- an outer function outer which has a variable b, and returns the inner function
- an inner function inner which has its variable called a, and accesses an outer variable b, within its function body

The scope of variable b is limited to the outer function, and the scope of variable a is limited to the inner function.

#### Prototypes is JS

The prototype property is initially an empty object, and can have members added to it - as you would any other object.

```js
var myObject = function(name){
    this.name = name;
    return this;
};
 
console.log(typeof myObject.prototype); // object
 
myObject.prototype.getName = function(){
    return this.name;
};
```
In the snippet above, we’ve created a function, but if we call myObject(), it will simply return the window object, because it was defined within the global scope. this will therefore return the global object, as it has not yet been instantiated.

```js
console.log(myObject() === window); // true
```
#### How to Use Prototype

To make the application run faster (and follow best practices), we can (re)define the prototype property of the myObject; every instance of myObject will then reference the methods within myObject.prototype as if they were their own methods.

We can then instantiate the myObject 100 times and still keep the App performance in good shape rather then having 100 different methods in memory.

```js
// define the GameObject constructor function
var myObject = function(width, height) {
    this.x = Math.floor((Math.random() * myCanvasWidth) + 1);
    this.y = Math.floor((Math.random() * myCanvasHeight) + 1);
    this.width = width;
    this.height = height;
    return this;
};
 
// (re)define the GameObject prototype object
myObject.prototype = {
    x: 0,
    y: 0,
    width: 5,
    width: 5,
    draw: function() {
        myCanvasContext.fillRect(this.x, this.y, this.width, this.height);
    }
};
```

The JavaScript prototype property also allows you to add new methods to objects constructors:

```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.name = function() {
  return this.firstName + " " + this.lastName;
};
```

**What I've Learned:**

> - A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

> - Prototypes are the mechanism by which JavaScript objects inherit features from one another. 

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
[**"Thermostat App"**](https://github.com/EdAncerys/Thermostat-Java-Script)

**Plan:** Pair with Zsofia and keep working on the afternoon challenge for the week - *"Thermostat App".*

**Process:**

#### Learning Objectives covered

- Define 'AJAX' as 'Asynchronous JavaScript And XML'
- Explain that AJAX allows users to interact asynchronously with other web entities (such as servers) without page reloads
- Use AJAX to retrieve data from an API

#### Thermostat: APIs

To get the weather for London we can returns in the console, using a basic `$.get` request:

```javascript
// console
$.get('http://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=a3d9eb01d4de82b9b8d0849ef604dbed', function(data) {
  console.log(data);
})
```

`$.get()` is shorthand for `$.ajax()`, which in turn is a wrapper around JavaScript's inbuilt `XMLHttp` library.

We can pass an additional parameter to the request to make sure our request returns a metric unit, in this case Celcius:

```javascript
// console
$.get('http://api.openweathermap.org/data/2.5/weather?q=London,uk&appid=a3d9eb01d4de82b9b8d0849ef604dbed&units=metric', function(data) {
  console.log(data.main.temp);
})
```

To add some HTML to hold the result:

```html
<section>
  <h1>Current temperature: <span id="current-temperature"></span></h1>
</section>
```

And display it on page load:

```javascript
// interface.js, within the $(document).ready(function() { })
$.get('http://api.openweathermap.org/data/2.5/weather?q=London&appid=a3d9eb01d4de82b9b8d0849ef604dbed&units=metric', function(data) {
  $('#current-temperature').text(data.main.temp);
})
```

To load this dynamically, based on the user's selection. One way you can do this is to have a selector with pre-defined cities, and some JavaScript to detect the change:

```html
<section>
  <h1>Current temperature: <span id="current-temperature">20</span></h1>
  <select id="current-city">
    <option value="london">London</option>
    <option value="newyork">New York</option>
    <option value="paris">Paris</option>
    <option value="tokyo">Tokyo</option>
  </select>
</section>
```

```javascript
// interface.js
$('#current-city').change(function() {
  var city = $('#current-city').val();
  $.get('http://api.openweathermap.org/data/2.5/weather?q=' + city + '&appid=a3d9eb01d4de82b9b8d0849ef604dbed&units=metric', function(data) {
    $('#current-temperature').text(data.main.temp)
  })
})
```

Or can let the user type in whatever city they want:

```html
<section>
  <h1>Current temperature: <span id="current-temperature">20</span></h1>
  <form id="select-city">
    <input id="current-city" type="text" placeholder="Enter a city"></input>
    <input type="submit"></input>
  </form>
</section>
```

```javascript
// interface.js
$('#select-city').submit(function(event) {
  event.preventDefault();
  var city = $('#current-city').val();
  $.get('http://api.openweathermap.org/data/2.5/weather?q=' + city + '&appid=a3d9eb01d4de82b9b8d0849ef604dbed&units=metric', function(data) {
    $('#current-temperature').text(data.main.temp);
  })
})
```

Either way, that `$.get()` function is looking a bit messy - to re factor and extract it to a function that's a bit clearer:

```javascript
// interface.js
function displayWeather(city) {
 var url = 'http://api.openweathermap.org/data/2.5/weather?q=' + city;
 var token = '&appid=a3d9eb01d4de82b9b8d0849ef604dbed';
 var units = '&units=metric';
 $.get(url + token + units, function(data) {
   $('#current-temperature').text(data.main.temp);
 })
```

And refactor the existing code:

```javascript
// interface.js

displayWeather('London');

$('#select-city').submit(function(event) {
  event.preventDefault();
  var city = $('#current-city').val();
  displayWeather(city);
})

```

**What I've Learned:**

> - Asynchronous JavaScript and XML, while not a technology in itself, is a "new" approach to using a number of existing technologies together, including HTML or XHTML, CSS, JavaScript, DOM, XML, XSLT, and most importantly the XMLHttpRequest object.

> - When these technologies are combined in the Ajax model, web applications are able to make quick, incremental updates to the user interface without reloading the entire browser page. This makes the application faster and more responsive to user actions.

> - Although X in Ajax stands for XML, JSON is used more than XML nowadays because of its many advantages such as being lighter and a part of JavaScript. Both JSON and XML are used for packaging information in the Ajax model.








