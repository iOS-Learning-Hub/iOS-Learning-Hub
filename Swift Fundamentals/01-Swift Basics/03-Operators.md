# Operators

## 🎯 Learning Objectives

By the end of this lesson you will:
- Understand what are operators and how they work in Swift
- Know how to use each of them according to your needs

--- 

## What are operators?
An operator is a special symbol or phrase that you use to check, change, or combine values. Swift supports the operators you may already know from languages like C, and improves several capabilities to eliminate common coding errors. 


### Assignment Operator

The assignment operator (a = b) initializes or updates the value of a with the value of b:

```
let b = 10
var a = 5
a = b
// a is now equal to 10
```

### Arithmetic Operators

Swift supports the four standard *arithmetic operators* for all number types:

**Addition(+)**

```
1 + 2      // equals 3
```

**Subtraction(-)**

```
5 - 2      // equals 3
```

**Multiplication(*)**

```
2 * 3      // equals 6
```

**Division (/)**

```
10.0 / 2.5     // equals 4.0
```

### Remainder Operator
The remainder operator (a % b) works out how many multiples of b will fit inside a and returns the value that's left over (known as the *remainder*).

>Note: 
The remainder operator (%) is also known as *modulo operator* in other languages. However, its behavior in Swift for negative numbers means that, strictly speaking, it's a remainder rather than a modulo operation.

` 9 % 4 // equals 1`


--- 
### Compound Assignment Operators

Swift provides *compound assignment operators* that combine assignment (=) with another operation. 

**Addition Assignment Operator**
```
var a = 1
a += 2
// a is now equal to 3
```

**Subtraction Assignment Operator**
```
var a = 6
a -= 2
// a is now equal to 4
```

**Multiplication Assignment Operator**
```
var a = 3
a *= 7
// a is now equal to 21
```

**Division Assignment Operator**
```
var a = 10
a /= 5
// a is now equal to 2
```

### Comparison Operators

Swift supports the following comparison operators:
- Equal to (a == b)
- Not equal to (a != b)
- Greater than (a > b)
- Less than (a < b)
- Greater than or equal to (a >= b)
- Less than or equal to (a <= b)

> Note
> Swift also provides two *identity operators* (=== and !==), which you use to test whether two object references both refer to the same object instance. For more information, see [Identity Operators](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Identity-Operators).

Each of the comparison operators returns a `Bool` value to indicate whether or not the statement is true:

```
1 == 1  // true because 1 is equal to 1
2 != 1  // true because 2 is not equal to 1
2 > 1   // true because 2 is greater than 1
1 < 2   // true because 1 is less than 2
1 >= 1  // true because 1 is greater than or equal to 1
2 <= 1  // false because 2 isn't less than or equal to 1

```

### Ternary Conditional Operator
It's a shortcut for evaluating one of two expressions based on whether `question` is true or false. Its parts are: 
`question ? answer1 : answer2`

If `question` is true, it evaluates `answer1` and returns its value; otherwise, it evaluates `answer2` and returns its value.

```
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```


### Nil-Coalescing Operator
The *nil-coalescing operator* (a ?? b) unwraps and optional a if it contains a value, or returns a default value b if a is `nil`. The expression a is always of an optional type. The expression b must match the type that's stored inside a.

> Note
If the value of a is non-nil, the value of b isn't evaluated. This is known as *short-circuit evaluation*.

```
let defaultColorName = "red"
var userDefinedColorName: String?   // defaults to nil

var colorNameToUse = userDefinedColorName ?? defaultColorName
// userDefinedColorName is nil, so colorNameToUse is set to default of "red"
```

### Range Operators

#### Closed Range Operator
The *closed range operator* (a..b) defines a range that runs from a to b, and includes the values of a and b. The value of a must not be greater than b.

```
for index in 1..5 {
    print("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```
#### Half-Open Range Operator
The *half-open range operator* (a..< b) defines a range that runs from a to b, but doesn't include b. It's said to be *half-open* because it contains its first value, but not its final value. The value of a must not be greater than b.

```
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..<count {
    print("Person \(i + 1) is called \(names[i]))
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```
Note that the array contains four items, but 0..< count only counts as far as 3 (the index of the last item in the array), because it's a half-open range.

#### One-Sided Ranges

### Logical Operators
*Logical operators* modify or combine the Boolean logic values `true` and `false`. Swift supports the three standard logical operators found in C-based languages.
- Logical NOT (!a)
- Logical AND (a && b)
- Logical OR (a || b)

#### Logical NOT operator
The *logical NOT operator* (!a) inverts a Boolean value so that `true` becomes `false`, and `false` becomes `true`.

```
let allowedEntry = false
if !allowedEntry {
    print("ACCESS DENIED")
}
// Prints "ACCESS DENIED"
```

The phrase `if !allowedEntry` can be read as "if not allowed entry." The subsequent line is only executed if "not allowed entry" is true; that is, if `allowedEntry` is `false`.

#### Logical AND operator

#### Logical OR operator

--- 
## 🛫 Next Steps
Now that you understand more about the operators in Swift, you are one step closer to complete the Swift Basics and continue your journey in the iOS development path.

#### What You've Learned
- ✅ **Assignment Operator:**
- ✅ **Arithmetic Operators:**
- ✅ **Remainder Operator:**
- ✅ **Compound Assignment Operators:**
- ✅ **Ternary Conditional Operator:**
- ✅ **Nil-Coalescing Operator:**
- ✅ **Range Operators:**
- ✅ **Logical Operators:**


#### Where to Go Next

**Continue to** [Swift Basics - Comments and Documentation](/Swift%20Fundamentals/01-Swift%20Basics/04-Comments%20and%20Documentation.md)


---

## 📚 Resources
- [Basic Operators | The Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/basicoperators)