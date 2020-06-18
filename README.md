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

There are numerous Ruby gems that asses how well your code follows OOD principles. Metrics software works by scanning source code and counting things that predict quality. Running a metrics suite against your own code can be illuminating, humbling, and sometimes alarming. Seemingly well-designed applications can rack up impres-
sive numbers of OOD violations.

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

#### 2.2.1. An Example Application: Bycicles and Gears

A class consists of eveything it directly implements plus everything it inherits.

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

You can use a `Struct` to separate structure from meaning.

This style of code allows you to protect against changes in externally owned data structures and to make your code more readable and intention revealing.

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
