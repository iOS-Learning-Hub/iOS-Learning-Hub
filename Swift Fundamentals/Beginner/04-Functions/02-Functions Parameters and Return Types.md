# Functions - Parameters and Return Types

## 🎯 Learning Objectives
By the end of this lesson you will:
- Master different types of function parameters (default values, variadic, inout)
- Understand how to use argument labels and parameter names effectively
- Know how to create functions that return values using return types
- Be able to return multiple values using tuples
- Understand optional return types and when to use them
- Master function overloading and type signatures

---

## Function Parameters Deep Dive

Parameters make functions flexible by allowing them to accept different inputs. Swift provides several powerful parameter features.

### Parameter Names and Argument Labels

Swift functions can have both parameter names (used inside the function) and argument labels (used when calling the function).

```swift
func greet(person name: String, from hometown: String) {
    //        ↑ argument label  ↑ parameter name
    print("Hello \(name)! Greetings from \(hometown)!")
}

// When calling, we use the argument labels
greet(person: "Alice", from: "New York")
// Inside the function, we use parameter names: name and hometown
```

### Omitting Argument Labels

Use an underscore `_` to omit argument labels when calling the function:

```swift
func add(_ a: Int, _ b: Int) {
    let result = a + b
    print("The sum is \(result)")
}

// No argument labels needed when calling
add(5, 3)  // The sum is 8

// Compare with labeled version:
func addNumbers(first a: Int, second b: Int) {
    let result = a + b
    print("The sum is \(result)")
}

addNumbers(first: 5, second: 3)  // Requires labels
```

---

## Default Parameter Values

You can provide default values for parameters, making them optional when calling the function:

```swift
func createUser(name: String, email: String, isAdmin: Bool = false, theme: String = "light") {
    print("Creating user: \(name)")
    print("Email: \(email)")
    print("Admin: \(isAdmin)")
    print("Theme: \(theme)")
}

// All these are valid calls:
createUser(name: "John", email: "john@email.com")
// Uses defaults: isAdmin = false, theme = "light"

createUser(name: "Jane", email: "jane@email.com", isAdmin: true)
// Uses default: theme = "light"

createUser(name: "Bob", email: "bob@email.com", isAdmin: true, theme: "dark")
// All parameters specified
```

### Best Practices for Default Parameters

```swift
// ✅ Good: Place parameters with defaults at the end
func setupServer(host: String, port: Int, ssl: Bool = true, timeout: Int = 30) { }

// ❌ Not recommended: Defaults in the middle can be confusing
func setupServer(host: String, ssl: Bool = true, port: Int, timeout: Int = 30) { }
```

---

## Variadic Parameters

Variadic parameters accept zero or more values of the same type:

```swift
func calculateAverage(_ numbers: Double...) {
    guard !numbers.isEmpty else {
        print("No numbers provided")
        return
    }
    
    let total = numbers.reduce(0, +)
    let average = total / Double(numbers.count)
    print("Average of \(numbers) is \(average)")
}

// Can call with different numbers of arguments:
calculateAverage(1.0, 2.0, 3.0, 4.0, 5.0)  // Average: 3.0
calculateAverage(10.0, 20.0)                // Average: 15.0
calculateAverage()                          // No numbers provided
```

### Practical Variadic Example

```swift
func logMessages(_ messages: String...) {
    let timestamp = Date()
    for message in messages {
        print("[\(timestamp)] \(message)")
    }
}

logMessages("User logged in", "Session started", "Dashboard loaded")
```

---

## In-Out Parameters

In-out parameters allow functions to modify variables passed to them:

```swift
func swapValues(_ a: inout Int, _ b: inout Int) {
    let temp = a
    a = b
    b = temp
}

var x = 10
var y = 20
print("Before swap: x = \(x), y = \(y)")  // x = 10, y = 20

swapValues(&x, &y)  // Note the & symbol
print("After swap: x = \(x), y = \(y)")   // x = 20, y = 10
```

### In-Out Parameter Rules

```swift
func updateScore(_ score: inout Int, bonus: Int) {
    score += bonus
}

var playerScore = 100
updateScore(&playerScore, bonus: 50)  // playerScore is now 150

// ❌ Cannot pass constants or literals to inout parameters
let constantScore = 100
// updateScore(&constantScore, bonus: 50)  // Error!
// updateScore(&200, bonus: 50)            // Error!
```

---

## Return Types

Functions can return values to the code that called them using the `->` syntax:

### Single Return Values

```swift
func calculateArea(width: Double, height: Double) -> Double {
    return width * height
}

func formatCurrency(amount: Double) -> String {
    return "$\(String(format: "%.2f", amount))"
}

func isEven(number: Int) -> Bool {
    return number % 2 == 0
}

// Using returned values
let area = calculateArea(width: 5.0, height: 3.0)  // 15.0
let price = formatCurrency(amount: 19.99)           // "$19.99"
let evenCheck = isEven(number: 7)                   // false
```

### Implicit Returns

For single-expression functions, you can omit the `return` keyword:

```swift
func double(_ number: Int) -> Int {
    number * 2  // Implicit return
}

func getGreeting(for name: String) -> String {
    "Hello, \(name)!"  // Implicit return
}

func isPositive(_ number: Double) -> Bool {
    number > 0  // Implicit return
}
```

---

## Multiple Return Values with Tuples

Functions can return multiple values grouped in tuples:

