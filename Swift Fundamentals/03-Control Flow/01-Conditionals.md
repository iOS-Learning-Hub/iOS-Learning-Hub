# Conditionals

## 🎯 Learning Objectives
By the end of this lesson you will:
  
---

## Conditional Statements

Swift provides two ways to add conditional branches to your code: the **if** statement and the **switch** statement.

### If
Used to evaluate simple conditions with only a few possibles outcomes

```
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    print("It's very cold, consider wearing a scarf")
}
// Prints "It's very cold, consider wearing a scarf"
```

The **if** statement can provide an alternative set of statements, known as an *else clause*, for situations when the **if** condition is `false`. These statements are indicated by the `else` keyword.

```
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    print("It's very cold. Consider wearing a scarf.")
} else {
    print("It's not that cold. Wear a T-shirt.")
}
// Prints "It's not that cold. Wear a T-shirt."
```

You can chain multiple if statements together to consider additional clauses.

```
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


--- 

## 🛫 Next Steps

#### What You've Learned
- ✅

#### Where to Go Next
**Continue to** [Control Flow - Loops](/Swift%20Fundamentals/02-control-flow/02-loops.md)

---

## 📚 Resources 
- []