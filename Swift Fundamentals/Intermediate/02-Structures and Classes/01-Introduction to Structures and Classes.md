# Structures and Classes in Swift

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand the fundamental differences between structures and classes
- Know when to use structs vs classes in your Swift code
- Grasp the concept of value types vs reference types
- Create basic structures and classes with properties and methods

---

## What Are Structures and Classes?

Both **structures** (structs) and **classes** are fundamental building blocks in Swift that allow you to create custom data types. They help you organize and model data in your applications.

### Common Features

Both structs and classes can:
- Define properties to store values
- Define methods to provide functionality
- Define initializers to set up their initial state
- Be extended to expand their functionality
- Conform to protocols

```swift
// A basic struct example
struct Person {
    var name: String
    var age: Int
    
    func introduce() {
        print("Hi, I'm \(name) and I'm \(age) years old")
    }
}

// A basic class example
class Vehicle {
    var brand: String
    var model: String
    
    init(brand: String, model: String) {
        self.brand = brand
        self.model = model
    }
    
    func start() {
        print("\(brand) \(model) is starting...")
    }
}
```

## Key Differences

### 1. Value Types vs Reference Types

**Structures are value types** - they are copied when assigned or passed around
**Classes are reference types** - they are passed by reference, sharing the same instance

```swift
// Struct example (Value Type)
struct Point {
    var x: Int
    var y: Int
}

var pointA = Point(x: 5, y: 10)
var pointB = pointA  // Creates a copy
pointB.x = 20

print(pointA.x)  // Output: 5 (unchanged)
print(pointB.x)  // Output: 20

// Class example (Reference Type)
class Rectangle {
    var width: Int
    var height: Int
    
    init(width: Int, height: Int) {
        self.width = width
        self.height = height
    }
}

let rectA = Rectangle(width: 10, height: 20)
let rectB = rectA  // Shares the same reference
rectB.width = 30

print(rectA.width)  // Output: 30 (changed!)
print(rectB.width)  // Output: 30
```

### 2. Initialization

```swift
// Structs get automatic memberwise initializers
struct Book {
    var title: String
    var author: String
    var pages: Int
}

let book = Book(title: "Swift Guide", author: "Apple", pages: 500)

// Classes require explicit initializers
class Car {
    var make: String
    var model: String
    
    init(make: String, model: String) {
        self.make = make
        self.model = model
    }
}

let car = Car(make: "Toyota", model: "Camry")
```

### 3. Inheritance

Classes support inheritance, while structs do not

```swift
// Classes can inherit from other classes
class Animal {
    var name: String
    
    init(name: String) {
        self.name = name
    }
    
    func makeSound() {
        print("Some generic animal sound")
    }
}

class Dog: Animal {
    override func makeSound() {
        print("\(name) says Woof!")
    }
}

// Structs cannot inherit from other structs
// But they can conform to protocols for shared behavior
```

### 4. Mutability

```swift
// Struct instances must be var to modify properties
let constantStruct = Point(x: 5, y: 10)
// constantStruct.x = 20  // Error! Cannot modify

var mutableStruct = Point(x: 5, y: 10)
mutableStruct.x = 20  // Works!

// Class instances can modify properties even when declared as let
let constantClass = Rectangle(width: 10, height: 20)
constantClass.width = 30  // Works! (modifying the object, not the reference)
```

## When to Use Structs vs Classes

### Use Structs When:
- You want value semantics (copying behavior)
- Modeling simple data that doesn't require inheritance
- You prefer immutability and thread safety
- Working with small, lightweight data structures
- Representing mathematical values, colors, geometric shapes

### Use Classes When:
- You need reference semantics (shared instances)
- You require inheritance to share behavior
- Working with complex objects that have identity
- Need deinitialization (cleanup when object is destroyed)
- Interfacing with Objective-C APIs

## Apple's Recommendation

Apple recommends using structures by default because they're easier to reason about, and only use classes when they're appropriate or necessary.

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Fundamental differences between structs and classes
- ✅ Value types vs reference types concept
- ✅ Basic syntax for creating structs and classes
- ✅ When to choose structs vs classes

#### Where to Go Next
**Continue to:**
- [Deep Dive to Structures](/Swift%20Fundamentals/Intermediate/02-Structures%20and%20Classes/02-Deep%20Dive%20to%20Structures.md)

- [Memory Management and ARC](/Swift%20Fundamentals/03-structures-classes/04-memory-management.md)

---

## 📚 Resources 
- [Choosing Between Structures and Classes - Apple Developer](https://developer.apple.com/documentation/swift/choosing-between-structures-and-classes)
- [The Swift Programming Language - Structures and Classes](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures)