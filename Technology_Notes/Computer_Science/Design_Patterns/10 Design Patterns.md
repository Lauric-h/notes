#designpatterns, #learnings, #computerscience

From [this video](https://www.youtube.com/watch?v=tv-_1er1mWI)

# 10 Design Patterns
Design patterns are divided into 3 types:
- Creational => how objects are created
- Structural => how objects relate to each other
- Behavioral => how objects communicate

## Creational
**Singleton**  
Type of object taht can only be instantiated once.  

**Prototype**  
= Clone. Alternative way to implement inheritance. Inherite from an already created object.  

**Builder**  
Create an object step by step using methods instead of constructor. Each method return `this` so we can chain them.  

**Factory**  
Instead of using the `new` keyword, we use a method or function to build object.

## Structural
**Facade**  
Simplified API to hide low level details in codebase.  

**Proxy**  
A substitute. Replace a target object with a proxy (an other object).  

## Behavioral
**Iterator** 
Allows to traverse a collection of object.  

**Observer**  
Allows many objects to subscribe to events that are broadcasted by an other object (1 to many relationship).  

**Mediator**  
Middleman/middleware. Object that sits between 2 objects.  

**State**  
Make an object predictable based on its underlying class => we set the state as a property and use diferrent class for each state., if the state changes, the behavior changes too. Prevents using long switch statements.
