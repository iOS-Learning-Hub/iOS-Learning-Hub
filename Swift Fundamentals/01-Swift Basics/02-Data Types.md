# Data Types in Swift

## 🎯 Learning Objectives

By the end of this lesson, you will:
- Understand Swift's fundamental data types
- Know when to use each data type
- Master type conversion and type safety
- Handle different number types effectively

---

## 📖 What are Data Types?

Swift provides many fundamental data types, including:

- **Int**: Whole numbers (1, 43, -10)
- **Double**: Decimal numbers (3.14, -0.5, 1999.88)
- **String**: Text ("Hello", "Swift is awesome!")
- **Bool**: True or false values
- **Character**: Single characters ('A', '🥳', '7')

Swift is a **type-safe** language, meaning it prevents you from mixing incompatible types accidentally.

--- 

## 🔢 Number Types

### Integers (Int)
```
let age = 25
let temperature = -5
let maxScore = 1000
let year = 2024

// Large numbers (Swift handles big integers)
let worldPopulation = 8_000_000_000  // Underscores for readability
let distanceToSun = 93_000_000       // 93 million miles
```

### Floating-Point Numbers

#### Double(Default for decimals)

```
let pi = 3.14159
let accountBalance = 1234.56
let temperature = 98.6
let percentage = 85.5

```

#### Float (Less precision, smaller memory)

```
let smallDecimal: Float = 2.5
let ratio: Float = 0.333
```


---

## 📝 Text Types

### String
For text of any length
```
let firstName = "Emma"
let lastName = "Johnson"
let fullName = firstName + " " + lastName    // "Emma Johnson"

// Multi-word strings
let message = "Welcome to Swift programming!"
let address = "123 Main Street, San Francisco, CA"

// Empty strings
let emptyString = ""
let anotherEmpty = String()
```


### Character
For single characters:
```
let firstLetter: Character = "A"
let emoji: Character = "🎉"
let digit: Character = "7"
let symbol: Character = "@"

// ❌ This won't work - too many characters
// let wrongCharacter: Character = "AB"  // Error!
```

---

## ✅ Boolean Type
For true/false values:
```
let isLoggedIn = true
let isGameOver = false
let hasInternet = true
let isWeekend = false

// Useful for conditions
let canPlay = isLoggedIn && hasInternet && !isGameOver
```

---

## 🔄 Type Conversion
Swift requires explicit type conversion - it won't guess what you want:

**Number conversions**
```
let wholeNumber = 42
let decimalNumber = 3.14

// ❌ This doesn't work
// let result = wholeNumber + decimalNumber  // Error!

// ✅ Convert explicitly
let result1 = Double(wholeNumber) + decimalNumber    // 45.14
let result2 = wholeNumber + Int(decimalNumber)       // 45 (loses decimal)
```

**String Conversions**
```
let age = 25
let score = 98.5
let isWinner = true

// Convert to strings
let ageText = String(age)           // "25"
let scoreText = String(score)       // "98.5"
let winnerText = String(isWinner)   // "true"

// Convert strings to numbers
let numberString = "123"
let convertedNumber = Int(numberString)    // Optional Int (might fail)
```

**Practical Example**
```
// User input (always comes as String)
let userInput = "42"
let userAge = Int(userInput) ?? 0    // Convert with fallback

// Display calculations
let height = 5.8
let weight = 150
let bmi = weight / (height * height)
let bmiText = "Your BMI is \(bmi)"
```

---

## 🛫 Next Steps
Now that you understand the principal data types in Swift, you're ready to continue your journey in the Swift Basics path.

#### What You've Learned
- ✅ **Fundamental Data Types:** Data types used and supported in Swift
- ✅ **Type Conversion:** Convert different data types into other ones
- ✅ **Type Safety:** How Swift prevents you to mix different data types

#### Where to Go Next
**Continue to** [Swift Basics - Operators](/Swift%20Fundamentals/01-Swift%20Basics/03-Operators.md)

---

## 📚 Resources

- [The Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/thebasics)
- [Apple Swift Documentation](https://developer.apple.com/documentation/swift)