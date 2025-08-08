# Conditionals

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand how to use if statements to create conditional logic in Swift
- Master else and else if clauses to handle multiple conditions
- Learn when and how to implement switch statements for complex pattern matching
- Recognize the difference between if and switch statements and when to use each
- Write exhaustive switch statements with proper case handling and default clauses
- Apply conditional statements to solve real-world programming scenarios
  
---

## Conditional Statements

Swift provides two ways to add conditional branches to your code: the **if** statement and the **switch** statement.

### If
Used to evaluate simple conditions with only a few possibles outcomes

```swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold, consider wearing a scarf")
}
// Prints "It's very cold, consider wearing a scarf"
```

The **if** statement can provide an alternative set of statements, known as an *else clause*, for situations when the **if** condition is `false`. These statements are indicated by the `else` keyword.

```swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a T-shirt.")
}
// Prints "It's not that cold. Wear a T-shirt."
```

You can chain multiple if statements together to consider additional clauses.

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    print("It's really warm. Don't forget to wear sunscreen.")
} else {
    print("It's not that cold. Wear a T-shirt.")
}
// Prints "It's really warm. Don't forget to wear sunscreen."
```

### Switch
A switch statement considers a value and compares it against several possible matching patterns. It then executes an appropriate block of code, based on the first pattern that matches successfully. 

Every switch statement consists of multiple possible *cases*, each of which begins with the `case` keyword.

Every switch statement must be *exhaustive*. That is, every possible value of the type being considered must be matched by one of the switch cases. If it's not appropriate to provide a case for every possible value, you can define a `default` case to cover any values that aren't addressed explicitly. This default case must always appear last.

Here is an example of a switch statement in Swift:

```swift
let someCharacter: Character = "z"
switch someCharacter {
case "a":
    print("The first letter of the Latin alphabet")
case "z":
    print("The last letter of the Latin alphabet")
default:
    print("Some other character")
}
// Prints "The last letter of the Latin alphabet"
```

--- 

## 🛫 Next Steps

#### What You've Learned
- ✅ How to write basic if statements to execute code based on conditions
- ✅ Using else clauses to provide alternative execution paths
- ✅ Chaining multiple conditions with else if for complex decision trees
- ✅ Understanding switch statements for pattern matching and value comparison
- ✅ The importance of exhaustive switch statements in Swift
- ✅ When to use default cases in switch statements to handle unspecified values
- ✅ The differences between if and switch statements and when to choose each approach

#### Where to Go Next
**Continue to** [Control Flow - Loops](/Swift%20Fundamentals/Beginner/03-Control%20Flow/02-Loops.md)

---

## 📚 Resources 
- [The Swift Programming Language - Conditional Statements](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#Conditional-Statements)
  