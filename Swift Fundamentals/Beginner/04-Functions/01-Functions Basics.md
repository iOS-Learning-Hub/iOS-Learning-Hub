# Functions - Basics

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand what functions are and why they're essential in programming
- Know how to define and call functions using the `func` keyword
- Be able to create functions with and without parameters
- Master the syntax for function declaration and function calls
- Understand the difference between parameters and arguments
- Know how to write functions that perform specific tasks

---

## What Are Functions?

Functions are reusable blocks of code that perform specific tasks. Think of them as mini-programs within your program that you can call whenever you need to accomplish a particular job. Instead of writing the same code multiple times, you write it once in a function and call it whenever needed.

**Why use functions?**
- **Reusability**: Write once, use many times
- **Organization**: Keep your code clean and structured  
- **Maintenance**: Fix bugs or make changes in one place
- **Readability**: Make your code easier to understand

---

## Basic Function Syntax

Every function in Swift starts with the `func` keyword, followed by the function name, parentheses, and curly braces containing the code to execute.

```swift
func functionName() {
    // Code to execute
    print("Hello from a function!")
}
```

### Calling a Function

To use a function, you "call" it by writing its name followed by parentheses:

```swift
functionName()  // This executes the function
```

---

## Functions Without Parameters

The simplest functions take no input and just perform an action.

```swift
func sayHello() {
    print("Hello, Swift!")
}

func playSound() {
    print("🔊 Playing notification sound...")
}

func clearScreen() {
    print("🧹 Clearing the screen...")
}

// Calling the functions
sayHello()      // Prints: Hello, Swift!
playSound()     // Prints: 🔊 Playing notification sound...
clearScreen()   // Prints: 🧹 Clearing the screen...
```

---

## Functions With Parameters

Parameters allow functions to accept input values, making them more flexible and reusable.

### Single Parameter

```swift
func greet(name: String) {
    print("Hello, \(name)!")
}

func celebrate(event: String) {
    print("🎉 Congratulations on your \(event)!")
}

// Calling functions with arguments
greet(name: "Alice")                    // Hello, Alice!
celebrate(event: "graduation")          // 🎉 Congratulations on your graduation!
```

### Multiple Parameters

```swift
func introduce(firstName: String, lastName: String, age: Int) {
    print("Hi! I'm \(firstName) \(lastName) and I'm \(age) years old.")
}

func calculateRectangleArea(width: Double, height: Double) {
    let area = width * height
    print("The area is \(area) square units")
}

// Calling functions with multiple arguments
introduce(firstName: "John", lastName: "Doe", age: 25)
// Prints: Hi! I'm John Doe and I'm 25 years old.

calculateRectangleArea(width: 5.0, height: 3.0)
// Prints: The area is 15.0 square units
```

---

## Parameters vs Arguments

It's important to understand the difference between these terms:

- **Parameters**: The variables defined in the function declaration
- **Arguments**: The actual values passed when calling the function

```swift
func sendMessage(to recipient: String, message: String) {
    //              ↑ recipient and message are PARAMETERS
    print("Sending '\(message)' to \(recipient)")
}

sendMessage(to: "Mom", message: "I'll be home soon")
//             ↑ "Mom" and "I'll be home soon" are ARGUMENTS
```

---

## Practical Examples

### User Authentication

```swift
func loginUser(username: String, password: String) {
    print("🔐 Attempting to log in user: \(username)")
    print("📝 Password verification in progress...")
    print("✅ Login successful!")
}

loginUser(username: "developer123", password: "secretPass")
```

### Shopping Cart

```swift
func addToCart(item: String, quantity: Int) {
    print("📦 Adding \(quantity) x \(item) to your cart")
    print("🛒 Cart updated successfully!")
}

func removeFromCart(item: String) {
    print("🗑️ Removing \(item) from your cart")
}

addToCart(item: "iPhone", quantity: 1)
addToCart(item: "AirPods", quantity: 2)
removeFromCart(item: "iPhone")
```

### Temperature Converter

```swift
func convertToFahrenheit(celsius: Double) {
    let fahrenheit = (celsius * 9/5) + 32
    print("\(celsius)°C is equal to \(fahrenheit)°F")
}

func convertToCelsius(fahrenheit: Double) {
    let celsius = (fahrenheit - 32) * 5/9
    print("\(fahrenheit)°F is equal to \(celsius)°C")
}

convertToFahrenheit(celsius: 25.0)    // 25.0°C is equal to 77.0°F
convertToCelsius(fahrenheit: 77.0)    // 77.0°F is equal to 25.0°C
```

---

## Function Naming Best Practices

Good function names make your code self-documenting:

```swift
// ✅ Good function names - clear and descriptive
func calculateTax(amount: Double, rate: Double) { }
func validateEmail(address: String) { }
func downloadUserProfile(userID: Int) { }
func formatCurrency(amount: Double) { }

// ❌ Poor function names - vague and unclear
func doStuff(x: Double, y: Double) { }
func check(str: String) { }
func get(id: Int) { }
func format(num: Double) { }
```

**Naming Guidelines:**
- Use verbs to describe what the function does
- Be specific about the action performed
- Use camelCase (first letter lowercase, subsequent words capitalized)
- Make names readable and self-explanatory

---

## Common Beginner Mistakes

### 1. Forgetting Parentheses When Calling

```swift
func showWelcomeMessage() {
    print("Welcome to our app!")
}

// ❌ Wrong - this doesn't call the function
showWelcomeMessage

// ✅ Correct - this calls the function
showWelcomeMessage()
```

### 2. Parameter Label Confusion

```swift
func createUser(name: String, email: String) {
    print("Creating user: \(name) with email: \(email)")
}

// ❌ Wrong - missing parameter labels
createUser("John", "john@email.com")

// ✅ Correct - includes parameter labels
createUser(name: "John", email: "john@email.com")
```

### 3. Case Sensitivity

```swift
func calculateTotal() {
    print("Calculating total...")
}

// ❌ Wrong - function names are case-sensitive
calculatetotal()  // This won't work
CALCULATETOTAL()  // This won't work either

// ✅ Correct - exact case match
calculateTotal()
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Functions are reusable blocks of code that perform specific tasks
- ✅ All functions start with the `func` keyword followed by a name and parentheses
- ✅ Functions without parameters perform the same action every time they're called
- ✅ Parameters allow functions to accept input values for more flexibility
- ✅ Arguments are the actual values passed when calling a function
- ✅ Good function naming makes code self-documenting and easier to understand
- ✅ Functions help organize code, prevent repetition, and make maintenance easier

#### Where to Go Next
**Continue to** [Functions - Parameters and Return Types](/Swift%20Fundamentals/Beginner/04-Functions/02-Functions%20Parameters%20and%20Return%20Types.md)

---

## 📚 Resources 
- [The Swift Programming Language - Functions](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/)
