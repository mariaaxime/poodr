# Practical Object-Oriented Design in Ruby

## 1. Object-Oriented Design

### 1.1. In Praise of Design

> The programming techniques that make code a joy to write overlap with those that most efficiently produce software.

#### 1.1.1. The Problem Design Solves

Applications are constantly changing. They need to be flexible and adaptable. 

#### 1.1.2. Why Change is Hard

Object-oriented applications are made of objects that pass messages between them. These interactions create dependencies. 


Object-oriented design is about _managing dependencies_. When objects know too much about each other, changing one of them requires changing all of them.

#### 1.1.3. A Practical Definition of Design

Every problem has two components. Writing code for the feature you're building and writing code that's amenable to be changed later.


When designing for the future you shouldn't do it thinking about specific requirements. The purpose of design is to allow you to do design later, and its primary goal is to reduce the cost of change.

### 1.2. The Tools of Design

#### 1.2.1. Design Principles

- **S**ingle Responsibility
- **O**pen-Closed
- **L**iskov Substitution
- **I**nterface Segregation
- **D**ependency Inversion

> The principles of good design represent measurable truths.

#### 1.2.2. Design Patterns

Patterns: Simple and elegant solutions to specific problems in object-oriented software design that you can use to make your own designs more flexible, modular, reusable and understandable.


Applying patterns to the wrong problem is not fault of the pattern itself.

> A tool cannot be faulted for its use; the user must master
the tool.

### 1.3. The Act of Design

#### 1.3.1 How Design Fails

The first way design fails is due to lack of it.

> The syntax of the Ruby language is so gentle that anyone blessed with the ability to string thoughts into logical order can produce working applications.

_Undesigned_ applications carry the seeds of their own destruction; they are easy to write but gradually become impossible to change.


More experienced programmers are aware of OOD techniques but do not yet understand how to apply them. They fall into the trap of _overdesign_: applying principles inappropriately and seeing patterns when none exist.


Object-oriented software fails when the act of design is separated from the act of programming. Design relies on a feedback loop that should be timely and incremental (iterative techniques). When design is dictated from afar, none of the necessary adjustments can occur and early failures of understanding get cemented into the code.

#### 1.3.2. When to Design

Big Up Front Design (BUFD) leads to an adversarial relationship between customers and programmers. The requirements are constantly changing and your application is not capable of changing at the same pace. 

> If you cannot write well-designed code, you'll have to rewrite your application during every iteration.

#### 1.3.3. Judging Design

There are numerous Ruby gems that asses how well your code follows OOD principles. Metrics software works by scanning source code and counting things that predict quality. Running a metrics suite against your own code can be illuminating, humbling, and sometimes alarming. Seemingly well-designed applications can rack up impressive numbers of OOD violations.

> OOD metrics cannot identify designs that do the wrong thing in the right way.

The ultimate software metric would be _cost per feature over the time interval that matters_. If lack of a feature will force you out of business today, it doesn't matter how much it will cost to deal with the code tomorrow; you must do the best you can in the time you have. Making this kind of design compromise is known as taking on _technical debt_.

> When the act of design prevents software from being delivered on time, you have lost. Delivering half of a well-designed application might be the same as delivering no application at all.

### 1.4. A Brief Introduction to Object-Oriented Programming

#### 1.4.1. Procedural Languages

Variables: names with associated data. The data type is known and you know what to do with it (append to strings, do math with numbers, index into arrays, etc).


In this language, data is one thing and behavior is something completely different. Data gets packaged up into variables and then passed around to behavior, which could, frankly, do anything to it.

#### 1.4.2. Object-Oriented Languages

Instead of dividing data and behavior, they are a single thing: an object. Objects have behavior and may contan data, data to whick they alone control access. Objects invoke one another's behavior by sending each other messages.


OO languages don't limit you to a small set of built-in types and pre-defined operations; you can invent brand new types of your own.

### 1.5. Summary

> If an application lives long enough, that is, if it succeeds, its biggest problem will become that of dealing with change.

The most visible elements of design are principles and patterns, but unfortunately even applying principles correctly and using patterns appropriately does not guarantee the creation of an easy-to-change application.

> Design relies on your ability to translate theory into practice.

## 2. Designing Classes with a Single Responsibility

> Anyone can arrange code to make it work right now. Creating an easy-to-change application, however, is a different matter.

### 2.1. Deciding What Belongs in a Class

The problem is not one of technical knowledge but of organization, you know how to write the code but not where to put it.

#### 2.1.1. Grouping Methods into Classes

> Design is more the art of preserving changeability that it is the act of achieving perfection.

#### 2.1.2. Organizing Code to Allow for Easy Changes

Code that's easy to change means:

- changes have no unexpected side effects
- small changes in requirements require correspondingly small changes in code
- existing code is easy to reuse
- the easies way to make a change is to add code that in itself is easy to change

To achieve that the code should have the following qualities:

- **Transparent**: The consequences of change should be obvious in the code that is hanging and in distant code that relies upon it
- **Reasonable**: The cost of any change should be proportional to the benefits the change achieves
- **Usable**: Existing code should be usable in new and unexpected contexts
- **Exemplary**: The code itself should encourage those who change it to perpetuate these qualities

### 2.2. Creating Classes that have a Single Responsibility

A class should do the smallest possible useful thing.

#### 2.2.1. An Example Application: Bicycles and Gears

A class consists of everything it directly implements plus everything it inherits.

#### 2.2.2. Why Single Responsibility Matters

> An application that is easy to change is like a box of building blocks; you can select just the pieces you need and assemble them in unanticipated ways.

A class that has more than one responsibility is difficult to reuse. The responsibilities are entangled within the class. If you want to reuse some of its behavior, it's impossible to get just the parts you need.


You could duplicate the code you need, but **that's a terrible idea**. It leads to additional maintenance and increases bugs.

> You increase your application's chance of breaking unexpectedly if you depend on classes that do too much.

#### 2.2.3. Determining if a Class has a Single Responsibility

- Interrogate the class. If you rephrase every one of its methods as a question, asking the question ought to make sense
- Attempt to describe what the class does in a sentence. If the simplest description you can devise uses the word 'and', the class likely has more than one responsibility. If it uses the word 'or', the class has more than one responsibility and they're not even related

