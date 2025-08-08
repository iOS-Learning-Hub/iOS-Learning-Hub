# Functions - Advanced Functions

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand functions as first-class types and how to use them as variables
- Master nested functions and their scope rules
- Know how to create and use higher-order functions
- Understand closures and their relationship to functions
- Be able to use function types as parameters and return values
- Master advanced concepts like function composition and currying
- Understand when and how to use escaping and non-escaping closures

---

## Functions as First-Class Types

In Swift, functions are first-class types, meaning they can be:
- Stored in variables and constants
- Passed as parameters to other functions
- Returned from functions
- Used in collections

### Storing Functions in Variables

```swift
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

func multiply(_ a: Int, _ b: Int) -> Int {
    return a * b
}

// Store functions in variables
let operation: (Int, Int) -> Int = add
let anotherOperation = multiply

// Use them like regular functions
let sum = operation(5, 3)        // 8
let product = anotherOperation(4, 7)  // 28

// You can even change which function the variable points to
var currentOperation = add
currentOperation = multiply  // Now points to multiply function
```

### Function Type Annotations

```swift
// Function type: (ParameterTypes) -> ReturnType
var mathOperation: (Double, Double) -> Double

func divide(_ a: Double, _ b: Double) -> Double {
    return a / b
}

func power(_ base: Double, _ exponent: Double) -> Double {
    return pow(base, exponent)
}

mathOperation = divide
let result1 = mathOperation(10, 2)  // 5.0

mathOperation = power
let result2 = mathOperation(2, 3)   // 8.0
```

---

## Higher-Order Functions

Higher-order functions are functions that take other functions as parameters or return functions as results.

### Functions That Take Functions as Parameters

```swift
func processNumbers(_ numbers: [Int], using operation: (Int) -> Int) -> [Int] {
    var result: [Int] = []
    for number in numbers {
        result.append(operation(number))
    }
    return result
}

func double(_ x: Int) -> Int {
    return x * 2
}

func square(_ x: Int) -> Int {
    return x * x
}

let numbers = [1, 2, 3, 4, 5]
let doubled = processNumbers(numbers, using: double)  // [2, 4, 6, 8, 10]
let squared = processNumbers(numbers, using: square)  // [1, 4, 9, 16, 25]
```

### Generic Higher-Order Functions

```swift
func transform<T, U>(_ items: [T], using function: (T) -> U) -> [U] {
    var result: [U] = []
    for item in items {
        result.append(function(item))
    }
    return result
}

func stringLength(_ text: String) -> Int {
    return text.count
}

func isEven(_ number: Int) -> Bool {
    return number % 2 == 0
}

let words = ["Hello", "Swift", "Programming"]
let lengths = transform(words, using: stringLength)  // [5, 5, 11]

let nums = [1, 2, 3, 4, 5]
let evenChecks = transform(nums, using: isEven)      // [false, true, false, true, false]
```

---

## Functions Returning Functions

Functions can create and return other functions:

```swift
func makeMultiplier(factor: Int) -> (Int) -> Int {
    func multiply(number: Int) -> Int {
        return number * factor
    }
    return multiply
}

let tripler = makeMultiplier(factor: 3)
let quadrupler = makeMultiplier(factor: 4)

print(tripler(5))    // 15
print(quadrupler(5)) // 20
```

### Practical Example: Logger Factory

```swift
func createLogger(prefix: String, level: String) -> (String) -> Void {
    return { message in
        let timestamp = Date()
        print("[\(timestamp)] [\(level)] \(prefix): \(message)")
    }
}

let errorLogger = createLogger(prefix: "UserAuth", level: "ERROR")
let infoLogger = createLogger(prefix: "UserAuth", level: "INFO")

errorLogger("Failed to authenticate user")
infoLogger("User logged in successfully")
```

---

## Nested Functions

Nested functions are functions defined inside other functions. They have access to variables and parameters of their enclosing function.

