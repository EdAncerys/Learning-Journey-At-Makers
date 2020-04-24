

## Daily Goals 
### $$$$$$ of April 2020

## Morning Goals 

*Object-orientated principles (OOP)* - **Polymorphism**. 

**Plan:**

- Perform research on-line individually.  
- Describe what **Polymorphism in OO is** and it's usages. 
- Summarize and give some practical example. 
  
**Process:** 

Polymorphism is a made up of two words Poly which means Many and Morph which means Forms. So Polymorphism is a method where one is able to execute the same method using different objects. In polymorphism, we can obtain different results using the same method by passing different input objects. 

Generally, **Polymorphism** is the ability to appear in many forms. In object-oriented programming, polymorphism refers to a programming language's ability to process objects differently depending on their data type or class. More specifically, it is the ability to redefine methods for derived classes. For example, given a base class shape, polymorphism enables the programmer to define different area methods for any number of derived classes, such as circles, rectangles and triangles. No matter what shape an object is, applying the area method to it will return the correct results. Polymorphism is considered to be a requirement of any true object-oriented programming language (OOPL).

In Polymorphism, classes have different functionality but they share common interference. The concept of polymorphism can be studied under few sub categories.

- Polymorphism using Inheritance
- Polymorphism using Duck-Typing

**Polymorphism using inheritance** Inheritance is a property where a child class inherits the properties and methods of a parent class. One can easily implement polymorphism using inheritance. It can be explained using the following *example:*

```rb
    # Ruby program of Polymorphism using inheritance 
    class Vehicle 
      def tyreType 
        puts "Heavy Car"
      end
    end
   
    # Using inheritance  
    class Car < Vehicle 
      def tyreType 
        puts "Small Car"
      end
    end
   
    # Using inheritance  
    class Truck < Vehicle 
      def tyreType 
        puts "Big Car"
      end
    end

# Creating object  
vehicle = Vehicle.new
vehicle.tyreType() # Outputs "Heavy car"
   
# Creating different object calling same function  
vehicle = Car.new
vehicle.tyreType() # Outputs "Small car" 
   
# Creating different object calling same function  
vehicle = Truck.new
vehicle.tyreType() # Outputs "Big car" 
```

**Polymorphism using Duck-Typing** In Ruby, we focus on the object’s capabilities and features rather than its class. So, Duck Typing is nothing but working on the idea of what an object can do rather than what it actually is. Or, what operations could be performed on the object rather than the class of the object.
Here is a small program to represent the before mentioned process.
*Example:*

```rb
# Ruby program of polymorphism using Duck typing 
# Creating three different classes 
class Hotel 
   
  def enters 
    puts "A customer enters"
  end
   
  def type(customer) 
    customer.type 
  end
   
  def room(customer) 
    customer.room 
  end
   
end
   
# Creating class with two methods  
class Single 
   
  def type 
    puts "Room is on the fourth floor."
  end
   
  def room 
    puts "Per night stay is 50£"
  end
   
end
   
   
class Couple 
   
 # Same methods as in class single 
  def type 
    puts "Room is on the second floor"
  end
   
  def room 
    puts "Per night stay is 80£"
  end
   
end
   
# Creating Object 
# Performing polymorphism  
hotel= Hotel.new
puts "This visitor is Single."
customer = Single.new
hotel.type(customer) # Outputs "Room is on the fourth floor"
hotel.room(customer) # Outputs "Per night stay is 50£"
   
   
puts "The visitors are a couple."
customer = Couple.new
hotel.type(customer) # Outputs "Room is on the second floor"
hotel.room(customer) # Outputs "Per night stay is 80£"
```

**What I've learned:** 

> In OOP **Polymorphism** is an ability to created a variable, method or an object that have more than one form.
