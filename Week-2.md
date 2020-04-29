# Week 2 Goals 

- Use all of week 1's skills (don't underestimate the importance of this)
- Break one class into two classes that work together, while maintaining test coverage
- Unit test classes in isolation using mocking
- Explain some basic OO principles and tie them to high level concerns (e.g. ease of     change)
- Review another person's code and give them meaningful feedback

## Daily Goals 
### Monday 20 of April 2020

## Morning Goals 

Code Review for the weekend [**Airport Challenge:**](https://github.com/EdAncerys/airport_challenge)

**Plan:** Peer code review of the weekend challenge. Will be reviewing and getting a feedback to Jed's code.

**Process:**  
- Attend todays *"Intro to code review"* workshop. 
- Start with making an appreciation about Jed’s code.
- Write at least one piece of constructive feedback.
- Spend time implementing those changes.

**What I've learned:**  

> **Test doubles** allow you to define objects that "stands" for a real object in your system and will give and "received" data in a predefined patterns as if they were an actual object. To **create a double** use:
```rb
plane = double() # create a double with an optional name
plane = double("new plane")
```

## Afternoon Challenges  

*Practice pairing and Test-Driven development.*  
**"Oystercard Challenge"**

**Plan:** Pair with Jed and keep working on the afternoon challenge for the week - *"Oystercard Challenge".*

**Process:**

- Create a Gemfile (source for gems, version of ruby and add the **RSpec** gem to "test" and "development" groups).
- Create **RSpec** conventional files
- Review debugging basics (understand how to read a stack trace).
- Enable Oystercard card to have a #balance (and equal to 0) on the very first step. 
- Add ability to add money to the *Oystercard* balance on a #top_up.
```rb
  it '#top_up should be able to add to the balance' do
    expect(subject.balance).to eq Oystercard::MINIMUM_VALUE
  end
```  

- Enable #top_up functionality to the *card*.
- Enforce *maximum* balance to the *Oystercard*.
- Ability to #deduct money from current *@balance*.
```rb
  def deduct(value)
    @balance -= value
  end
```
- Add touch in/out support for *Oystercard*.
```rb
  it 'should change @in_journey to false when #touch_out' do
    subject.touch_in "station"
    expect(subject.touch_out).to eq false
  end
```
- Functionality to checking *minimum* balance on touch in for the card.
- When journey is complete, add ability the correct amount deducted from card.
```rb
  def touch_out
    deduct(MINIMUM_VALUE)
    @in_journey = false
  end
```

**What I've Learned:**

> **Gemfile:** a file we create which is used for describing gem dependencies for Ruby programs. A gem is a collection of Ruby code that we can extract into a "collection" which we can call later. Gemfile should always be in the root of your project directory, this is where Bundler expects it to be.

```rb
source "https://rubygems.org"
git_source(:github) {|repo_name| "https://github.com/#{repo_name}" }
ruby '2.7.0'
group :development, :test do
gem "rspec"
```

## Daily Goals 
### Tuesday 21 of April 2020

## Morning Goals 

Unit test classes in isolation using mocking

**Plan:**

- Perform research online individually.  
- Describe what is **Mocking and doubles** and its usage. 
- Summarize and give some practical example for **doubles**. 
  
**Process:**  

In automated testing it is common to use objects that look and behave like their production equivalents. This reduces complexity, allows to verify code independently from the rest of the classes and sometimes it is even necessary to execute self validating tests at all. A Test Double is a generic term used for these objects.

It will be times where we need to return fixed/expected value, specially if output might vary or deliberately be random. In **RSpec** we need to have predicted outcome every time no matter what is the input. There is two ways we can approach and control other methods to returned value. 

One way is by using **stubs**, that returns fixed value of the method **without testing behavior** of the method:
```rb
subject.stub(:stormy?) { true }
```

Another way is to perform **mock's**. And why **Mock**? 

- Represent objects that don't exist yet, allowing you to focus on what you are currently implementing instead of stopping and creating that object.
```rb
plane = double()
allow(plane).to receive(:stormy?).and return(true)
or
allow(plane).to receive(:stormy?) { true }
```
- Prevent your test from depending on another objects implementation and having to set up complex dependencies and data just to write a test. Mocking (*and stubbing*) allow you to truly test in isolation.
```rb
it 'able to place once' do
    allow(subject).to receive(:order).and_return("Tomato Salad")
    expect(subject).to receive(:order)
    takeaway.order("Tomato Salad")
end
```

**Creating Test double:**

A test double is an object that stands in for another object in your system during a code
example. Use the double method, passing in an optional identifier, to create one:
```rb
plane = double("plane")
```
Important fact to remember that by mocking we **Do test method functionality** by passing/expected to receive, predefined input.
And now implementing mocking in **RSpec** can be written as per bellow:

```rb
expect(subject).to receive(:stormy?).with("stormy")
```

**What I've learned:** 

>**Mocks**  

>Mocking gives you the ability to focus in on what you are testing while removing dependencies in your test on how collaborator objects are implemented. However, the dangers of ‘faking it’ means you need to mock responsibly.

>**Test doubles** allow you to define objects that "stands" for a real object in your system and will give and receive data in a predefined patterns as if they were an actual object.

## Afternoon Challenges  

*Practice pairing and Test-Driven development.*  
**"Oystercard Challenge"**

**Plan:** Pair with Colin and keep working on the afternoon challenge for the week - *"Oystercard Challenge".*

**Process:**

- Save the Entry station (upon #touch_in store station argument to instance variable. Set that variable back to nil upon touch_out)
- Re-factor to remove the in_journey variable. Rewrite the in_journey? method to infer its status based on whether or not there is an entry station
```rb
  def in_journey?
    !!@entry_station  # converts @entry_station in a boolean (will return true for any value thats not nil/false)
  end
```
- Expose entry_station instance variable using an attribute reader.
- Create a Journey History (at #touch_out push a hash with @entry_station and @exit_station into the @journey_history array)
```rb
@journey_history << {:entry_station => @entry_station, :exit_station => @exit_station}
```
- Create a station class that initializes with name and zone.

**What I've Learned:**

>**Double Bang:** When using the not-operator(!) we turn the data it's operating on into a Boolean before negating it. A truthy value would become the Boolean false and a falsy value would become the Boolean true. <br/>
When we add the second bang (!!) it flips the resultant Boolean back to the appropriate value: it will make a truthy value into the Boolean true and a falsy to false.
```rb
"hello"   #-> this is a string; it is not in a boolean context
!"hello"  #-> this is a string that is forced into a boolean 
          #   context (true), and then negated (false)
!!"hello" #-> this is a string that is forced into a boolean 
          #   context (true), and then negated (false), and then 
          #   negated again (true)
```

## Daily Goals 
### Wednesday 22 of April 2020

## Morning Goals 

Unit test and Feature test usage and deferences. 

**Plan:**

- Perform research online individually.  
- Describe what **Unit and Feature Tests are** and their usages. 
- Summarize and give some practical example. 
  
**Process:** 

**Unit tests** are automated tests written and run by software developers to ensure that a section of an application (known as the "unit") meets its design and behaves as intended. In *object-oriented programming*, a unit is often an entire interface, such as a class, but could be an individual method. By writing tests first for the smallest testable units, then the compound behaviors between those, one can build up comprehensive tests for complex applications.

<p align="center">
    <img width="200" src="images/TDD_01.png">  
    *TDD* 
</p>

**Feature Testing** normally a tester isn't concerned with the actual code, rather then to verify the output based on given the user requirements with the expected output.   

The prime objective of **Feature testing** is to check the functionalities of the system. **Feature tests** check the entire application, its hardware, and networking infrastructure, from the front end UI to the back-end database systems. In that sense, feature tests are also a form of integration testing, ensuring that different components are working together as expected.

Unlike **unit tests**, the **feature tests** don't tell you what is broken or where to locate the failure in the code base. They just tell you something is broken and not performs/couldn't be tested as expected. **Feature tests**, by definition, testing end-to-end user functionality that normally end user sees/performs at UI.

<p align="center">
    <img width="400" src="images/Feature_test_01.png">  
    *Feature Test illustration* 
</p>

**When to perform?** Unit tests aren't a replacement for functional testing. But they are the solid foundation on which the rest of your testing process should be built. 

The best practice is that you should start writing your tests when you start writing your code. Test Driven Development (TDD) is a popular software development practice which advocates writing tests before the code.  

*Unlike unit tests, the functional tests don't tell you what is broken or where to locate the failure in the code base. They just tell you something is broken.*

**What I've learned:** 

> The ultimate goal of software testing is to build a quality product. In testing, **Unit testing and Feature testing** considered as a foundation of the testing process. However, *unit testing* is performed by Developers whereas *feature testing* is performed by Testers (similar to UI).  
*According to Ward Cunningham, "Functional" test and Unit test serve different purposes. One gives the developer confidence when refactoring, the other gives the customer confidence when planning.”*

## Afternoon Challenges  

*Practice pairing and Test-Driven development.*  
**"Oystercard Challenge"**

**Plan:** Pair with Lizzie and keep working on the afternoon challenge for the week - *"Oystercard Challenge".*

**Process:**

- Spent some time to re-factor code in Lizzie's project to bring it up in better shape. 
- Reviewed and compared code and discussed similarities and differences.
- Extracted method #deduct as a private method.
```rb
  private 
  def deduct(value)
    @balance -= value
  end
```
- Added ability to have @journey_history empty upon start of the journey.
- Tested to have ability to have @journey_history after #touch_out.
```rb
  it 'shout have journey_history after a travel' do
    subject.touch_in station
    subject.touch_out station
    expect(subject.journey_history.empty?).to eq false
  end
```

**What I've Learned:**

> Privates methods can't be tested with **RSpec** directly. Walk around to test private method is by testing method that is dependent on private method and writing a test for it. It also can be done by mocking it:
```rb
expect { subject.touch_out(:deduct, Oystercard::MINIMUM_VALUE) }.to change{ subject.balance }.by -Oystercard::MINIMUM_VALUE
```

## Skills workshop

**Plan:** *Attend Skill workshop and practice TDD skills in pairs.*

*Been paired up with Dec to work on skills workshop challenges*

**Process:**

- Watch our pair partner test drive "kata" challenge and provide constructive feedback. 
- Kata that I test drive been *"Get the Middle Letter(s)"* challenge.
- My main goal was to take *step by step approach* to solve this challenge by braking it down in to smaller pieces.
- Even I did have a plan but took completely different approach to it as jumped straight in to thinking about the outcome and the result without taking methodical and thought-full approach to the challenge.
- In fact spent nearly all the time jumping from one solution to the other and waist most of the time not even taking right approach.
- Close to preset challenge time I started to make a progress as get a grip of what's needed to be done and what approach I should take.

**What I've learned:** 

> Take methodical approach to the problem. **NEVER** start solving the problem without having a plan and/or good understanding of what approach/way I should take and what requirements are in the first place! 

> Did have first practical example where I needed to expect/get different outputs in **RSpec** test. Learned that matchers can be chained to expect multiple outcomes:

```rb
it "fails when the second matcher fails" do
    expect(string).to start_with("foo").and end_with("bar")
  end
```

## Daily Goals 
### Thursday 23 of April 2020

## Morning Goals 

*Object-orientated principles (OOP)* - **Abstraction**. 

**Plan:**

- Perform research online individually.  
- Describe what **Abstraction in OO is** and it's usages. 
- Summarize and give some practical example. 
  
**Process:** 

**Abstraction** is on of the four key concepts concepts of **OOP** (Object Oriented Programming). They are *Inheritance, Abstraction, Polymorphism and Encapsulation*.

What is Abstraction in OOP? **Abstraction** is selecting data from a larger pool to show only the relevant details of the object to the user. Abstraction "shows" only the essential attributes and "hides" unnecessary information. It helps to reduce programming complexity and effort.

Let's illustrate **Abstraction** concept with an Example. Suppose you want to create a banking application and you are asked to collect all the information about your customer. There are chances that you will come up with following information about the customer:

<p align="center">
    <img width="200" src="images/Abstraction_01.png">  
    *Abstraction in OOP* 
</p>

But, not all of the above information is required to create a banking application. So, you need to select only the useful information for your banking application from that pool. Data like name, address, tax information, etc. make sense for a banking application.

Since we have fetched/removed/selected the customer information from a larger pool, the process is referred as Abstraction.

There are also the different levels of Abstraction and it's good practice that classes/methods should interact with other classes/methods with the same level of abstraction or higher level of abstraction. As you increase the level of Abstraction, things start getting simpler and simpler because you leave out details.

When the object data is not visible to the outer world, it creates data abstraction.

<p align="center">
    <img width="400" src="images/Abstraction_02.png">  
    *Data Abstraction in OOP* 
</p>

We don't need to provide details about all the methods of an object. When we hide the internal implementation of the different functions involved in a user operation, it creates process abstraction.

Abstraction hides complexity by giving you a more abstract picture, a sort of 10,000 feet view, while Encapsulation hides internal working so that you can change it later. In other words, Abstraction hides details at the design level, while Encapsulation hides details at the implementation level.

For example, when you first describe an object, you talk in more abstract term e.g. a Vehicle which can move, you don't tell how Vehicle will move, whether it will move by using tires or it will fly or it will sell. It just moves. This is called Abstraction. We are talking about a most essential thing, which is moving, rather than focusing on details like moving in plane, sky, or water.

<p align="center">
    <img width="400" src="images/Abstraction_03.png">  
    *Proses Abstraction in OOP* 
</p>

**What I've learned:** 

> **Abstraction** is about hiding unwanted details while giving out most essential details.
> **Abstraction** lets you focus on what the object does instead of how it does.
> **Abstraction** is displaying only essential information and hiding the details. Data abstraction refers to providing only essential information about the data to the outside world, hiding the background details or implementation.

## Afternoon Challenges  

*Practice pairing and Test-Driven development.*  
**"Oystercard Challenge"**

**Plan:** Pair with Ellis and keep working on the afternoon challenge for the week - *"Oystercard Challenge".*

**Process:**

- Recap and compare code before start.
- Write up a plan for how you will interact with your code and manually test in IRB.
- Test drive the creation of a Station class that exposes a name and a zone variable.
```rb
subject { described_class.new(name: "Kings cross", zone: 1)}
```
```rb
  it 'knows its name' do                      
    expect(subject.name).to eq("Old Street")              
  end 
```
- Use only one expectation per test.

**What I've Learned:**

>  Use multiple describe blocks to group tests. That keeps tests more organized and in order. That as well helps to extract some code in to **before** block that keeps tests more readable.

```
  describe '#touch_out' do
    before do 
      subject.touch_in entry_station
      subject.touch_out exit_station
    end

    it 'should set entry station to nil' do
      expect(subject.entry_station).to eq nil
    end
  ...//...
  end
```

## Daily Goals 
### Friday 24 of April 2020

## Morning Goals 

**Dependency injection**. What it is and where it is used.

**Plan:**

- Perform research online individually.  
- Describe what **Dependency injection** is and it's usages. 
- Summarize and give some practical example. 
  
**Process:** 

**Use dependency injection to test classes in isolation**

Dependency injection is a technique for helping you test classes in isolation. It allows a class to use either its real dependency, or a double.

Consider this code:

```rb
class Greeter
  def initialize(smiley = Smiley.new)
    @smiley = smiley
  end

  def greet
    "Hello #{@smiley.get}"
  end
end

class Smiley
  def get
    ":)"
  end
end
```
And then test both like this:
```rb
# greeter_spec.rb

describe Greeter do
  describe "#greet" do
    it "prints a message and a smiley" do
      smiley_double = double :smiley, get: ":D"
      greeter = Greeter.new(smiley_double)
      expect(greeter.greet).to eq "Hello :D"
    end
  end
end

# smiley_spec.rb
describe Smiley do
  describe "#get" do
    it "returns a smiley" do
      smiley = Smiley.new
      expect(smiley.get).to eq ":)"
    end
  end
end
```
This is called dependency injection. Instead of hard coding the dependency, we 'inject' it into the class via the initializer.

**What I've learned:** 

> As per example above we now can test class in isolation by injecting other class as a double. That ensures that tests wont fail and wont be dependent on other class having bug. 
```rb
smiley_double = double :smiley, get: ":D"
```

## Afternoon Challenges  

**Plan:** Pair with Marija and keep working on the afternoon challenge for the week - *"Oystercard Challenge".*

**Process:**

- Recap previous days progress and compare code.
- Next steps involved to extract some methods and functionality from *Oystercard* class to *Journey* class. To approach it needed to re draw/came up with **Domain model** that will represent relationship between classes.

Card | Journey | Station
:---: | :---: | :---: 
@journey | @journeys | @name
@fare | | @zones
@balance | |
`--------` | `--------` | `--------` 
#top_up | #completed? |
#tap_in | #calculate_fare |
#tap_out | |

- Come up a plan for how you will interact with your code and manually test in IRB.
- Re factor test suite to reflect a new Journey class.
- Create a new class Journey and move some the functionality that relates to a journey from **Oystercard to Journey**.
- Make sure all tests pass, all existing functionality is preserved.

**What I've Learned:**

> **Domain Modeling** is an important aspect of OOP  
- The Domain Model is your organized and structured knowledge of the problem. The Domain Model should represent the vocabulary and key concepts of the problem domain and it should identify the relationships among all of the entities within the scope of the domain.
- A domain model is a visual representation of conceptual classes or real-world objects in a domain of interest.
  
## Weekend Challenge

**Takeaway Challenge:** Full path to the project on [GitHub](https://github.com/EdAncerys/takeaway-challenge)

Weekend challenge project been a good way of recapping progress that been made over the week. It brought back some confidence and reassurance of what been learned over the week. 

**Takeaway challenge** to start of been approached by coming up with *Domain Model* for it. That gave structure and plan of how app should look like and functionality/data flow. 

**Focus** over doing this project: 
- Better understanding of relationships between classes and how they interact with each other.   
- Using **doubles** and mocking class. Testing them in **isolation**.
- **RSpec** syntax 

#### Domain Model for Takeaway app

TakeAway | Kitchen | Menu | Text 
:---: | :---: | :---: | :---:
 | @order  |   | @number
 | @checkout| | @body
 `----------` | `----------` | `----------` | `----------` 
#menu() | #order() | #menu() | #send_text()
#order() | #order_total() | #print() | 
#checkout() | #complete?() | |

#### User Stories

```
As a customer
So that I can check if I want to order something
I would like to see a list of dishes with prices

As a customer
So that I can order the meal I want
I would like to be able to select some number of several available dishes

As a customer
So that I can verify that my order is correct
I would like to check that the total I have been given matches the sum of the various dishes in my order

As a customer
So that I am reassured that my order will be delivered on time
I would like to receive a text such as "Thank you! Your order was placed and will be delivered before 18:52" after I have ordered
```


**What I've Learned:**
> Context blocks in **RSpec** is handy way of keeping your documentation well organized. 

> Contexts are a powerful method to make your tests clear and well organized. In the long term this practice will keep tests easy to read.
```rb
context 'order cart' do
  it 'be empty at start' do
    expect(kitchen.order_cart.empty?).to be true
  end
end
```
> Mocking behavior of of the other classes allows us to perform **RSpec** tests in isolation.
```rb
context 'instance variables' do
  it 'responds to Menu_class double' do
    allow(subject).to receive(:menu) { menu_class }
    expect(subject.menu).to eq menu_class
  end
end
```
- Instance variable @menu responds to double of Menu class.

<br>

***

<br>


# Weekend Reflections

### Did you meet all of your goals you set at the start of the week?
- Unit test classes in isolation using mocking is till need some exploring and practicing.

### What things do you still need to work through?
- RSpec Mocking and doubles

### What would you change/improve to keep moving forward?
##### Technical: 
- Domain Modeling and implementation.
- still need to work on approach to the main problem, making sure I'm breaking them down significantly before approaching with solution.

##### Personal:
- Set achievable goals and PLAN !

### A pat on the back
- Made a progress in understanding of **RSpec**
- Have better day plan routine and strategy.  

<br>
  