```swift
func calculateStatistics(numbers: [Double]) -> (average: Double, median: Double) {
    
    // Nested function to calculate average
    func calculateAverage() -> Double {
        let sum = numbers.reduce(0, +)
        return sum / Double(numbers.count)
    }
    
    // Nested function to calculate median
    func calculateMedian() -> Double {
        let sorted = numbers.sorted()
        let count = sorted.count
        
        if count % 2 == 0 {
            return (sorted[count/2 - 1] + sorted[count/2]) / 2
        } else {
            return sorted[count/2]
        }
    }
    
    return (calculateAverage(), calculateMedian())
}

let data = [1.0, 2.0, 3.0, 4.0, 5.0]
let stats = calculateStatistics(numbers: data)
print("Average: \(stats.average), Median: \(stats.median)")  // Average: 3.0, Median: 3.0
```

### Nested Functions with Closure Capture

```swift
func makeCounter(startingAt initialValue: Int = 0) -> () -> Int {
    var count = initialValue
    
    func increment() -> Int {
        count += 1
        return count
    }
    
    return increment  // Returns the nested function
}

let counter1 = makeCounter(startingAt: 10)
let counter2 = makeCounter()

print(counter1())  // 11
print(counter1())  // 12
print(counter2())  // 1
print(counter1())  // 13
print(counter2())  // 2
```

---

## Closures and Function Relationships

Closures are unnamed functions that can capture values from their surrounding context.

### Closure Syntax

```swift
// Full closure syntax
let doubleNumbers = numbers.map({ (number: Int) -> Int in
    return number * 2
})

// Simplified - Swift can infer types
let tripleNumbers = numbers.map({ number in
    return number * 3
})

// Even more simplified - single expression
let quadrupleNumbers = numbers.map({ number in number * 4 })

// Shortest form - using shorthand argument names
let quintupleNumbers = numbers.map({ $0 * 5 })

// Trailing closure syntax
let sextupleNumbers = numbers.map { $0 * 6 }
```

### Closures vs Functions

```swift
// Function version
func isPositive(_ number: Int) -> Bool {
    return number > 0
}

let positiveNumbers1 = numbers.filter(isPositive)

// Closure version
let positiveNumbers2 = numbers.filter { $0 > 0 }

// Both produce the same result!
```

---

## Common Higher-Order Functions

Swift's standard library provides powerful higher-order functions:

### Map - Transform Elements

```swift
let prices = [19.99, 29.99, 39.99, 49.99]

// Convert to strings with currency formatting
let formattedPrices = prices.map { price in
    String(format: "$%.2f", price)
}
// ["$19.99", "$29.99", "$39.99", "$49.99"]

// Add tax
let pricesWithTax = prices.map { $0 * 1.08 }
// [21.5892, 32.3892, 43.1892, 53.9892]
```

### Filter - Select Elements

```swift
let ages = [16, 18, 21, 25, 30, 17, 22]

// Filter adults (18+)
let adults = ages.filter { $0 >= 18 }
// [18, 21, 25, 30, 22]

// Filter young adults (18-25)
let youngAdults = ages.filter { age in
    age >= 18 && age <= 25
}
// [18, 21, 25, 22]
```

### Reduce - Combine Elements

```swift
let scores = [85, 92, 78, 96, 88]

// Calculate total
let total = scores.reduce(0) { accumulator, score in
    accumulator + score
}
// 439

// Find maximum (alternative to max())
let maximum = scores.reduce(0) { currentMax, score in
    score > currentMax ? score : currentMax
}
// 96

// Concatenate strings
let words = ["Swift", "is", "awesome"]
let sentence = words.reduce("") { result, word in
    result.isEmpty ? word : result + " " + word
}
// "Swift is awesome"
```

### Sorted - Arrange Elements

```swift
let students = ["Alice", "Bob", "Charlie", "Diana"]

// Sort alphabetically
let alphabetical = students.sorted()
// ["Alice", "Bob", "Charlie", "Diana"]

// Sort by length
let byLength = students.sorted { $0.count < $1.count }
// ["Bob", "Alice", "Diana", "Charlie"]

// Custom sorting
struct Student {
    let name: String
    let grade: Int
}

let classList = [
    Student(name: "Alice", grade: 85),
    Student(name: "Bob", grade: 92),
    Student(name: "Charlie", grade: 78)
]

let topStudents = classList.sorted { $0.grade > $1.grade }
// Sorted by grade (highest first)
```

---

## Escaping and Non-Escaping Closures

### Non-Escaping Closures (Default)