```swift
func getNameComponents(fullName: String) -> (first: String, last: String) {
    let components = fullName.split(separator: " ")
    let firstName = String(components.first ?? "")
    let lastName = String(components.last ?? "")
    return (firstName, lastName)
}

let name = getNameComponents(fullName: "John Doe")
print("First name: \(name.first)")   // John
print("Last name: \(name.last)")     // Doe

// You can also destructure the tuple
let (firstName, lastName) = getNameComponents(fullName: "Jane Smith")
print("Hello, \(firstName) \(lastName)!")  // Hello, Jane Smith!
```

### Complex Tuple Example

```swift
func analyzeText(_ text: String) -> (wordCount: Int, characterCount: Int, hasNumbers: Bool) {
    let words = text.split(separator: " ")
    let wordCount = words.count
    let characterCount = text.count
    let hasNumbers = text.contains { $0.isNumber }
    
    return (wordCount, characterCount, hasNumbers)
}

let analysis = analyzeText("Hello World 123")
print("Words: \(analysis.wordCount)")           // 3
print("Characters: \(analysis.characterCount)") // 13
print("Contains numbers: \(analysis.hasNumbers)") // true
```

---

## Optional Return Types

When a function might not be able to return a value, use optional return types:

```swift
func findFirstEven(in numbers: [Int]) -> Int? {
    for number in numbers {
        if number % 2 == 0 {
            return number
        }
    }
    return nil  // No even number found
}

// Using optional return
if let firstEven = findFirstEven(in: [1, 3, 6, 7, 8]) {
    print("First even number: \(firstEven)")  // 6
} else {
    print("No even numbers found")
}
```

### Safe Division Example

```swift
func safeDivide(_ a: Double, by b: Double) -> Double? {
    guard b != 0 else {
        return nil  // Cannot divide by zero
    }
    return a / b
}

if let result = safeDivide(10, by: 3) {
    print("Result: \(result)")  // 3.333...
} else {
    print("Division by zero is not allowed")
}
```

---

## Function Overloading

Swift allows multiple functions with the same name but different parameter types or counts:

```swift
func process(_ data: String) {
    print("Processing string: \(data)")
}

func process(_ data: Int) {
    print("Processing integer: \(data)")
}

func process(_ data: Double) {
    print("Processing double: \(data)")
}

func process(_ data: [String]) {
    print("Processing array of strings: \(data)")
}

// Swift chooses the correct function based on the argument type
process("Hello")           // Calls String version
process(42)               // Calls Int version
process(3.14)             // Calls Double version
process(["A", "B", "C"])  // Calls Array version
```

### Overloading with Different Parameter Counts

```swift
func createButton() -> String {
    return "Default Button"
}

func createButton(title: String) -> String {
    return "Button: \(title)"
}

func createButton(title: String, color: String) -> String {
    return "Button: \(title) (\(color))"
}

let btn1 = createButton()                              // "Default Button"
let btn2 = createButton(title: "Save")                 // "Button: Save"
let btn3 = createButton(title: "Save", color: "Blue")  // "Button: Save (Blue)"
```

---

## Real-World Examples

### User Registration System

```swift
func registerUser(
    username: String,
    email: String,
    password: String,
    newsletter: Bool = false
) -> (success: Bool, message: String) {
    
    // Validation
    guard username.count >= 3 else {
        return (false, "Username must be at least 3 characters")
    }
    
    guard email.contains("@") else {
        return (false, "Invalid email format")
    }
    
    guard password.count >= 8 else {
        return (false, "Password must be at least 8 characters")
    }
    
    // Registration logic here...
    print("Creating account for \(username)")
    if newsletter {
        print("Subscribing to newsletter")
    }
    
    return (true, "Registration successful!")
}

let result = registerUser(
    username: "john_doe",
    email: "john@example.com",
    password: "secretPass123",
    newsletter: true
)

if result.success {
    print("✅ \(result.message)")
} else {
    print("❌ \(result.message)")
}
```

### Shopping Cart Calculator

```swift
func calculateTotal(
    prices: Double...,
    taxRate: Double = 0.08,
    discountPercent: Double = 0.0
) -> (subtotal: Double, tax: Double, total: Double) {
    
    let subtotal = prices.reduce(0, +)
    let discountAmount = subtotal * (discountPercent / 100)
    let discountedSubtotal = subtotal - discountAmount
    let tax = discountedSubtotal * taxRate
    let total = discountedSubtotal + tax
    
    return (subtotal, tax, total)
}

let order = calculateTotal(
    prices: 29.99, 15.50, 8.75,
    taxRate: 0.095,
    discountPercent: 10.0
)

print("Subtotal: $\(String(format: "%.2f", order.subtotal))")
print("Tax: $\(String(format: "%.2f", order.tax))")
print("Total: $\(String(format: "%.2f", order.total))")
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Argument labels and parameter names provide flexibility in function calls
- ✅ Default parameters make function calls more convenient
- ✅ Variadic parameters accept multiple values of the same type
- ✅ In-out parameters allow functions to modify external variables
- ✅ Return types specify what kind of value a function gives back
- ✅ Tuples enable functions to return multiple values at once
- ✅ Optional return types handle cases where functions might fail
- ✅ Function overloading allows multiple functions with the same name but different signatures

#### Where to Go Next
**Continue to** [Functions - Advanced Functions](/Swift%20Fundamentals/Beginner/04-Functions/03-Functions%20Advanced.md)

---

## 📚 Resources 
- [The Swift Programming Language - Functions Parameters and Return Values](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/#Function-Parameters-and-Return-Values)
