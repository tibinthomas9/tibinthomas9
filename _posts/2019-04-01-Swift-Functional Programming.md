---
layout: post
title: Swift-Functional Programming
subtitle: Concepts
show-avatar: false
---

# Functional Programming in Swift

>   A programming paradigm that treats  computations  as the evaluation of mathematical functions and  avoids changing-state and mutable data. It is  declarative programming paradigm, which means  programming is done with  expressions.​
    
In terms of Swift, functional programming means **using lets instead of vars when dealing with data**. This has its benefits, mainly that functional code is less prone to bugs and easier to understand  than imperative code. Imperative programming is the opposite of functional programming — it’s a paradigm that uses statements that change a program’s state.

In **procedural/imperative program** we say **how to do** whereas in **functional/declarative programming** we say **what to do**.

## Programming Paradigms



-   **Object-oriented programming (OOP**) is a programming paradigm based on the concept of “objects”, which may contain data, in the form of fields, often known as attributes; and code, in the form of procedures, often known as methods​
    
    
-   **Procedural programming** is a programming paradigm, derived from structured programming, based upon the concept of the procedure call. Procedures, also known as routines, subroutines, or functions (not to be confused with mathematical functions, but similar to those used in functional programming), simply contain a series of computational steps to be carried out.”​
    

    
-   **Functional programming (FP)** is a programming paradigm — a style of building the structure and elements of computer programs — that treats computation as the evaluation of mathematical functions and avoids changing-state and mutable data​

Functional programming tends to reuse a common set of functional utilities to process data. Object oriented programming tends to colocate methods and data in objects. Those colocated methods can only operate on the type of data they were designed to operate on, and often only the data contained in that specific object instance.

## How to do it?
  A key practice in functional programming is breaking code down into smaller, pure functions, which can be used several times throughout the project. Pure functions are functions that have no side effects on the program as a whole, meaning they exist solely to help other functions which do participate in the program.​
    
  
   Without providing a concrete definition, here are what I see as the 3 main goals of functional programming:​
    
-   use pure functions where possible​
    
-   avoid mutability where possible​
    
-   use functions as the basic building blocks

## Functional Programming Principles
1. Functions are first-class data types. That means they can be created, copied, and passed around like integers and strings.​



2. Because functions are first-class data types, they can be used as parameters to other functions. Functions that accepts another function as a parameter are referred to as higher-order functions. ​

    

3. In order to allow our functions to be re-used in various ways, they should always return the same output when given specific input, and not cause any side effects. Pure functions are essentially ones that give consistent results for a given input and cause no side effects. ​
4. Because functions always return the same output for some given input, we should prefer to use immutable data types rather than using functions to change mutable variables. ​


5. Because our functions don't cause side effects and variables are all immutable, we can reduce how much state we track in our program – and often eliminate it altogether​ .

## Aspects of functional programming



###  **Immutable Data(Values)​**

A **mutable** object can be changed after it's created, and an **immutable** object can't.


Immutable datastructures are an important technique for reducing software bugs, and they do this by simply being very limited about what you can do with them. There is one and only one thing that can be done with an immutable datastructure: data can be read from it.

###   **Side Effects**
A side effect is any application state change that is observable outside the called function other than its return value. Side effects include:

  Modifying any external variable or object property (e.g., a global variable, or a variable in the parent function scope chain)
	-   Logging to the console
	-   Writing to the screen
	-   Writing to a file
	-  Writing to the network
	-   Triggering any external process
	-   Calling any other functions with side-effects

Side effects are mostly avoided in functional programming, which makes the effects of a program much easier to understand, and much easier to test.
    

    
###     **Pure functions​**
-   Same input always results in same  output (Referential  Transparency)​
	
-  Evaluation of result does not cause any side  effect​  ​
      eg. No change in database or to I/O  devices​
 
-   Result value need not depend on all arguments but it must depend on nothing other than the arguments​
    
    
###     **Higher Order  Functions​**

In FP languages, **functions are  _first-class_  citizens**. You treat functions like other objects that you can assign to variables.

Because of this, functions can also accept other functions as parameters or return other functions. Functions that accept or return other functions are called **higher-order functions.**
    

    
###     ​**Partial Functions / Currying**
		
Partial functions allow you to encapsulate one function within another.
		
Currying allows you to turn a single function with multiple arguments into a series of functions – each with one argument. This allows you to store variables in functions and also create functions that return functions.
		
In short they are **functions that return functions**.
		
It  helps to reduce function arguments, and store some of the arguments within the function itself.It is also used to allow the chaining of operations on a particular dataset.
		
In Swift instance methods are implemented as Curried”Functions /An instance method in Swift is just a type method that takes the instance as an argument and returns a function which will then be applied to the instance.
## Functional Programming in Swift - Key Functions

-   **map()** Takes a value out of a container, applies a function to it, then puts the result of that function back into a new container that gets returned to you.​
      ​
    
-   **flatMap()** The flatMap() function is effectively the combination of using map() and flatten() in a single call, in that order; useful in handling optionals. ​
 
    
-   **filter()** The filter() method loops over every item in a collection, and passes it into a function that you write. If your function returns true for that item it will be included in a new array, which is the return value for filter(). ​


-   **reduce()** The reduce() function condenses an array into a single value by applying a function to every item. Each time the function is called, you get passed the previous value from your function as well as the next item in your array. ​
 
 
-   **sort()** Can do basic sorts on arrays without even passing arguments to it, but can also pass in blocks that handle more complex sorting.​

## Advantages

- Maintainable  code.​   
- Easier and complete  testing.​  
- Easier parallel and concurrent  programming.​
- Preserves State
- Avoid Deadlocks
- Cleaner and Readable Code
- Modularity










 



 