Most closures are non-escaping, meaning they're called before the function returns:

```swift
func processData(_ data: [Int], operation: (Int) -> Int) -> [Int] {
    return data.map(operation)  // Closure is called immediately
}

let result = processData([1, 2, 3]) { $0 * 2 }
// [2, 4, 6]
```

### Escaping Closures

Escaping closures can be stored and called after the function returns:

```swift
var storedClosures: [() -> Void] = []

func storeTask(_ task: @escaping () -> Void) {
    storedClosures.append(task)  // Closure "escapes" the function
}

func executeTasks() {
    for task in storedClosures {
        task()
    }
    storedClosures.removeAll()
}

// Usage
storeTask { print("Task 1 completed") }
storeTask { print("Task 2 completed") }
storeTask { print("Task 3 completed") }

executeTasks()
// Prints all three messages
```

### Practical Example: Asynchronous Operations

```swift
class NetworkManager {
    typealias CompletionHandler = (String?, Error?) -> Void
    
    func fetchData(completion: @escaping CompletionHandler) {
        // Simulate async operation
        DispatchQueue.global().asyncAfter(deadline: .now() + 2) {
            // This closure escapes because it's called after the function returns
            completion("Data received", nil)
        }
    }
}

let manager = NetworkManager()
manager.fetchData { data, error in
    if let data = data {
        print("Success: \(data)")
    } else if let error = error {
        print("Error: \(error)")
    }
}
```

---

## Function Composition

Function composition allows you to combine simple functions to create more complex ones:

```swift
func add10(_ x: Int) -> Int {
    return x + 10
}

func multiply2(_ x: Int) -> Int {
    return x * 2
}

func compose<T>(_ f: @escaping (T) -> T, _ g: @escaping (T) -> T) -> (T) -> T {
    return { x in f(g(x)) }
}

let add10ThenMultiply2 = compose(multiply2, add10)
let result = add10ThenMultiply2(5)  // (5 + 10) * 2 = 30

// Create a pipeline of operations
func pipeline<T>(_ value: T, _ operations: ((T) -> T)...) -> T {
    return operations.reduce(value) { result, operation in
        operation(result)
    }
}

let finalResult = pipeline(5, add10, multiply2, add10)  // ((5 + 10) * 2) + 10 = 40
```

---

## Currying

Currying transforms a function with multiple parameters into a series of functions with single parameters:

```swift
// Regular function
func add(_ a: Int, _ b: Int) -> Int {
    return a + b
}

// Curried version
func curriedAdd(_ a: Int) -> (Int) -> Int {
    return { b in a + b }
}

let add5 = curriedAdd(5)
let result1 = add5(3)  // 8
let result2 = add5(7)  // 12

// Generic currying function
func curry<A, B, C>(_ function: @escaping (A, B) -> C) -> (A) -> (B) -> C {
    return { a in { b in function(a, b) } }
}

let curriedMultiply = curry { (a: Int, b: Int) in a * b }
let multiplyBy3 = curriedMultiply(3)
print(multiplyBy3(4))  // 12
```

---

## Real-World Advanced Examples

### Custom Array Extension with Higher-Order Functions

```swift
extension Array {
    func asyncMap<T>(_ transform: @escaping (Element) -> T, completion: @escaping ([T]) -> Void) {
        let group = DispatchGroup()
        var results: [T?] = Array(repeating: nil, count: self.count)
        
        for (index, element) in self.enumerated() {
            group.enter()
            DispatchQueue.global().async {
                let result = transform(element)
                results[index] = result
                group.leave()
            }
        }
        
        group.notify(queue: .main) {
            completion(results.compactMap { $0 })
        }
    }
    
    func partition(by predicate: (Element) -> Bool) -> ([Element], [Element]) {
        var matching: [Element] = []
        var nonMatching: [Element] = []
        
        for element in self {
            if predicate(element) {
                matching.append(element)
            } else {
                nonMatching.append(element)
            }
        }
        
        return (matching, nonMatching)
    }
}

// Usage
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let (evens, odds) = numbers.partition { $0 % 2 == 0 }
print("Evens: \(evens)")  // [2, 4, 6, 8, 10]
print("Odds: \(odds)")    // [1, 3, 5, 7, 9]
```

### Functional Programming Pipeline