When everything in a class is related to its main purpose, the class is _highly cohesive_.

> A class has responsibilities that fulfill its purpose.

Single Responsibility Principe doesn't mean that the class does one very narrow thing. It requires that the class is cohesive, that everything it does is highly related to its purpose.

#### 2.2.4. Determining when to make Design Decisions

> When the future cost of doing nothing is the same as the current cost, postpone the decision.

> For better or for worse, the patterns you establish today will be replicated forever.

Other developers believe that your intentions are reflected in the code; when the code lies, you must be alert to programmers believing and then propagating that lie.


A good designer understands the tension between 'improve it now' vs 'improve it later' and minimizes costs by making informed tradeoffs between the needs of the present and the possibilities of the future.

### 2.3. Writing Code that Embraces Change

> Because change is inevitable, coding in a changeable style has big future payoffs. Coding in these styles will improve your code, today, at no extra cost.

#### 2.3.1. Depend on Behavior, Not Data

Don't Repeat Yourself (DRY) code tolerates change because any change in behavior can be made by changing code in just one place.

##### Hide Instance Variables

Always wrap instance variables in accessor methods instead of directly referring to variables. Implementing this method (`attr_reader`) changes the variable from data (which is referenced all over) to behavior (which is defined once). You could make the `attr_reader` private.


You should hide data from yourself to protect the code from being affected by unexpected changes. 

_Don't_

```ruby
class Gear
  def initialize(chainring, cog)
    @chainring = chainring
    @cog = cog
  end

  def ratio
    @chainring / @cog.to_f # <-- road to ruin
  end
end
```

_Do_
```ruby
class Gear
  def initialize(chainring, cog)
    @chainring = chainring
    @cog = cog
  end

  def ratio
    chainring / cog.to_f # <-- road to ruin
  end
  
  private
  
  attr_reader :chainring, :cog
end
```

##### Hide Data Structures

Avoid code that depends upon the data structure. If that structure changes, then the code must change.
Direct references into complicated structures are confusing, because they obscure what the data really is, and they are a maintenance nightmare, because every reference will need to be changed when the structure of the data changes.
You can use a `Struct` to separate structure from meaning. This style of code allows you to protect against changes in externally owned data structures and to make your code more readable and intention revealing.

> Although it might be easier to just have an array of Wheels to begin with, it is not always possible. If you can control the input, pass in a useful object, but if you are compelled to take a messy structure, hide the mess even from yourself.

_Don't_

```ruby
class ObscuringReferences
  attr_reader :data
  
  def initialize(data)
    @data = data
  end
  
  def diameters
    # 0 is rim, 1 is tire
    data.collect {|cell| cell[0] + (cell[1] * 2)}
  end
end
```

_Do_
```ruby
class RevealingReferences
  attr_reader :wheels
  
  def initialize(data)
    @wheels = wheelify(data)
  end
  
  def diameters
    wheels.collect{|wheel| wheel.rim + (wheel.tire * 2)}
  end
  
  Wheel = Struct.new(:rim, :tire)
  
  def wheelify(data)
    data.collect {|cell| Wheel.new(cell[0], cell[1])}
  end
end
```

#### 2.3.2. Enforce Single Responsibility Everywhere

##### Extract Extra Responsibilities from Methods

Methods should have a single responsibility, to make them easy to change and easy to reuse.

_Don't_

This method has two responsibilities: iterating and calculating the diameter

```ruby
def diameters
  wheels.collect{|wheel| wheel.rim + (wheel.tire * 2)}
end
```

_Do_

```ruby
def diameters
  wheels.collect{|wheel| diameter(wheel)}
end

def diameter(wheel)
  wheel.rim * (wheel.tire * 2)
end
```

> You don't have to know where you're going to use good design practices to get there.

Methods that have a single responsibility confer the following benefits:

- **Expose previous hidden qualities**: having each method serve a single purpose makes the set of things the class does more obvious
- **Avoid the need for comments**: if a bit of code inside a method needs a comment, extract that bit into a separate method and the new method will serve the same purpose as did the old comment
- **Encourage reuse**: other programers will reuse small methods instead of duplicating the code
- **Are easy to move to another class**: you can rearrange behavior without doing a lot of method extraction and refactoring

##### Isolate Extra Responsibilities in Classes

You can create a new class or you can create a Struct inside of the current class to isolate extra responsibilities.

> Because you are writing changeable code, you are best served by postponing decisions until you are absolutely forced to make them. Any decision you make in advance of an explicit requirement is just a guess. Don’t decide; preserve your ability to make a decision later.

If you have a muddled class with too many responsibilities, separate those into different classes.


If you identify extra responsibilities that you can't yet remove, isolate them.

#### 2.4. Finally, the Real Wheel

> The code is not perfect, but in some ways, it achieves a higher standard: it is good enough.

#### 2.5. Summary

> The path to changeable and maintainable object-oriented software begins with classes that have a single responsibility. 


## 3. Managing Dependencies

There are three ways for an object to invoke some bit of behavior:

- Knowing it personally
- Inheriting it
- Knowing another object who knows it

Well-designed objects have a single responsibility, so their nature is to collaborate to accomplish complex tasks. To collaborate, an object must know something about others. _Knowing_ creates a dependency.

### 3.1. Understanding Dependencies

An object depends on another object if, when one object changes, the other might be forced to change in turn.


Take a look at this code:

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
    @rim = rim 
    @tire = tire
  end

  def gear_inches
    ratio * Wheel.new(rim, tire).diameter
  end

  def ratio
    chainring / cog.to_f
  end
  # ...
end

class Wheel
  attr_reader :rim, :tire
    
  def initialize(rim, tire)
    @rim = rim
    @tire = tire
  end
    
  def diameter
    rim + (tire * 2)
  end
  # ...
end

