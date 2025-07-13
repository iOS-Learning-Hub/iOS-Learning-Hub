# Variables and Constants

### 🎯 Learning Objectives

By the end of this lesson you will:

- Understand the difference between variables and constants
- Know when to use `var` vs `let`
- Understant type annotations
- Master Swift naming conventions
- Understand type inference and explicit typing
- Understand more about Comments and Semicolons in Swift

---

### 📝 What are Variables and Constants?
In Swift, we store data in two types of containers:
- **Variables (`var`):** Values that can change
- **Constants (`let`):** Values that cannot change once set

Think of them like containers:
- **Variable** = A box you can open and change contents
- **Constant** = A sealed box that cannot be reopened

---

### 🔧 Creating Variables

```
swift

// Creating a variable

var playerScore = 0
var playerName = "Alex"
var isGameOver = false

// You can change variables later
playerScore = 100
playerName = "Sarah"
isGameOver = true

```

#### **Key Points:**
- Use `var` keyword
- Can be changed after creation

--- 

### 🔒 Creating Constants

```
swift

// Creating constants
let maxScore = 100
let gameName = "Super Quiz"
let pi = 3.14159

// ❌ This would cause an error:
// maxScore = 1500 // Cannot assign to value: 'maxScore' is a 'let' constant
```

#### **Key Points:**
- Use `let` keyword
- Cannot be changed after creation
- More memory efficient
- Prevents accidental changes

---

### 🎯 When to Use Each

**Use `let`(Constants) When:**
- Values won't change
- Configuration values
- **Default choice** - always prefer `let` unless you need to change the value

**Use `var`(Variables) When:**
- Values will change during execution
- User input, scores, counters
- Temporary calculations

```
swift

// Good examples

let appName = "My iOS App"      // Never changes
let maxUsers = 1000             // Fixed limit
var currentUsers = 0            // Changes as users join/leave
var userScore = 0               // Changes during gameplay

```

---
### ⚠️ Type Annotations
In Swift, you can provide a *type annotation* when you declare a constant or variable, to be clear about the kind of values the constant or variable can store.

`var welcomeMessage: String`

> **Note:** 
> It's rare that you need to write type annotations in practice. If you provide an initial value for a constant or variable at the point that it's defined, Swift can almost always infer the type to be used for that constant or variable. See more in [Type Safety and Type Inference](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics/#Type-Safety-and-Type-Inference)

---

### 🏷️ Naming Conventions

Constant and variable names can contain almost any character, including Unicode characters:

```
let π = 3.14159
let 你好 = "你好世界"
let 🐶🐮 = "dogcow"
```

**Rules:**
- Can't contain whitespace characters, mathematical symbols, arrows, private-use Unicode scalar values, or line- and box-drawing characters.
- They can't begin with a number, although numbers may be included elsewhere within the name

Swift follows **camelCase** naming:

```
swift

// ✅ Good naming
let userName = "john_doe"
var highestScore = 2500
let isUserLoggedIn = true
var numberOfAttempts = 3

// ❌ Bad naming
let user_name = "john_doe"      // Don't use underscores
var HighestScore = 2500         // Don't start with uppercase
let isuserloggedin = true       // Hard to read
var x = 3                       // Not descriptive

```

**Best practices:**
  1. **Start with lowercase letter**
  2. **Use camelCase** for multple words
  3. **Be descriptive** - code should read like English
  4. **Use meaningful names** that explain the purpose

--- 

### 🎨 Type Inference vs Type Annotation

Swift can almost always figure out types (type inference) 

```
swift
// Type inference (Swift figures it out)
let age = 25                    // Swift knows this is Int
let name = "Emma"               // Swift knows this is String
let height = 5.8                // Swift knows this is Double
let isActive = true             // Swift knows this is Bool

// Type Annotation
let age: Int = 25
let name: String = "Emma"
let height: Double = 5.8
let isActive: Bool = true
```

**When to use Type Annotation:**
- When the type isn't obvious
- When you want a specific type
- For clarity in complex code

```
swift

// Sometimes you need to be explicit
let score: Double = 0   // Without this, it would be Int
let userID: String = "12345"    // This looks like a number but should be String

```

---

### ✍️ Comments

Use comments to include nonexecutable text in your code, as a note or reminder to yourself. Comments are ignored by the Swift compiler when your code is compiled

**Single-line comments** begin with two forward-slashes (//)

**Multiline comments** start with a forward-slash followed by an asterisk ( /* ) and end with an asterisk followed by a forward-slash (*/)

```

// This is a comment


/* This is also a comment
but is written over multiple lines. */

/* This is the start of the first multiline comment.
    /* This is the second, nested multiline comment. */
This is the end of the first multiline comment. */

```

--- 

### ; Semicolons
Unlike many other languages, Swift doesn't require you to write a semicolon (;) after each statement in your code, although you can do so if you wish. However, semicolons *are* required if you want to write multiple separate statements on a single line:

```
let cat = "🐱"; print(cat)
// Prints "🐱"
```