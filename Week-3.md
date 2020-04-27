# Week 3 Goals 

#### By the end of the week all developers can:

- Build a simple web app
- Follow an effective debugging process for web applications
- Explain the basics of how the web works (e.g. request/response, HTTP, HTML, CSS)
  Explain the MVC pattern

## Daily Goals 
### Monday 27 of April 2020

## Morning Goals 

Attend *Week 3* kick of class.

**Plan:**

Break down weekly goals to focus on this week.

**Process:** 

Analise and go through the main Web concepts and skills: 

- The relationship between a client and a server.
- How HTTP is used to send information over the web.
- RESTful APIs.
- The request/response cycle.
- Web templating with HTML/CSS.

## Morning Goals 

The relationship between a client and a server. How HTTP is used to send information over the web.

**Plan:**

- Perform research on-line individually.  
- Describe what **server-client** relationship is and how **HTTP** is used. 
- Summarize and give some practical example. 
  
**Process:** 

The *World Wide Web* is an information space made up of two chief components: resources (mostly stored on servers), and the entities that request those resources (usually called clients).

The whole **Web** is built on **client-server** relationships. There are different kinds of **clients** and **servers** but the relationship is roughly the same: the client is dependent on the server for providing and managing information. Anything that can request a resource from a server can be called a client.

<p align="center">
    <img width="250" src="images/Client-Server_01.png">  
    *Client-Server relationship* 
</p>

**HTTP** or *Hypertext Transfer Protocol* is a protocol which allows the fetching of resources, such as HTML documents. It is the foundation of any data exchange on the Web and it is a client-server protocol, which means requests are initiated by the recipient, usually the Web browser. A complete document is reconstructed from the different sub-documents fetched, for instance text, layout description, images, videos, scripts, and more.

#### Components of HTTP-based systems

**Client: the user-agent**

The user-agent is any tool that acts on the behalf of the user. This role is primarily performed by the Web browser; other possibilities are programs used by engineers and Web developers to debug their applications.

The browser is **always** the entity initiating the request. It is never the server (though some mechanisms have been added over the years to simulate server-initiated messages).

<p align="center">
    <img width="400" src="images/HTTP_Request_01.png">  
    *Client-Server relationship* 
</p>

**The Web server**

On the opposite side of the communication channel, is the server, which serves the document as requested by the client. A server appears as only a single machine virtually: this is because it may actually be a collection of servers, sharing the load (load balancing) or a complex piece of software interrogating other computers (like cache, a DB server, or e-commerce servers), totally or partially generating the document on demand.

<p align="center">
    <img width="400" src="images/HTTP_Response_01.png">  
    *Client-Server relationship* 
</p>

**Proxies**

Between the Web browser and the server, numerous computers and machines relay the HTTP messages. Due to the layered structure of the Web stack, most of these operate at the transport, network or physical levels, becoming transparent at the HTTP layer and potentially making a significant impact on performance. Those operating at the application layers are generally called proxies. 

**What I've learned:** 

**HTTP** is an extensible protocol that is easy to use. The client-server structure, combined with the ability to simply add headers, allows HTTP to advance along with the extended capabilities of the Web.

## Afternoon Challenges  

*Practice pairing and building Web-app.*  
**"Battle Challenge"**

**Plan:** Pair with Hibo and keep working on the afternoon challenge for the week - *"Battle".*

**Process:**

- Reflect on documentation and get familiar with following: *The Web, HTTP, HTTP parameters, HTTP verbs.*
- Sinatra: Getting started. As basic web framework, Sinatra, that can receive and respond to HTTP requests. Set up and run Sinatra from within your own computer.
- Sinatra: Defining a route
```rb
require 'sinatra'
get '/' do
  'hello!'
end
```
- Sinatra: Start and restart server to render different information.
- Sinatra: Returning HTML. Placing a **"string"** in a block to render view.
```rb
get '/home' do
  "<h1>Hello World</h1>"
end
```
- Sinatra: Views. Can render partial by passing to the block `erb(:index)`
- Sinatra: ERB. Ruby Expression using `<%= %>` ('ERB tags')
- Sinatra: Keeping views clean. Making sure our file that renders *view* only have elements that related and do not have any logic/functions. **SRP !!!**
- Sinatra: Introducing `params`. Thats information passed in form of **hash** as **key-value** pair to servers `/home path: ?name=James`
- Sinatra: Using forms. Instead of letting user to interact  via URL bar we can allow our users to interact with our app via a `<form>` element. 
```rb
form.erb # View partial 
  <form name="input" action=“/form” method=“post”>
  username: <input type=“text” name=“username”>
  password: <input type=“password” name=“password”>

  <input type=“submit” value=“Submit”>
  </form>
```

**What I've Learned:**

> **Sinatra: Defining a route**. We can handle/define and setup routes by the request path ** /. / **. Browser is making a request using a path for which your server has route setup. When a server receives a request along with a path, it activates a particular route.  
> **Sinatra** gem basic web framework that can receive and respond to HTTP requests.  
> **Sinatra: Views**. How to set up view partials that helps to render views for web apps. 




















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
