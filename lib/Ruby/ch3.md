# 3) Organizing objects with classes

Defining a class lets you group behaviours (methods) into convenient bundles, so that you can quickly create many objects that behave essentially the same way. 
 
Everything you handle in Ruby is either an object or a construct that evaluates to an object, and every object is an instance of some class. This fact hold true even where it might first seem a little old. Integres are instances of class, and the classes themselves are objects.

### 3.1) Classes and instances

Classes usually exist for the purpose of being *instantiated* -that is, of having objects created that are instances of the class.

You have seen instantiation in cation before: `obj = Object.new`

The *new* method is a *constructor*: a method whose purpose it to manufature and return to you a new instance of the class, a newly mindted object.

You define a class with the `class` keyword. Classes are named with *constants*, a special type of identifier recognizable by the fact that it begins with a capital letter. Constants are used to store information and values that don't change over the course of a program run.