```swift
struct User {
    let name: String
    let age: Int
    let isActive: Bool
    let email: String
}

let users = [
    User(name: "Alice", age: 25, isActive: true, email: "alice@example.com"),
    User(name: "Bob", age: 17, isActive: false, email: "bob@example.com"),
    User(name: "Charlie", age: 30, isActive: true, email: "charlie@example.com"),
    User(name: "Diana", age: 22, isActive: true, email: "diana@example.com")
]

// Functional pipeline to get emails of active adult users
let adultActiveUserEmails = users
    .filter { $0.age >= 18 }           // Filter adults
    .filter { $0.isActive }            // Filter active users
    .map { $0.email.lowercased() }     // Convert emails to lowercase
    .sorted()                          // Sort alphabetically

print(adultActiveUserEmails)
// ["alice@example.com", "charlie@example.com", "diana@example.com"]

// Alternative: Using a single chain with multiple conditions
let result = users
    .filter { $0.age >= 18 && $0.isActive }
    .map { $0.email.lowercased() }
    .sorted()
```

### Advanced Calculator with Function Composition

```swift
typealias MathOperation = (Double) -> Double
typealias BinaryOperation = (Double, Double) -> Double

class FunctionalCalculator {
    private var operations: [MathOperation] = []
    
    func add(_ operation: @escaping MathOperation) -> FunctionalCalculator {
        operations.append(operation)
        return self
    }
    
    func compute(_ initialValue: Double) -> Double {
        return operations.reduce(initialValue) { result, operation in
            operation(result)
        }
    }
    
    func clear() -> FunctionalCalculator {
        operations.removeAll()
        return self
    }
    
    // Factory methods for common operations
    static func add(_ value: Double) -> MathOperation {
        return { $0 + value }
    }
    
    static func multiply(_ value: Double) -> MathOperation {
        return { $0 * value }
    }
    
    static func power(_ exponent: Double) -> MathOperation {
        return { pow($0, exponent) }
    }
    
    static func root(_ index: Double) -> MathOperation {
        return { pow($0, 1.0 / index) }
    }
}

// Usage
let calculator = FunctionalCalculator()

let result = calculator
    .add(FunctionalCalculator.add(10))      // Add 10
    .add(FunctionalCalculator.multiply(2))   // Multiply by 2
    .add(FunctionalCalculator.power(2))      // Square it
    .add(FunctionalCalculator.root(2))       // Square root
    .compute(5)                              // Start with 5

print("Result: \(result)")  // ((5 + 10) * 2)² = 30
```

---

## Performance Considerations

### When to Use Higher-Order Functions

```swift
// ✅ Good: Readable and expressive
let processedData = rawData
    .filter { $0.isValid }
    .map { $0.processed() }
    .sorted { $0.priority > $1.priority }

// ❌ Be careful: Multiple passes through large datasets
// This creates intermediate arrays
let hugArray = Array(1...1_000_000)
let result = hugArray
    .filter { $0 % 2 == 0 }     // Pass 1: Creates array of ~500k elements
    .map { $0 * $0 }            // Pass 2: Creates another array
    .filter { $0 > 1000 }       // Pass 3: Creates final array

// ✅ Better: Single pass with lazy evaluation
let lazyResult = hugArray
    .lazy
    .filter { $0 % 2 == 0 }
    .map { $0 * $0 }
    .filter { $0 > 1000 }

let finalArray = Array(lazyResult)  // Only one allocation
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Functions are first-class types that can be stored, passed, and returned
- ✅ Higher-order functions take other functions as parameters or return functions
- ✅ Nested functions have access to their enclosing function's variables
- ✅ Closures are unnamed functions that can capture values from their context
- ✅ Escaping closures can be stored and called after their containing function returns
- ✅ Function composition allows combining simple functions into complex ones
- ✅ Swift's built-in higher-order functions (map, filter, reduce) enable functional programming
- ✅ Understanding these concepts enables writing more expressive and maintainable code

#### Where to Go Next
**Continue to** [Intermediate - Enumerations](/Swift%20Fundamentals/Intermediate/01-Enumerations/01-Enumerations.md)

---

## 📚 Resources 
- [The Swift Programming Language - Function Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions#Function-Types)