puts Gear.new(52, 11, 26, 1.5).gear_inches # => 137.0909090909091
```

#### 3.1.1. Recognizing Dependencies

The class `Gear` has at least four dependencies on `Wheel`

1. The name of the class. `Gear` expects a class named `Wheel` to exist
2. The name of the message that it intends to send to someone other than `self`. `Gear` expects a `Wheel` instance to respond to `diameter`
3. The argument that a message requires. `Gear` know that `Wheel.new` requires a `rim` and a `tire`
4. The order of those arguments. `Gear` knows that `Wheel` takes positional arguments and that the first one should be `rim` and the second `tire`

There's some degree of dependency between those two classes as they need to collaborate, but unnecessary dependencies make the code less reasonable. These dependencies turn minor tweaks into major undertakings where small changes cascade through the application, forcing many changes.

> A class should know just enough to do its job and not one thing more.

#### 3.1.2. Coupling Between Objects (CBO)

These dependencies _couple_ `Gear` to `Wheel`. 


The more tightly coupled two objects are, the more they behave like a single entity. When two or more objects are so tightly coupled that they behave as a unit, it's impossible to reuse just one. Changes to one object force changes to all.

#### 3.1.3. Other Dependencies

- An object knows another who knows another who knows something. This is the magnified version of 'Knowing the name of the message that it intends to send to someone other than `self`'. Message chaining created a dependency between the original object and every object and message along the way to its ultimate target.
- Tests depending on code. If you write tests that are too tightly couple to code, they will break every time the code is refactored, even when the fundamental behavior does not change. These couplings are dependencies that cause changes to the code to cascade into the tests, forcing them to change in turn.

### 3.2. Writing Loosely Coupled Code

> Reducing dependencies means recognizing and removing the ones you don't need.

#### 3.2.1. Inject Dependencies

Referring to another class by its name creates a dependency.


When `Gear` hard-codes a reference to `Wheel` inside its `gear_inches` method, it is explicitly declaring that it is only willing to calculate gear inches for instances of `Wheel`. `Gear` refuses to collaborate with any other kind of object, even if that object has a diameter and uses gears.

> It it not the class of the object that's important, it's the message you plan to send to it.

Instead of being glued to `Wheel`, this next version of `Gear` expects to be initialized with an object that can respond to `diameter`:

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, wheel)
    @chainring = chainring
    @cog = cog
    @wheel = wheel
  end

  def gear_inches
    ratio * wheel.diameter
  end
# ...
end

# Gear expects a ‘Duck’ that knows ‘diameter’
puts Gear.new(52, 11, Wheel.new(26, 1.5)).gear_inches # => 137.0909090909091
```

`Gear` doesn't know or care that the object might be an instance of class `Wheel`. It only know that it holds an object that responds to `diameter`.


This technique is known as _dependency injection_. Using dependency injection to shape code relies on your ability to recognize that the responsibility for knowing the name of a class and the responsibility for knowing the name of a message to send to that class may belong in different objects.

#### 3.2.2. Isolate Dependencies

> If prevented from achieving perfection, your goals should switch to improving the overall situation by leaving the code better than you found it.

**Isolate Instance Creation**

If you're so constrained that you cannot change the code to inject a `Wheel` into a `Gear`, you should isolate the creation of a new `Wheel` inside the `Gear` class.

- Alternative 1: Move the creation of the new instance of `Wheel` from the `gear_inches` method to `Gear`'s initialization method.

```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, rim, tire)
    @cog = cog
    @wheel = Wheel.new(rim, tire)
    @chainring = chainring
  end
  
  def gear_inches
    ratio * wheel.diameter
  end
  # ...
end

puts Gear.new(52, 11, 26, 1.5).gear_inches # => 137.0909090909091
```

- Alternative 2: Isolate the creation of a new `Wheel` in its own explicitly defined `wheel` method.

```ruby
class Gear
  attr_reader :chainring, :cog, :rim, :tire

  def initialize(chainring, cog, rim, tire)
    @chainring = chainring
    @cog = cog
    @rim = rim
    @tire = tire
  end

  def gear_inches
    ratio * wheel.diameter
  end
    
  def wheel
    @wheel ||= Wheel.new(rim, tire)
  end
  # ... 
end

puts Gear.new(52, 11, 26, 1.5).gear_inches # => 137.0909090909091
```

They reveal dependencies instead of concealing them, lowering the barriers to reuse and making the code easier to refactor when circumstances allow.

**Isolate Vulnerable External Messages**

External messages: Messages that are sent to someone other than `self`.


The `gear_inches` method send `ratio` and `wheel` to `self` but sends `diameter` to wheel.

```ruby
def gear_inches
  ratio * wheel.diameter
end
```

This method depends on `Gear` responding to `wheel` and on `wheel` responding to `diameter`. You can reduce tour chance of being forced to make a change to `gear_inches` by removing the external dependency and encapsulating it in a method of its own.

```ruby
def gear_inches
  ratio * diameter
end

def diameter
  wheel.diameter
end
```

`Gear` now isolates `wheel.diameter` in a separate method, and `gear_inches` can depend on a message sent to `self`.

#### 3.2.3. Remove Argument-Order Dependencies

Many method signatures not only require arguments, but they also require that those arguments be passed in a specific, fixed order.


When a new instance of `Gear` is created, the three arguments must be passed and they must be passed in the correct order.
 
 ```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring, cog, wheel)
    @chainring = chainring
    @cog = cog
    @wheel = wheel
  end
  # ...
end

puts Gear.new(52, 11, Wheel.new(26, 1.5)).gear_inches # => 137.0909090909091
```

**Use Keyword Arguments**

Change the code to take keyword arguments. They may be passed in any order.

 ```ruby
class Gear
  attr_reader :chainring, :cog, :wheel

  def initialize(chainring:, cog:, wheel:)
    @chainring = chainring
    @cog = cog
    @wheel = wheel
  end
  # ...
end

puts Gear.new(cog: 11, chainring: 52, wheel: Wheel.new(26, 1.5)).gear_inches # => 137.0909090909091
```

This technique adds verbosity. It requires the sender and the receiver of a message to state the keyword names. This results in explicit documentation at both ends of the message.
 
 **Explicitly Define Defaults**
 
  ```ruby
 class Gear
   attr_reader :chainring, :cog, :wheel

   def initialize(chainring: 40, cog: 18, wheel:)
     @chainring = chainring
     @cog = cog
     @wheel = wheel
   end
   # ...
 end
 
 puts Gear.new(wheel: Wheel.new(26, 1.5)).chainring # => 40
 ```

