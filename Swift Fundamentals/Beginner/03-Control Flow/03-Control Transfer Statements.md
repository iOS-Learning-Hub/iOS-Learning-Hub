# Control Transfer Statements

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand what control transfer statements are and why they're important
- Know how to use `break` to exit loops and switch statements early
- Master the `continue` statement to skip iterations in loops
- Learn when and how to use `fallthrough` in switch statements
- Understand how `return` works to exit functions and return values
- Know the basics of `throw` for error handling
- Be able to use labeled statements for precise control flow

---

## What Are Control Transfer Statements?

Control transfer statements are special keywords that change the normal flow of your code. Instead of executing statements one after another, these statements let you "jump" to different parts of your code or exit early from loops, functions, or switch statements.

Swift has five control transfer statements: `break`, `continue`, `fallthrough`, `return`, and `throw`. Think of them as traffic signals that direct the flow of your program.

---

## The Break Statement

The `break` statement immediately stops the execution of a loop or switch statement and jumps to the code that comes after it.

### Break in Loops

```swift
// Finding the first even number
for number in 1...10 {
    if number % 2 == 0 {
        print("Found first even number: \(number)")
        break  // Exit the loop immediately
    }
}
// Prints: "Found first even number: 2"
// Numbers 3-10 are never checked
```

### Break in Switch Statements

```swift
let grade = "B"
switch grade {
case "A":
    print("Excellent!")
case "B":
    print("Good job!")
    break  // Not required in Swift, but shows explicit exit
case "C":
    print("You can do better")
default:
    print("Keep trying!")
}
```

**Note:** Unlike other languages, Swift doesn't require `break` in switch statements because they don't automatically fall through to the next case.

---

## The Continue Statement

The `continue` statement skips the current iteration and moves to the next iteration of the loop.

```swift
// Print only odd numbers
for number in 1...5 {
    if number % 2 == 0 {
        continue  // Skip even numbers
    }
    print(number)
}
// Prints: 1, 3, 5
```

### Continue vs Break

```swift
print("=== Using Continue ===")
for i in 1...5 {
    if i == 3 {
        continue  // Skip only iteration 3
    }
    print(i)
}
// Prints: 1, 2, 4, 5

print("=== Using Break ===")
for i in 1...5 {
    if i == 3 {
        break  // Stop the entire loop at 3
    }
    print(i)
}
// Prints: 1, 2
```

---

## The Fallthrough Statement

The `fallthrough` keyword causes execution to continue to the next case in a switch statement, regardless of whether the pattern matches.

```swift
let number = 5
var description = "The number \(number) is"

switch number {
case 5:
    description += " equal to five"
    fallthrough  // Continue to next case
case 1, 3, 5, 7, 9:
    description += " and is odd"
default:
    break
}
print(description)
// Prints: "The number 5 is equal to five and is odd"
```

**Important:** `fallthrough` doesn't check the condition of the next case—it simply executes the code in the next case block.

---

## The Return Statement

The `return` statement exits a function and optionally returns a value to the caller.

### Return with Value

```swift
func calculateArea(width: Double, height: Double) -> Double {
    if width <= 0 || height <= 0 {
        return 0  // Early exit for invalid input
    }
    return width * height
}

let area = calculateArea(width: 5, height: 3)  // Returns 15
```

### Return without Value

```swift
func processUser(age: Int) {
    if age < 0 {
        print("Invalid age")
        return  // Exit function early
    }
    
    if age < 18 {
        print("Minor user")
        return  // Exit function early
    }
    
    print("Adult user")
    // Function ends here naturally
}
```

---

## The Throw Statement

The `throw` statement is used to throw an error and stop the current execution. This is part of Swift's error handling system.

```swift
enum ValidationError: Error {
    case tooShort
    case tooLong
}

func validatePassword(_ password: String) throws {
    if password.count < 6 {
        throw ValidationError.tooShort
    }
    if password.count > 20 {
        throw ValidationError.tooLong
    }
    print("Password is valid!")
}

// Using the throwing function
do {
    try validatePassword("hi")
} catch ValidationError.tooShort {
    print("Password is too short")
} catch ValidationError.tooLong {
    print("Password is too long")
}
```

---

## Labeled Statements

When you have nested loops or complex control structures, labels help you specify exactly which loop or statement you want to break or continue.

```swift
gameLoop: for round in 1...3 {
    print("Round \(round)")
    
    for attempt in 1...3 {
        print("  Attempt \(attempt)")
        
        if attempt == 2 && round == 2 {
            print("  Game over!")
            break gameLoop  // Break out of the outer loop
        }
    }
}
print("Game ended")

// Output:
// Round 1
//   Attempt 1
//   Attempt 2
//   Attempt 3
// Round 2
//   Attempt 1
//   Attempt 2
//   Game over!
// Game ended
```

---

## Practical Examples

### Password Strength Checker

```swift
func checkPasswordStrength(_ password: String) -> String {
    // Early returns for quick checks
    if password.count < 6 {
        return "Too short"
    }
    
    if password.count > 50 {
        return "Too long"
    }
    
    var hasNumber = false
    var hasUppercase = false
    var hasLowercase = false
    
    for character in password {
        if character.isNumber {
            hasNumber = true
            continue  // Found number, check next character
        }
        
        if character.isUppercase {
            hasUppercase = true
            continue
        }
        
        if character.isLowercase {
            hasLowercase = true
            continue
        }
    }
    
    // Check strength
    if hasNumber && hasUppercase && hasLowercase {
        return "Strong"
    } else {
        return "Weak"
    }
}
```

### Grade Calculator with Early Exit

```swift
func calculateLetterGrade(_ scores: [Int]) -> String {
    guard !scores.isEmpty else {
        return "No scores provided"
    }
    
    var total = 0
    var validScores = 0
    
    for score in scores {
        if score < 0 || score > 100 {
            continue  // Skip invalid scores
        }
        
        total += score
        validScores += 1
        
        // If we have enough valid scores, we can break early
        if validScores >= 10 {
            break
        }
    }
    
    guard validScores > 0 else {
        return "No valid scores"
    }
    
    let average = total / validScores
    
    switch average {
    case 90...100:
        return "A"
    case 80..<90:
        return "B"
    case 70..<80:
        return "C"
    case 60..<70:
        return "D"
    default:
        return "F"
    }
}
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Control transfer statements change the normal flow of code execution
- ✅ `break` exits loops and switch statements immediately
- ✅ `continue` skips the current iteration and moves to the next one
- ✅ `fallthrough` makes switch statements execute the next case
- ✅ `return` exits functions and can return values
- ✅ `throw` is used for error handling to stop execution and throw errors
- ✅ Labeled statements provide precise control over nested structures
- ✅ These statements help write more efficient and readable code

#### Where to Go Next
**Continue to** [Functions](/Swift%20Fundamentals/Beginner/04-Functions/01-Functions%20Basics.md)

---

## 📚 Resources 
- [The Swift Programming Language - Control Flow](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow/)
- [Swift Control Transfer Statements - Apple Documentation](https://developer.apple.com/documentation/swift)