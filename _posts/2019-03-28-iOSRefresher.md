---
layout: post
title: iOS and Swift Refresher!
subtitle: Basics
image: /img/hello_world.jpeg
---

***Must Refer***

> [swift apple
> documentation](https://developer.apple.com/documentation/swift)
> 
> [swift lang
> documentation](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
> 
> [swift tutorials
> point](https://www.tutorialspoint.com/swift/index.htm)



### iOS Basic Info
 - iPhone OS(first name)
 - Unix based
 - first os with muti touch GUI,in their words a phone that runs macOS
 - Latest Version - 12.2
 - Privacy oriented

### Development Languages
 - **swift**
    Curent version: swift 5.0
    open source
    modern and better performance than objective c
  - **objective** c    (header(.h) and implementation (.m) files ) 
    Programming language for NeXTSTEP OS
 - **c and c++** (limited)




 



#  Swift Language
Swift includes modern features like type inference, optionals, and closures, which make the syntax concise yet expressive. Swift ensures your code is fast and efficient, while its memory safety and native error handling make the language safe by design. Writing Swift code is interactive and fun in Swift Playgrounds, playgrounds in Xcode, and REPL.

## Constants and Variables

Variables are nothing but *reserved memory locations to store values*. This means that when you create a variable, you reserve some space in memory
 

   > **let** : constant   
   >  **var**: variable

 -    **Type Annotations**
Telling the type of a variable or constant
 

>     var name: String

 - **Type Inference**
 The ability of Swift's compiler to figure out what kind of data type should be assigned to each of your variables and constants, so you don't have to explicitly state it.
 

>     var name = "Swift"

 - **Type Aliases**

	_Type aliases_  define an alternative name for an existing type. You define type aliases with the  `typealias`  keyword.
- **Type Coversion**

	`SomeType(ofInitialValue)` is the default way to call the initializer of a Swift type and pass in an initial value.
	
-	**[Typecasting](https://medium.com/@abhimuralidharan/typecastinginswift-1bafacd39c99)**

	 _Type casting_  is a way to check the type of an instance, or to treat that instance as a different superclass or subclass from somewhere else in its own class hierarchy.

	Type casting in Swift is implemented with the  **`is`  and  `as`**  operators. These two operators provide a simple and expressive way to check the type of a value or cast a value to a different type.
 - **Naming**
 Constant and variable names can’t contain whitespace characters, mathematical symbols, arrows, private-use Unicode scalar values, or line- and box-drawing characters. 

	 Nor can they begin with a number, although numbers may be included elsewhere within the name
	

## Data Types


Based on the data type of a variable, the operating system allocates memory and decides what can be stored in the reserved memory.

### Built-in Data Types
	
In Swift Data types are ***internally implemented as structs***.

The swift standard library contains **Int,Double,String,Array,Dictionary** as structs,

Swift  offers the programmer a rich assortment of built-in as well as user-defined data types. The following types of basic data types are most frequently when declaring variables −

-   **Int or UInt**  − This is used for whole numbers. More specifically, you can use Int32, Int64 to define 32 or 64 bit signed integer, whereas UInt32 or UInt64 to define 32 or 64 bit unsigned integer variables. For example, 42 and -23.
	    
-   **Float**  − This is used to represent a 32-bit floating-point number and numbers with smaller decimal points. For example, 3.14159, 0.1, and -273.158.
	    
-   **Double**  − This is used to represent a 64-bit floating-point number and used when floating-point values must be very large. For example, 3.14159, 0.1, and -273.158.
	    
-   **Bool**  − This represents a Boolean value which is either true or false.
	    
-   **String**  − This is an ordered collection of characters. For example, "Hello, World!"
	    
-   **Character**  − This is a single-character string literal. For example, "C"
	    
-   **Optional**  − This represents a variable that can hold either a value or no value.
	    
-   **Tuples**  − This is used to group multiple values in single Compound Value.
	    

	 Few important points related to Integer types −

	-   On a 32-bit platform, Int is the same size as Int32.
	    
	-   On a 64-bit platform, Int is the same size as Int64.
	    
	-   On a 32-bit platform, UInt is the same size as UInt32.
	    
	-   On a 64-bit platform, UInt is the same size as UInt64.
	    
	-   Int8, Int16, Int32, Int64 can be used to represent 8 Bit, 16 Bit, 32 Bit, and 64 Bit forms of signed integer.
	    
	-   UInt8, UInt16, UInt32, and UInt64 can be used to represent 8 Bit, 16 Bit, 32 Bit and 64 Bit forms of unsigned integer.

## Tuples

_Tuples_  group multiple values into a single compound value. The values within a tuple can be of any type and don’t have to be of the same type as each other.

    1.  let http404Error = (404, "Not Found")
    2.  // http404Error is of type (Int, String), and equals (404, "Not Found")

Tuples are useful for temporary groups of related values. They’re not suited to the creation of complex data structures.

## Optionals

You use  _optionals_  in situations where a value may be absent. An optional represents two possibilities: Either there  _is_  a value, and you can unwrap the optional to access that value, or there  _isn’t_  a value at all.

### Optional Binding

You use  _optional binding_  to find out whether an optional contains a value, and if so, to make that value available as a temporary constant or variable. Optional binding can be used with  `if`  and  `while`  statements to check for a value inside an optional, and to extract that value into a constant or variable, as part of a single action

  

    if let constantName = someOptional {
      statements
      }
### Implicitly Unwrapped Optionals

You write an implicitly unwrapped optional by placing an exclamation mark (`String!`) rather than a question mark (`String?`) after the type that you want to make optional.

Implicitly unwrapped optionals are useful when an optional’s value is confirmed to exist immediately after the optional is first defined and can definitely be assumed to exist at every point thereafter. The primary use of implicitly unwrapped optionals in Swift is during class initialization.

###  Optional Chaining


The process of querying, calling properties, subscripts and methods on an optional that may be 'nil' is defined as optional chaining. Optional chaining return two values −

>  Optional Chaining is used as an alternative to Forced Unwrapping

-   if the optional contains a 'value' then calling its related property, methods and subscripts returns values
    
-   if the optional contains a 'nil' value all its its related property, methods and subscripts returns nil

Optional chaining  fails gracefully when the optional is 'nil'.
    

## Error Handling

You use  _error handling_  to respond to error conditions your program may encounter during execution.

In contrast to optionals, which can use the presence or absence of a value to communicate success or failure of a function, error handling allows you to determine the underlying cause of failure, and, if necessary, propagate the error to another part of your program.

When a function encounters an error condition, it  _throws_  an error. That function’s caller can then  _catch_  the error and respond appropriately.

      func canThrowAnError() throws {
      // this function may or may not throw an error
      }

Swift automatically propagates errors out of their current scope until they’re handled by a  `catch`  clause.

      do {
      try canThrowAnError()
      // no error was thrown
     } catch {
      // an error was thrown
      }

A  `do`  statement creates a new containing scope, which allows errors to be propagated to one or more  `catch`  clauses.

## Assertions and Preconditions

_Assertions_  and  _preconditions_  are checks that happen at runtime. You use them to make sure an essential condition is satisfied before executing any further code. If the Boolean condition in the assertion or precondition evaluates to  `true`, code execution continues as usual. If the condition evaluates to  `false`, the current state of the program is invalid; code execution ends, and your app is terminated.

The difference between assertions and preconditions is in when they’re checked: Assertions are checked only in debug builds, but preconditions are checked in both debug and production builds.

	    







<!--stackedit_data:
eyJoaXN0b3J5IjpbNzE4NjUyNjcyLDY2NzQ5MDkwMSw1MzUxND
g0NTUsLTE4MzkzODM0MzUsLTcyNzE2Mzc0MSwxMjMyNzkwMzk3
LDEzNjg1MTEyOSwyNTIzMDM3MzIsLTQxODUyODUzMyw1NzA2OD
YwMDcsLTE2NjU3MDMxNyw4MjY2MjMwNjksNTA5NDQyMTY1LDIw
NzY5NjI3MzVdfQ==
-->