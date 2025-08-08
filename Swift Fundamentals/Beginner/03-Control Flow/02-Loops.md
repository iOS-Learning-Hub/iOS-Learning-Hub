# Loops

## 🎯 Learning Objectives
By the end of this lesson you will:
- Master for-in loops to iterate over collections, arrays, and ranges
- Understand how to use while loops for condition-based iteration
- Learn the difference between while and repeat-while loops
- Apply loops to solve common programming tasks like data processing and repeated operations
- Choose the appropriate loop type based on your specific use case and iteration requirements
- Work with string interpolation and loop variables effectively


---

## For-In Loops
You use the for-in loop to iterate over a sequence, such as items in an array, ranges of numbers, or characters in a string.

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    print("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

You can also use for-in loops with numeric ranges. This example prints the first few entries in a five-times table:

```swift
for index in 1...5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```
---

## While Loops
A while loop performs a set of statements until a condition becomes `false`. These kinds of loops are best used when the number of iterations isn't known before the first iteration begins. Swift provide two kinds of while loops:
- `while` evaluates its condition at the start of each pass through the loop
- `repeat-while` evaluates its condition at the end of each pass through the loop
  
### While
A `while` loop starts by evaluating a single condition. If the condition is `true`, a set of statements is repeated until the condition becomes false.

Here is the general form of a `while` loop:
```
while <#condition#> {
   <#statements#>
}
```

### Repeat-While
The other variation of the `while` loop, known as the `repeat-while` loop, performs a single pass through the loop block first, *before* considering the loop's condition. It then continues to repeat the loop until the condition is `false`.

> Note
> The repeat-while loop in Swift is analogous to a `do-while` loop in other languages.

Here is the general form of a `repeat-while` loop:

```swift
repeat {
   <#statements#>
} while <#condition#>
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ How to use for-in loops to iterate over arrays, collections, and sequences
- ✅ Working with numeric ranges (1...5) in for-in loops for counting operations
- ✅ Understanding while loops for condition-based iteration with unknown iteration counts
- ✅ The difference between while and repeat-while loops and when to use each
- ✅ How repeat-while guarantees at least one execution before checking the condition
- ✅ Proper syntax and structure for all three loop types in Swift
- ✅ Using string interpolation with loop variables to display dynamic content

#### Where to Go Next
Continue to [Control Transfer Statements](/Swift%20Fundamentals/Beginner/03-Control%20Flow/03-Control%20Transfer%20Statements.md)

## 📚 Resources
- [The Swift Programming Language - Loops](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/controlflow#For-In-Loops)