It's best to embed simple defaults right in the parameter list, but if getting the default requires running a bit of code, don't hesitate to send a message.

**Isolate Multiparameter Initialization**

Sometimes you don't control the signature of the method that needs to change. You will be forced to depend on a method that requires positional arguments.
 
 
Imagine that `Gear` is part of a framework and that its initialization method requires positional arguments. Imagine also that your code has many places where you must create a new instance of `Gear`. Just as you would DRY out repetitive code inside of a class, DRY out the creation of new `Gear` instances by creating a single method to wrap the external interface.

```ruby
# When Gear is part of an external interface
module SomeFramework
  class Gear
    attr_reader :chainring, :cog, :wheel 

    def initialize(chainring, cog, wheel)
      @chainring = chainring
      @cog = cog
      @wheel = wheel
    end
  # ...
  end
end

# Wrap the interface to protect yourself from changes
module GearWrapper
  def self.gear(chainring:, cog:, wheel:)
    SomeFramework::Gear.new(chainring, cog, wheel) 
  end
end
```

`GearWrapper` is a Ruby module instead of a class. Using a module here lets you define a separate and distinct object to which you can send the `gear` message while simultaneously conveying the idea that you don't expect to have instances of `GearWrapper`. 


_Factories_: Objects whose only purpose is to create instance of some other class.

### 3.3. Managing Dependency Direction

#### 3.3.1. Reversing Dependencies

In our code, `Gear` depends on `Wheel`, but we could've written the code so that `Wheel` depends on `Gear`.

> In an application that constantly changes, the choices you make about the direction of dependencies have far-reaching consequences that manifest themselves for the life of your application.

#### 3.3.2. Choosing Dependency Direction

> Depend on things that change less often than you do.

- Some classes are more likely than other to have changes in requirements
- Concrete classes are more likely to change than abstract classes
- Changing a class that has many dependents will result in widespread consequences

**Understanding Likelihood of Change**

Ruby base classes (`String`, `Array`, ...) always change less often than your own classes, and you can  continue to depend on them without another thought.


You need to assess how mature are the frameworks you use. In general, any framework you use will be more stable than your code, but you could choose a framework whose code changes more often than yours.


Rank evey class used in your application along a scale of how likely it is to undergo a change relative to all other classes. This ranking is one key piece of information to consider when choosing the direction of dependencies.

**Recognizing Concretions and Abstractions**

Concretion: Creating a `Wheel` from the `rim` and `tire` parameters
Abstraction: Passing a `wheel` argument that is a _Duck_ that responds to `diameter`


When you inject `Wheel` into `Gear` such that Gear then depends on a Duck who responds to `diameter`, you are, however casually, defining an interface. This interface is an abstraction of the idea that a certain category of things will have a diameter. 

**Avoid Dependent-Laden Classes**

> A class that, if changed, will cause changes to ripple through the application will be under enormous pressure to _never_ change. Ever. Under any circumstances whatsoever. Your application may be permanently handicapped by your reluctance to pay the price required to make a change to this class.

**Finding the Dependencies That Matter**

Classes vary in their likelihood of change, their level of abstraction, and their number of dependents. 


Each quality matters, but the interesting design decisions occur at the place where likelihood of change intersects with number of dependents.

- Abstract Zone (A): Changes are unlikely but, if they occur, will have broad effects
- Neutral Zone (B): Changes are unlikely and have few side effects
- Neutral Zone (C): Changes are likely but they have few side effects
- Danger Zone (D): These classes WILL change and the changes will cascade into dependents

Zone D classes are the ones that make an application painful to change. You can guarantee that any application will gradually become unmaintainable by making its Zone D classes more likely to change than their dependents.

### 3.4. Summary

- Injecting dependencies creates loosely coupled objects that can be reused
- Isolating dependencies allows objects to quickly adapt to unexpected changes
- Depending on abstractions decreases the likelihood of facing these changes

> Depend on things that change less often than you do.

## 4. Creating Flexible Interfaces

> An object-oriented application is made up of classes but defined by messages.

Design deals with:

* What objects know -> Their responsibilities
* Who they know -> Their dependencies
* How they talk to one another

### 4.1. Understanding Interfaces

You can build two types of applications: 

**Every object may send any message to any other object**

The objects expose too much about themselves and know too much about others. To reuse any you need all, to change one thing you must change everything.


The roots of this problem lie not in what each class does but in what it reveals.

**The objects communicate in specific and well-defined ways**

The objects are pluggable. They reveal as little about themselves, and know as little about others, as possible.


This application has some agreement about which messages may pass between its objects. Each object has a clearly defined set of methods that it expects other to use.

_Public interface_: Made up of the methods of a class that are intended to be used by others.

### 4.2. Defining Interfaces

A class exists to fulfill a single responsibility but implements many methods. These methods vary in scale and granularity and range from broad, general methods that expose the main responsibility of the class to tiny utility methods that are only meant to be used internally. Some of them should be public; others deal with internal implementation details and are private.

#### 4.2.1. Public Interfaces

The methods that make up the public interface:

* Reveal its primary responsibility
* Are expected to be invoked by others
* Will not change on a whim
* Are safe for others to depend on
* Are thoroughly documented in the tests

#### 4.2.2. Private Interfaces

All other methods in the class. They:

* Handle implementation details
* Are not expected to be sent by other objects
* Can change for any reason
* Are unsafe for others to depend on
* May not even be referenced in the tests

#### 4.2.3. Responsibilities, Dependencies and Interfaces

There is a correspondence between the statements you make about the specific responsibilities of a class and the class' public methods. Public methods should read like a description of responsibilities. 
 
> The public interface is a contract that articulates the responsibilities of your class.

The public methods are stable and the private methods are changeable. When you mark methods as public or private, you tell users of your class upon which methods they may safely depend.

### 4.3. Finding the Public Interface

#### 4.3.1. An Example Application: Bicycle Touring Company

