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

