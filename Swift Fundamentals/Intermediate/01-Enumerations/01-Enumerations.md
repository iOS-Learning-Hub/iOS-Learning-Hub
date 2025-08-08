# Swift Enumerations

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand what enumerations are and why they're useful in Swift
- Create basic enums with simple cases and raw values
- Work with associated values to store additional data
- Use enums with switch statements and control flow
- Implement the CaseIterable protocol for iterating over enum cases

---

## What are Enumerations?

Enumerations – usually called "enum" and pronounced "ee-num" - are a way for you to define your own kind of value in Swift. An enum (short for enumeration) is a user-defined data type that has a fixed set of related values.

An enumeration defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code.

## Basic Enum Declaration

The simplest way to create an enum is using the `enum` keyword:

```swift
enum WeatherType {
    case sunny
    case cloudy
    case rainy
    case windy
    case snowy
}

// Alternative syntax - all cases in one line
enum PaymentMethod {
    case creditCard, debitCard, paypal, applePay
}
```

### Using Enum Values

```swift
// Create a variable of enum type
var currentWeather: WeatherType
currentWeather = WeatherType.sunny

// Swift can infer the type, so you can use shorthand
var todaysWeather = WeatherType.cloudy
var tomorrowsWeather: WeatherType = .rainy  // Type already known
```

## Enums with Switch Statements

Enums are particularly useful inside switch/case blocks, particularly because Swift knows all the values your enum can have so it can ensure you cover them all.

```swift
enum PizzaSize {
    case small, medium, large
}

func getPizzaPrice(size: PizzaSize) -> Double {
    switch size {
    case .small:
        return 12.99
    case .medium:
        return 15.99
    case .large:
        return 18.99
    }
}

let price = getPizzaPrice(size: .medium)
print("Price: $\(price)")  // Price: $15.99
```

## Raw Values

In Swift, we can also assign values to each enum case. These values are called raw values.

```swift
// String raw values
enum Planet: String {
    case mercury = "Mercury"
    case venus = "Venus"
    case earth = "Earth"
    case mars = "Mars"
}

// Integer raw values (auto-incrementing)
enum HTTPStatusCode: Int {
    case ok = 200
    case notFound = 404
    case serverError = 500
}

// Access raw values
let planetName = Planet.earth.rawValue  // "Earth"
let statusCode = HTTPStatusCode.ok.rawValue  // 200
```

## Associated Values

In Swift, we can also attach additional information to an enum case.

```swift
enum Barcode {
    case upc(Int, Int, Int, Int)
    case qrCode(String)
}

// Create instances with associated values
let productBarcode = Barcode.upc(4, 85909, 51226, 3)
let websiteQR = Barcode.qrCode("https://apple.com")

// Extract associated values using switch
switch productBarcode {
case .upc(let numberSystem, let manufacturer, let product, let check):
    print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
case .qrCode(let productCode):
    print("QR code: \(productCode)")
}
```

## CaseIterable Protocol

Enums become especially powerful once you use the CaseIterable protocol to iterate over all cases.

```swift
enum Direction: CaseIterable {
    case north, south, east, west
}

// Iterate over all cases
for direction in Direction.allCases {
    print("Direction: \(direction)")
}

print("Total directions: \(Direction.allCases.count)")  // 4
```

### Methods in Enums

Enums can have computed properties and methods:

```swift
enum Device {
    case iPhone(model: String)
    case iPad(model: String)
    case mac(model: String)
    
    var category: String {
        switch self {
        case .iPhone:
            return "Mobile"
        case .iPad:
            return "Tablet"
        case .mac:
            return "Computer"
        }
    }
    
    func displayInfo() {
        switch self {
        case .iPhone(let model):
            print("iPhone model: \(model)")
        case .iPad(let model):
            print("iPad model: \(model)")
        case .mac(let model):
            print("Mac model: \(model)")
        }
    }
}

let myDevice = Device.iPhone(model: "15 Pro")
myDevice.displayInfo()  // iPhone model: 15 Pro
print(myDevice.category)  // Mobile
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ How to create and use basic enumerations
- ✅ Working with raw values and associated values
- ✅ Using enums with switch statements for control flow
- ✅ Implementing CaseIterable for iteration
- ✅ Adding methods and computed properties to enums

#### Where to Go Next
**Continue to** [Structure and Classes](/Swift%20Fundamentals/Intermediate/02-Structures%20and%20Classes/01-Introduction%20to%20Structures%20and%20Classes.md)

---

## 📚 Resources 
- [Swift Programming Language - Enumerations](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/enumerations/)
- [Swift Enum Tutorial - Hacking with Swift](https://www.hackingwithswift.com/read/0/14/enumerations)
- [Advanced Enum Patterns - Swift by Sundell](https://www.swiftbysundell.com/articles/the-power-of-switch-statements-in-swift/)