_Use case_: A customer, in order to choose a trip, would like to see a list of available trips of appropriate difficulty, on a specific date, where rental bicycles are available.

#### 4.3.2. Constructing an Intention

_Domain objects_: Nouns in the application that have both data and behavior.


Domain objects are easy to find, but they are not at the design center of your application. Design experts notice domain objects without concentrating on them; they focus not on these objects but on the messages that pass between them.

#### 4.3.3. Using Sequence Diagrams

Sequence diagrams provide a simple way to experiment with different object arrangements and message-passing schemes.
They specify the messages that pass between objects, and because objects should communicate using public interfaces, sequence diagrams are a vehicle for exposing, experimenting with, and ultimately defining those interfaces.
Instead of deciding on a class and then figuring out its responsibilities, you are now deciding on a message and figuring out where to send it.

> You don't send messages because you have objects, you have objects because you send messages.

#### 4.3.4. Asking for 'What' Instead of Telling 'How'

A class that is sending a message to another class should not have to worry about the implementation details.
Having a small public interface means that there are few methods for others to depend on.

#### 4.3.5. Seeking Context Independence

A class has a single responsibility but it expects a context.


The context that an object expects has a direct effect on how difficult it is to reuse. An object that could collaborate with others without knowing who they are or what they do could be reused in novel and unanticipated ways.

#### 4.3.6. Trusting Other Objects

> I know what I want, and I trust you to do your part.

This blind trust is a keystone of object-oriented design. It allows objects to col- laborate without binding themselves to context and is necessary in any application that expects to grow and change.

#### 4.3.7. Using Messages to Discover Objects

Sometimes you know the message a class should send (e.g. `suitable_trips` is what the Customer wants). The problem is not with the sender, it is with the receiver. You have not yet identified an object whose responsibility is to implement this method.

#### 4.3.8. Creating a Message-Based Application

Switching your attention from objects to messages allows you to concentrate on designing an application built upon public interfaces.

### 4.4. Writing Code That Puts Its Best (Inter)Face Forward

> It is more important that a well-defined interface exists than that it be perfect.

Think about interfaces. Create them intentionally. It's your interfaces that define your application and determine its future.

#### 4.4.1. Create Explicit Interfaces

Every time you create a class, declare its interfaces. Methods in the public interface should:

* Be explicitly identified as such
* Be more about what than how
* Have names that, insofar as you can anticipate, will not change
* Prefer keyword arguments


- **Private methods**: Least stable kind of methods. Must be called with an implicit receiver.
- **Protected methods**: Unstable methods. Allow explicit receivers as long as the receiver is `self` or an instance of the same class or subclass of `self`.
- **Public methods**: Stable methods. Are visible everywhere.

#### 4.4.2. Honor the Public Interfaces of Others

Do your best to interact with other classes using only their public interfaces.

> If your design forces the use of a private method in another class, first rethink your design.

#### 4.4.3. Exercise Caution When Depending on Private Interfaces

If you cannot avoid using a private method, you can prevent the method from being referenced in many places by isolating the dependency.

#### 4.4.4. Minimize Context

Keep the _what_ vs _how_ discussion in mind; create public methods that allow senders to get what they want without knowing how your class implements its behavior.

### 4.5. The Law of Demeter

#### 4.5.1. Defining Demeter

Demeter restricts the set of objects to which a method may _send_ messages; it prohibits routing a message to a third object via a second object of a different type.

> Only talk to your immediate neighbors

#### 4.5.2. Consequences of Violations

The risk incurred by Demeter violations is low for stable attributes, high for behavior. It could be permitted as long as you're not changing the value of the attribute you retrieve. Certain violations of Demeter reduce your application's flexibility and maintainability, while other make perfect sense.

#### 4.5.3. Avoiding Violations

 You could _delegate_ a message to avoid the dots. However, using delegation to hide tight coupling is not the same as decoupling the code.
 
 #### 4.5.4. Listening to Demeter
 
 Message chains like `customer.bicycle.wheel.rotate` occur when your design thoughts are unduly influenced by objects you already know. The code know not only what it wants but how to navigate through a bunch of intermediate objects to reach the desired behavior.
  
> The train wrecks of Demeter violations are clues that there are objects whose public interfaces are lacking.

### 4.6. Summary

Object-oriented applications are defined by the messages that pass between objects. This message passing takes place along _public_ interfaces.


When messages are trusting and ask for what the sender wants instead of telling the receiver how to behave, objects naturally evolve public interfaces that are flexible and reusable in novel and unexpected ways.

## 5. Reducing Costs with Duck Typing

_Duck typing_: Technique that combines messages + public interfaces.


_Duck types_: Interfaces that are not tied to any specific class.

> If an object quacks like a duck and walks like a duck, then its class is immaterial - it's a duck

### 5.1. Understanding Duck Typing

It is knowledge of the category of the contents of a variable (its _type_) that allows an application to have an expectation about how those contents will behave.

> Users of an object need not, and should not, be concerned about its class. [...] It's not what an object is that matters, it's what it does.

#### 5.1.1. Overlooking the Duck

`Trip`’s prepare method sends message `prepare_bicycles` to the object contained in its `mechanic` parameter.

```ruby
class Trip
  def prepare(mechanic)
    mechanic.prepare_bicycles(bicycles)
  end
end
```

The `Mechanic` class is not referenced. The object `mechanic` could be of any class.

#### 5.1.2. Compounding the Problem

Imagine that requirements change. In addition to mechanic, trip preparation now involves a trip coordinator and a driver.

```ruby
class Trip
  def prepare(preparers)
    preparers.each do |preparer|
      case preparer
      when Mechanic
        preparer.prepare_bicycles(bicycles)
      when TripCoordinator
        preparer.buy_food(customers)
      when Driver
        preparer.gas_up(vehicle)
        preparer.fill_water_tank(vehicle)
      end
    end
  end
end
```

> Code like this gets written when programmers are blinded by existing classes and neglect to notice that they have overlooked important messages; this dependent-laden code is a natural outgrowth of a class-based perspective.

New dependencies on the `prepare` method:

- Relies on specific classes
- Relies on the explicit name of those classes
- Knows the name of the messages that each class understands
- Knows the arguments that those messages require

This style of code propagates itself. When a new trip preparer appears, a programmer will add a new `when` branch to the `case` statement.
The logical endpoint of this programming style is a stiff and inflexible application, where it eventually becomes easier to rewrite everything than to change anything.

> Sequence diagrams should always be simpler than the code they represent; when they're not, something is wrong with the design.

#### 5.1.3. Finding the Duck

The `prepare` method wants to prepare the trip. Its arguments arrive ready to collaborate in trip preparation. 


Remove the expectation about the class of its arguments, and expect each to be a `Preparer`. Ask what message the `prepare` method can send each `Preparer`.


`Trip`'s prepare method now expects its arguments to be `Preparer`s that can respond to `prepare_trip`.

```ruby
class Trip
  def prepare(preparers)
    preparers.each do |preparer|
      preparer.prepare_trip(self)
    end
  end
end
```

#### 5.1.4. Consequences of Duck Typing

Concrete code is easy to understand but costly to extend. Abstract code may initially seem more obscure but, once understood, is far easier to change. 
Use of a duck type makes your code easier to extend but casts a veil over the underlying class of the duck.

> Once you begin to treat your objects as if they are defined by their behavior rather than by their class, you enter into a new realm of expressive flexible design.

**Polymorphism**

The ability of many different objects to respond to the same message. Senders of the message need not care about the class of the receiver; receivers supply their own specific version of the behavior.

### 5.2. Writing Code That Relies on Ducks

It's relatively easy to implement a duck type; your design challenge is to notice that you need on and to abstract its interface.

#### 5.2.1. Recognizing Hidden Ducks

**Case Statements that Switch on Class**

```ruby
class Trip
  def prepare(preparers)
    preparers.each do |preparer|
      case preparer
      when Mechanic
        preparer.prepare_bicycles(bicycles)
      when TripCoordinator
        preparer.buy_food(customers)
      when Driver
        preparer.gas_up(vehicle)
        preparer.fill_water_tank(vehicle)
      end
    end
  end
end
```

When you see this pattern, you know that all of the `preparer`s must share something in common. 
Ask yourself, _'What is it that `prepare` wants from each of its arguments?'_. The answer to that question suggests the message you should send; this message begins to define the underlying duck type.

**`kind_of?` and `is_a?`**

```ruby
class Trip
  def prepare(preparers)
    preparers.each do |preparer|
      if preparer.kind_of?(Mechanic)
        preparer.prepare_bicycles(bicycles)
      elsif preparer.kind_of?(TripCoordinator)
        preparer.buy_food(customers)
      elsif preparer.kind_of?(Driver)
        preparer.gas_up(vehicle)
        preparer.fill_water_tank(vehicle)
      end
    end
  end
end
```

This is the same thing as the previous example and it should be corrected using the same techniques.

**`responds_to?`**

```ruby
class Trip
  def prepare(preparers)
    preparers.each do |preparer|
      if preparer.responds_to?(:prepare_bicycles)
        preparer.prepare_bicycles(bicycles)
      elsif preparer.responds_to?(:buy_food)
        preparer.buy_food(customers)
      elsif preparer.responds_to?(:gas_up)
        preparer.gas_up(vehicle)
        preparer.fill_water_tank(vehicle)
      end
    end
  end
end
```

This code doesn't depend on the class names, but it depends on their behavior.

#### 5.2.2. Placing Trust in your Ducks

Each of the previous examples indicate the presence of an unidentified duck (_I know who you are, and because of that, I know what you do_). This is an indication that you're missing an object, one whose public interface you haven't discovered (doesn't matter if it's a duck type or not). 


When you see these patterns, concentrate on the offending code's expectations and use those expectations to find the duck type.

- Define its interface
- Implement that interface where necessary
- Trust those implementers to behave correctly

#### 5.2.3. Documenting Duck Types

> The simplest kind of duck type is one that exists merely as an agreement about its public interface.

The duck types are abstract; they are strong as a design tool but weak in the code. When you create duck types, you must both document and test their public interfaces.

#### 5.2.4. Sharing Code between Ducks

#### 5.2.5. Choosing your Ducks Wisely

 It is _ok_ to rely on Ruby base classes (`Array`, `String`, `NilClass`). Rails does it, because the chances of those classes changing is way too small. 
  
_Monkey patching_: Making changes to base classes. If you need to monkey patch one of Ruby's base classes, you're probably making the wrong design decision.

### 5.3. Conquering a Fear of Duck Typing

#### 5.3.1. Subverting Duck Types with Static Typing

- Statically typed languages require that you explicitly declare the type of each variable and every method parameter
- Dynamically typed languages allow you to put any value in any variable and pass any argument to any method

Programmers who fear dynamic typing tend to check the classes of their objects ➡ methods fail when new classes appear ➡ programmers think more checking is needed ➡ the code becomes less flexible and more dependent on class.


Duck typing removes the dependencies on class and thus avoid the subsequent type failures.

#### 5.3.2. Static vs Dynamic Typing

**Static Typing**

- The compiler unearths type errors at compile time
- Visible type information serves as documentation
- Complied code is optimized to run quickly

**Dynamic Typing**

- Code is interpreted and can be dynamically loaded; there is no compile/make cycle
- Source code does not include explicit type information
- Metaprogramming is easier 

#### 5.3.3. Embracing Dynamic Typing

For certain applications, well-optimized statically typed code will outperform a dynamically typed implementation.

The value of type declarations as documentation is more subjective: declarations could be distracting for someone that's used to dynamic typing. Once accustomed to it, you'll find this less verbose syntax easy to read, write and understand.

Metaprogramming: Writing code that writes code. Metaprogramming is a scalpel; though dangerous in the wrong hands, it’s a tool no good programmer should willingly be without.

> The fact that some people cannot be trusted with knives does not mean sharp instruments should be taken from the hands of all.

### 5.4. Summary

Duck types detach the public interfaces from specific classes, creating types that are defined by _what they do_ instead of by _who they are_.
Depending on this abstract classes reduces risk and increases flexibility, making your application cheaper to maintain and easier to change.

