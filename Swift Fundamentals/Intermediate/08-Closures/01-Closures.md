# Closures

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand what closures are and how they differ from functions
- Write basic closure expressions with parameters and return values
- Use closures as function parameters
- Apply trailing closure syntax to make your code more readable.

---

## What are Closures?

Closures are self-contained blocks of functionality that can be passed around and used in your code. Think of them as functions without names that you can create on the spot and pass to other functions or store in variables.

Closures are similar to blocks in C and Objective-C and to lambdas in other programming languages. They're incredibly useful for functional programming patterns and are used extensively throughout Swift and SwiftUI.

### Basic Closure Syntax

The simplest closure looks like this:

```swift
let greet = {
    print("Hello, World!")
}
// Call the closure
greet()
// Prints "Hello, World!"
```

This closure doesn't take any parameters and doesn't return a value. Notice that closures are not declared using the func keyword, and they don't have names in their signatures.

## Closures with Parameters and Return Values

Closures can accept parameters and return values, just like functions. The syntax puts everything inside the curly braces:

```swift
let addNumbers = { (a: Int, b: Int) -> Int in
    return a + b
}

let result = addNumbers(5, 3)
print(result) // Prints 8
```

The structure is:
- `{ (parameters) -> ReturnType in` - defines the closure signature
- `return value` - the closure body
- `}` - closes the closure

### Implicit Returns

Single-expression closures can implicitly return their result without the return keyword:

```swift
let multiply = { (a: Int, b: Int) -> Int in
    a * b  // No return keyword needed
}

let product = multiply(4, 5)
print(product) // Prints 20
```

## Using Closures with Functions

One of the most powerful features of closures is passing them as parameters to functions. Here's a common example using the `sorted(by:)` method:

```swift
let names = ["Chris", "Alex", "Ewa", "Barry", "Daniella"]

// Using a closure to sort alphabetically
let sortedNames = names.sorted(by: { (s1: String, s2: String) -> Bool in
    return s1 < s2
})
print(sortedNames)
// Prints ["Alex", "Barry", "Chris", "Daniella", "Ewa"]
```

### Type Inference

Swift can often infer the parameter types and return type from context, making closures more concise:

```swift
// Swift infers the types
let sortedNames = names.sorted(by: { s1, s2 in
    return s1 < s2
})
```

### Shorthand Argument Names

Swift provides shorthand argument names ($0, $1, $2, etc.) that refer to the closure's arguments:

```swift
// Using shorthand argument names
let sortedNames = names.sorted(by: { $0 < $1 })
```

Here, `$0` refers to the first parameter and `$1` refers to the second parameter.

## Trailing Closures

When a closure is the last parameter of a function, you can write it as a trailing closure outside the parentheses:

```swift
// Standard syntax
let sortedNames = names.sorted(by: { $0 < $1 })

// Trailing closure syntax
let sortedNames = names.sorted { $0 < $1 }
```

If the function only takes a closure as its parameter, you can omit the parentheses entirely.

### Real-World Example

Here's how trailing closures are commonly used with array methods:

```swift
let numbers = [1, 2, 3, 4, 5]

// Using map to transform each element
let doubled = numbers.map { $0 * 2 }
print(doubled) // Prints [2, 4, 6, 8, 10]

// Using filter to select elements
let evenNumbers = numbers.filter { $0 % 2 == 0 }
print(evenNumbers) // Prints [2, 4]
```

## Creating Functions that Accept Closures

You can create your own functions that accept closures as parameters:

```swift
func performOperation(on numbers: [Int], operation: (Int) -> Int) -> [Int] {
    var result: [Int] = []
    for number in numbers {
        result.append(operation(number))
    }
    return result
}

// Usage
let numbers = [1, 2, 3, 4, 5]
let squared = performOperation(on: numbers) { $0 * $0 }
print(squared) // Prints [1, 4, 9, 16, 25]
```

## Practical Example: Button Actions

In iOS development, closures are commonly used for button actions:

```swift
// SwiftUI Button example
Button("Tap Me") {
    print("Button was tapped!")
}

// This is equivalent to:
Button(
    action: {
        print("Button was tapped!")
    },
    label: {
        Text("Tap Me")
    }
)
```

--- 

## 🛫 Next Steps

#### What You've Learned
- ✅ Understanding closures as unnamed blocks of functionality
- ✅ Writing closures with parameters and return values
- ✅ Using the `in` keyword to separate parameters from the closure body
- ✅ Leveraging type inference to write concise closures
- ✅ Using shorthand argument names ($0, $1) for cleaner syntax
- ✅ Applying trailing closure syntax for better readability
- ✅ Creating functions that accept closures as parameters
- ✅ Recognizing common closure patterns in iOS development

#### Where to Go Next
**Continue to** [Control Flow - Loops](/Swift%20Fundamentals/02-control-flow/02-loops.md)

---

## 📚 Resources 
- [Swift Programming Language - Closures](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/closures/)
- [Hacking with Swift - Closures](https://www.hackingwithswift.com/quick-start/beginners/how-to-create-and-use-closures)
- [Ray Wenderlich - Swift Closures Tutorial](https://www.raywenderlich.com/543-swift-functional-programming-tutorial)
- [Apple Developer Documentation - Closures](https://developer.apple.com/documentation/swift/closures)