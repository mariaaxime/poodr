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

**S**ingle Responsibility
**O**pen-Closed
**L**iskov Substitution
**I**nterface Segregation
**D**ependency Inversion

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

```
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
```
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

```
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
```
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

```
def diameters
  wheels.collect{|wheel| wheel.rim + (wheel.tire * 2)}
end
```

_Do_

```
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