## 6. Acquiring Behavior through Inheritance

### 6.1. Understanding Classical Inheritance

Inheritance is a mechanism for automatic message delegation. It creates relationships such that, if one object can't respond to a received message, it delegates that message to another.

### 6.2. Recognizing Where to Use Inheritance

#### 6.2.1. Starting with a Concrete Class

This is the `Bicycle` class that represents a road bike.

```ruby
class Bicycle
  attr_reader :size, :tape_color

  def initialize(**opts)
    @size = opts[:size]
    @tape_color = opts[:tape_color]
  end

  # every bike has the same defaults for
  # tire and chain size
  def spares
    {chain: '11-speed',
     tire_size: '23',
     tape_color: tape_color}
  end
  # Many other methods...
end

bike = Bicycle.new(size: 'M',
                   tape_color: 'red')
```

#### 6.2.2. Embedding Multiple Types

What happens when you need the `Bicycle` class to represent mountain bikes as well?

```ruby
class Bicycle
  attr_reader :style, :size, :tape_color, :front_shock, :rear_shock

  def initialize(**opts)
    @style = opts[:style]
    @size = opts[:size]
    @tape_color = opts[:tape_color]
    @front_shock = opts[:front_shock]
    @rear_shock = opts[:rear_shock]
  end

  # checking 'style' starts down a slippery slope
  def spares
    if style == :road
      {chain: '11-speed',
       tire_size: '23', # millimeters
       tape_color: tape_color}
    else
      {chain: '11-speed',
       tire_size: '2.1', # inches
       front_shock: front_shock}
    end
  end
  # ...
end

bike = Bicycle.new(style: :mountain,
                   size: 'S', front_shock: 'Manitou', rear_shock: 'Fox')
puts bike.spares
# => {:chain=>"11-speed", :tire_size=>"2.1", :front_shock=>"Manitou"}

bike = Bicycle.new(style: :road,
                   size: 'M', tape_color: 'red')
puts bike.spares
# => {:chain=>"11-speed", :tire_size=>"23", :tape_color=>"red"}
```

This code contains an `if` statement that checks an attribute that holds the category of self to determine what message to send to self. This is the same pattern as checking for an object's class to know which message to send to it. 

#### 6.2.3. Finding the Embedded Types

Variables named _style_, _type_, _category_ are your cue to notice the underlying pattern.

The `style` variable divides instances of `Bicycle` into two different kinds of things. Some of `Bicycle`'s behavior applies to all bicycle, some only to road bikes and some only to mountain bikes.

> This is the exact problem that inheritance solves: that of highly related types that share common behavior but differ along some dimension

#### 6.2.4. Choosing Inheritance

> Inheritance provides a way to define two objects as having a relationship such that when the first receives a message that it does not understand, it automatically forwards, or delegates, the message to the second.

#### 6.2.5. Drawing Inheritance Relationships

You can use class diagrams to illustrate class relationships. 

- Boxes represent classes
- Lines indicate classes are related
- Hollow triangle means the relationship is inheritance
- The triangle points to the superclass

### 6.3. Misapplying Inheritance

`Bicycle` class is a concrete class that was not written to be subclassed. In order to extract its behavior, we'd need to extract both `MountainBike` and `RoadBike` behavior. If we only extracted `MountainBike`, it would inherit the logic from `Bicycle` that's related to road bikes. 

### 6.4. Finding the Abstraction

Subclasses are specializations of their superclasses.

For inheritance to work:

- The objects that you're modeling  must truly have a generalization-specialization relationship
- You must use the correct coding techniques

#### 6.4.1. Creating an Abstract Superclass

Being `Bicycle` the superclass of `MountainBike` and `RoadBike`, it will contain the common behavior and `MountainBike` and `RoadBike` will add specializations.


`Bicycle` now represents an abstract class, meaning it's disassociated from any specific instance.

> Abstract classes exist to be subclassed. This is their sole purpose. They provide a common repository for behavior that is shared across a set of subclasses—subclasses that in turn supply specializations.

Don't do early abstractions, it's ok for a class to have general and specific behavior in the beginning. 

#### 6.4.2. Promoting Abstract Behavior

We need to make `MountainBike` and `RoadBike` respond to `size`.

```ruby
class Bicycle
  attr_reader :size

  def initialize(**opts)
    @size = opts[:size]
  end
  # ...
end

class RoadBike < Bicycle
  attr_reader :tape_color

  def initialize(**opts)
    @tape_color = opts[:tape_color]
    super
  end
  # ...
end

class MountainBike < Bicycle
  attr_reader :front_shock, :rear_shock

  def initialize(**opts)
    @front_shock = opts[:front_shock]
    @rear_shock = opts[:rear_shock]
    super
  end
  # ...
end

road_bike = RoadBike.new(size: 'M',
                         tape_color: 'red')

mountain_bike = MountainBike.new(size: 'S',
                                 front_shock: 'Manitou',
                                 rear_shock: 'Fox')

puts road_bike.size
# => M

puts mountain_bike.size 
# => S
```

To refactor this code:

- Demote code to one of the subclasses ➡️ copy all the code from `Bicycle` to `RoadBike`
- Start promoting to the super class code that's shared between the subclasses ➡️ start moving the code from `RoadBike` to `Bicycle` to make `MountainBike` respond to shared behavior, like _size_

#### 6.4.3. Separating Abstract from Concrete

`RoadBike` and `MountainBike` both implement a version of `spares`.

Having this requirements:

- Bicycles have a chain and a tire size.
- All bicycles share the same default for chain.
- Subclasses provide their own default for tire size.
- Concrete instances of subclasses are permitted to ignore defaults and supply instance-specific values.

We can extract `chain` and `tire_size` into `Bicycle` ad both types respond to them.

```ruby
class Bicycle
  attr_reader :size, :chain, :tire_size

  def initialize(**opts)
    @size = opts[:size]
    @chain = opts[:chain]
    @tire_size = opts[:tire_size]
  end
  # ...
end
```

#### 6.4.4. Using the Template Method Pattern

This change adds the `default_chain` and `default_tire_size` methods to `Bicycle` for two reasons:

