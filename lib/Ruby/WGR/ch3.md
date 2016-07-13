# 3) Organizing objects with classes

Defining a class lets you group behaviours (methods) into convenient bundles, so that you can quickly create many objects that behave essentially the same way. 
 
Everything you handle in Ruby is either an object or a construct that evaluates to an object, and every object is an instance of some class. This fact hold true even where it might first seem a little old. Integres are instances of class, and the classes themselves are objects.

### 3.1) Classes and instances

Classes usually exist for the purpose of being *instantiated* -that is, of having objects created that are instances of the class.

You have seen instantiation in cation before: `obj = Object.new`

The `new` method is a *constructor*: a method whose purpose it to manufature and return to you a new instance of the class, a newly mindted object.

You define a class with the `class` keyword. Classes are named with *constants*, a special type of identifier recognizable by the fact that it begins with a capital letter. Constants are used to store information and values that don't change over the course of a program run.

#### 3.1.1) Instance methods

Methods defined inside a class and intended for use by all instances of the class, are called *instence* methods. They don't belong only to one object. Instead, any instance of the class can call them.

> Methods that you define for one particular object -as in `def ticket.price`- are called *singleton methods*.

### 3.2) Instance variables and object state

Information and data associated with a particular object embodies the *state* of the object. We need to be able to do the following:

* Set, or reset, the state of an object (say to a ticket, "You cost $11.99.").
* Read back the state (ask a ticket, "How much do you cost?").

Conveniently, Ruby objects come with their own storage and retrieval mechanisim for values: *instance variables*.

The instance variable enables individual objects to remember state. Instance variables work much like other variables: you assign values to them, and you read those values back; you can add them together, print them out, and so on. But instance variables have few differences:

* Instance variable names always start with a single @ (at sign). This enables you to recognize an instance variable at glance.
* Instance variables are only visible to the object to which they belong.
* An instance variable initialized in one method inside a class can be used by any method defined within that class.
 
Unlike a local variable, the instance variable retains the value assigned to it even after the method in which it was initialized has terminated. This property of instance variables -their survival across method calls- makes them suitable for maintaining state in an object.

#### 3.2.1.) Initializing an object with state

When you write a class, you can, if you wish, define a special method called `initialize`. If you do so, that method will be executed every time you create a new instance of the class.

You can employ this automatic initialization process to set an object's state at the time of the object's creation.

```ruby
class Ticket
  def initialize(venue, date)
    @venue = venues
    @date = date
  end
  
  def venue
    @venue
  end
  
  def date
    @date
  end
end
```

> The names of the instance variables, methods and arguments to `initialize` don't have to match. You could use `@v` instead of `@venue` for example to store the value passed in the argument `venue`. You could call the second method `event_date` and still use `@date` inside it. Still, it's usually good practice to match the names to make it clear what goes with what.

This opens up our prospects immensely. We can create, manipulate, compare, and examine any number of tickets at the same time, without having to write separate methods for each of them. All the tickets share the resources of `Ticket` class. At the same time, each ticket has its own set of instance variables to store state information.

### 3.3) Setter methods

When you need to set or change an object's state at some point in your program other than the `initalize` method, the heart of the matter is assigning (or reassigning) values to instance variables. 

```ruby
class Ticket
  def initialize(venue, date)
    @venue = venues
    @date = date
  end
  
  def price=(price)
    @price = price
  end
  
  def venue
    @venue
  end
  
  def date
    @date
  end
  
  def price
    @price
  end
end
```

> Setter methods don't return what you might think. When you use the syntactic sugar that lets you make calls to = methods that look like assignments, Ruby takes the assignment semantics seriously. Assignments (like `x = 1`) evaluate to whatever's on their right-hand side. Methods usually return the values of the last expression evaluated during execution. But = method calls behave like assignments: the values of the expression `ticket.price = 63.00` is `63.00`, even if the `ticket=` method return the string `"Ha ha!"`. The idea is to keep the semantics consistent. Under the hood, it's a method call; but it looks like an assignment and behaves like an assignement with respect to its value as an expression.

### 3.4) Attributes and the attr_* method family

An *attribute* is a property of an object whose value can be read and/or written through the object. In the case of ticket object, we'd say that each ticket has a `price` attribute as well as a `date` attribute and a `venue` attribute. Our `price=` method can be described as an *attribute write* method. `date`, `venue` and `price` (without the equal sign) are *attribute reader* methods. (The write/read terminology is equivalent to the set/get terminalogy used earlier, but the write/read is more common in Ruby discussions.)

The attributes of Ruby objects are implemented as reader and/or write methods wrapped around instance variables -or, if you prefer, instance variables wrapped up in reader and/or writer methods. There's no separate "attribute" construct at the language level. *Attribute* is a high-level term for a particular configuration of methods and instance variables. But it's a useful term, and Ruby does embed the concept of attributes in the language, in the form of shortcuts that help you write methods that implement them.

Ruby provides a built-in shortcut that automatically creates a method that reads and returns the value of the instance variable with the same name as the method (give or take an @):

```ruby
class Ticket
  attr_reader :venue, :date, price
end
```

The elements that start with colons (:`venue`,and so on) are *symbols*. Symbols are a kind of naming or labeling facility. They're cousin of strings, although not quite the same thing,

> `self` as default receiver
>
> You're seeing more method calls without an explicit receiver; there's no left-hand object and no dot in `attr_reader`, for example. In the absence of an explicit receiver, messages go to `self` the default object. In the topmost level of a class definition body, `self` is the class object itself. So the object receiving the `attr_reader` message is the actual class object `Ticket`.

| Method name | Effect | Example | Rquivalent code |
|-------------|--------|---------|-----------------|
| `attr_reader` | Creates a reader method | `attr_reader :venue` | `def venue; @venue; end` |
| `attr_writer` | Creates a writer method | `attr_write :price` | `def price=(price); @price = price; end` |
| `attr_accessor` | Creates reader and writer methods | `attr_accessor :price` | `def price=(price); @price = price; end` `def price; @price; end` |

### 3.5) Inheritance and the Ruby class hierarchy