- Wrapping the defaults in methods is a good practice
- To give subclasses the opportunity to contribute specializations by overriding them

> This technique of defining a basic structure in the superclass and sending messages to acquire subclass-specific contributions is known as the _template method_ pattern.

```ruby
class Bicycle
  attr_reader :size, :chain, :tire_size

  def initialize(**opts)
    @size = opts[:size]
    @chain = opts[:chain] || default_chain
    @tire_size = opts[:tire_size] || default_tire_size
  end

  def default_chain # <- common default
  "11-speed"
  end
  # ...
end

class RoadBike < Bicycle
  # ...
  def default_tire_size # <- subclass default
    "23"
  end
end

class MountainBike < Bicycle
  # ...
  def default_tire_size # <- subclass default
    "2.1" 
  end
end

road_bike = RoadBike.new(
  size: 'M',
  tape_color: 'red')

puts road_bike.tire_size # => 23
puts road_bike.chain # => 11-speed

mountain_bike = MountainBike.new(
  size: 'S',
  front_shock: 'Manitou',
  rear_shock: 'Fox')

puts mountain_bike.tire_size # => 2.1
puts mountain_bike.chain # => 11-speed
```

#### 6.4.5. Implementing Every Template Method

`Bicycle`'s `initialize` method sends `default_tire_size`, but `Bicycle` itself doesn't implement it. As `Bicycle` is written, subclasses must implement `default_tire_size`. It's imposing a requirement upon its subclasses that is not obvious from a glance at the code.


Any class that uses the template method pattern must supply an implementation for every message it sends, even if the only reasonable implementation in the sending class is raising an error.

```ruby
class Bicycle
  # ...
  def default_tire_size
    raise NotImplementedError, "#{self.class} should have implemented..."
  end
end

bent = RecumbentBike.new(size: "L")
# => RecumbentBike should have implemented...
# => .../some_file.rb:15:in `default_tire_size'
```

> Creating code that fails with reasonable error messages takes minor effort in the present but provides value forever.

### 6.5. Managing Coupling between Superclasses and Subclasses

#### 6.5.1. Understanding Coupling

We've now extracted the common `spares` into `Bicycle` and each of the subclasses implement their specific `spares`.

```ruby
class Bicycle
  attr_reader :size, :chain, :tire_size

  def initialize(**opts)
    @size = opts[:size]
    @chain = opts[:chain] || default_chain
    @tire_size = opts[:tire_size] || default_tire_size
  end

  def spares
    {tire_size: tire_size,
     chain: chain}
  end

  def default_chain
    "11-speed"
  end

  def default_tire_size
    raise NotImplementedError, "#{self.class} should have implemented..."
  end
end

class RoadBike < Bicycle
  attr_reader :tape_color

  def initialize(**opts)
    @tape_color = opts[:tape_color]
    super
  end

  def spares
    super.merge(tape_color: tape_color)
  end

  def default_tire_size
    "23"
  end
end

class MountainBike < Bicycle
  attr_reader :front_shock, :rear_shock

  def initialize(**opts)
    @front_shock = opts[:front_shock]
    @rear_shock = opts[:rear_shock]
    super
  end

  def spares
    super.merge(front_shock: front_shock)
  end

  def default_tire_size
    "2.1"
  end
end
```

Now both `MountainBike` and `RoadBike` know things about themselves (their spare parts specializations) and things about their superclass (that it implements `spares` to return a hash and that it responds to `initialize`).

> Knowing things about other classes creates dependencies, and dependencies couple objects together.

What happens if you create a new class and forget to call `super` in the `initialize` or `spares` methods?

Subclasses now know how they are supposed to interact with their superclass. They are forced to send `super`, and all the superclasses send `super` in the exact same places.

#### 6.5.2. Decoupling Subclasses Using Hook Messages

Instead of allowing subclasses to know the algorithm and requiring that they send `super`, subclasses can instead send _hook_ messages, ones that exist solely to provide subclasses a place to contribute information by implementing matching methods. This strategy removes knowledge of the algorithm from the subclass and returns control to the superclass.
 
```ruby
class Bicycle
  attr_reader :size, :chain, :tire_size

  def initialize(**opts)
    @size = opts[:size]
    @chain = opts[:chain] || default_chain
    @tire_size = opts[:tire_size] || default_tire_size

    post_initialize(opts) # Bicycle both sends
  end

  def post_initialize(opts)  # and implements this
  end
  # ...
end

class RoadBike < Bicycle
  attr_reader :tape_color

  def post_initialize(opts)
    @tape_color = opts[:tape_color]
  end
end
``` 

This change removes the `initialize` method from the subclasses. They no longer control initialization, they contribute specializations to a larger, abstract algorithm. That algorithm is defined in the abstract superclass `Bicycle`, which in turn is responsible for sending `post_initialize`.


Subclasses are responsible for what initialization they need but they're no longer responsible for when their initialization occurs. Putting control of the timing in the superclass means the algorithm can change without forcing changes upon the subclasses.

We can do the same for the `spares` method:

```ruby
class Bicycle
  # ...
  def spares
    {
      tire_size: tire_size,
      chain: chain
    }.merge(local_spares)
  end
  
  # hook for subclasses to override
  def local_spares
    {}
  end
end

class RoadBike < Bicycle
  # ...
  def local_spares
    { tape_color: tape_color }
  end
end
```

Now, it's simple to create a new subclass as it only needs to implement the template methods.

### 6.6. Summary

Inheritance solves the problem of related types that share a great deal of common behavior but differ across some dimension. It allows you to isolate shared code and implement common algorithms in an abstract classe, while also providing a structure that permits subclasses to contribute specializations.


The best way to create an abstract superclass is by pushing code up from concrete subclasses.


Identifying the correct abstraction is easiest if you have access to at least three existing concrete classes.


Abstract superclasses use the template method pattern to invite inheritors to supply specializations. Hook methods allow subclasses to contribute specializations without knowing the abstract algorithm and without needing to send `super`.

> Well-designed inheritance hierarchies are easy to extend with new subclasses, even for programmers who know very little about the application. This ease of extension is inheritance’s greatest strength.
