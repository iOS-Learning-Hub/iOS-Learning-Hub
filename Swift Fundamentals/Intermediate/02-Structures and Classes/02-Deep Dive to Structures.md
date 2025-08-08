# Structures Deep Dive

## 🎯 Learning Objectives
By the end of this lesson you will:
- Create structures with various property types
- Implement computed properties and property observers
- Use mutating methods to modify struct properties
- Work with static properties and methods
- Understand memberwise initializers and custom initializers

---

## Creating Structures

Structures are defined using the `struct` keyword followed by a name and body containing properties and methods.

```swift
struct Temperature {
    var celsius: Double
    var fahrenheit: Double {
        get {
            return celsius * 9 / 5 + 32
        }
        set {
            celsius = (newValue - 32) * 5 / 9
        }
    }
    
    init(celsius: Double) {
        self.celsius = celsius
    }
    
    init(fahrenheit: Double) {
        self.celsius = (fahrenheit - 32) * 5 / 9
    }
}

let temp = Temperature(celsius: 25)
print(temp.fahrenheit) // 77.0
```

## Property Types

### Stored Properties

Stored properties hold values as part of the instance

```swift
struct User {
    var username: String
    var email: String
    var isActive: Bool = true  // Default value
    let id: UUID = UUID()     // Constant property
}

var user = User(username: "john_doe", email: "john@example.com")
print(user.id) // Unique identifier
```

### Computed Properties

Computed properties calculate values rather than storing them

```swift
struct Rectangle {
    var width: Double
    var height: Double
    
    // Read-only computed property
    var area: Double {
        return width * height
    }
    
    // Read-write computed property
    var perimeter: Double {
        get {
            return 2 * (width + height)
        }
        set {
            // Assuming square for simplicity
            let side = newValue / 4
            width = side
            height = side
        }
    }
}

var rect = Rectangle(width: 5, height: 3)
print(rect.area)      // 15.0
print(rect.perimeter) // 16.0

rect.perimeter = 20
print(rect.width)     // 5.0
```

### Property Observers

Property observers respond to changes in property values

```swift
struct BankAccount {
    var balance: Double = 0.0 {
        willSet {
            print("About to set balance to \(newValue)")
        }
        didSet {
            if balance < 0 {
                print("Warning: Account balance is negative!")
            }
            print("Balance changed from \(oldValue) to \(balance)")
        }
    }
}

var account = BankAccount()
account.balance = 100.0
account.balance = -50.0
```

## Methods

### Instance Methods

```swift
struct Counter {
    var value: Int = 0
    
    func getValue() -> Int {
        return value
    }
    
    // Mutating method to modify properties
    mutating func increment() {
        value += 1
    }
    
    mutating func increment(by amount: Int) {
        value += amount
    }
    
    mutating func reset() {
        value = 0
    }
}

var counter = Counter()
counter.increment()
counter.increment(by: 5)
print(counter.getValue()) // 6
```

### Mutating Methods

When a struct method needs to modify properties, it must be marked as `mutating`

```swift
struct Point {
    var x: Double
    var y: Double
    
    mutating func moveBy(x deltaX: Double, y deltaY: Double) {
        x += deltaX
        y += deltaY
    }
    
    mutating func moveTo(x newX: Double, y newY: Double) {
        x = newX
        y = newY
    }
    
    // This method can replace self entirely
    mutating func moveToOrigin() {
        self = Point(x: 0.0, y: 0.0)
    }
}

var point = Point(x: 1.0, y: 1.0)
point.moveBy(x: 2.0, y: 3.0)
print("Point is now at (\(point.x), \(point.y))")
```

## Static Properties and Methods

Static members belong to the type itself, not to instances

```swift
struct MathUtilities {
    static let pi = 3.14159
    static var calculationCount = 0
    
    static func circleArea(radius: Double) -> Double {
        calculationCount += 1
        return pi * radius * radius
    }
    
    static func reset() {
        calculationCount = 0
    }
}

let area = MathUtilities.circleArea(radius: 5.0)
print("Area: \(area)")
print("Calculations performed: \(MathUtilities.calculationCount)")
```

## Initializers

### Memberwise Initializer

Swift automatically provides a memberwise initializer for structs

```swift
struct Song {
    var title: String
    var artist: String
    var duration: TimeInterval
    var genre: String = "Unknown"  // Default value
}

// Automatic memberwise initializer
let song1 = Song(title: "Imagine", artist: "John Lennon", duration: 183)
let song2 = Song(title: "Bohemian Rhapsody", 
                artist: "Queen", 
                duration: 355, 
                genre: "Rock")
```

### Custom Initializers

```swift
struct Color {
    var red: Double
    var green: Double
    var blue: Double
    var alpha: Double = 1.0
    
    // Custom initializer with RGB values (0-255)
    init(red: Int, green: Int, blue: Int) {
        self.red = Double(red) / 255.0
        self.green = Double(green) / 255.0
        self.blue = Double(blue) / 255.0
    }
    
    // Custom initializer with hex string
    init(hex: String) {
        let hex = hex.trimmingCharacters(in: CharacterSet.alphanumerics.inverted)
        var int = UInt64()
        Scanner(string: hex).scanHexInt64(&int)
        
        let a, r, g, b: UInt64
        switch hex.count {
        case 3: // RGB (12-bit)
            (a, r, g, b) = (255, (int >> 8) * 17, (int >> 4 & 0xF) * 17, (int & 0xF) * 17)
        case 6: // RGB (24-bit)
            (a, r, g, b) = (255, int >> 16, int >> 8 & 0xFF, int & 0xFF)
        default:
            (a, r, g, b) = (255, 0, 0, 0)
        }
        
        self.alpha = Double(a) / 255.0
        self.red = Double(r) / 255.0
        self.green = Double(g) / 255.0
        self.blue = Double(b) / 255.0
    }
    
    // Static factory methods
    static var black: Color {
        return Color(red: 0, green: 0, blue: 0)
    }
    
    static var white: Color {
        return Color(red: 255, green: 255, blue: 255)
    }
}

let color1 = Color(red: 255, green: 0, blue: 0)     // Red
let color2 = Color(hex: "FF0000")                   // Red from hex
let color3 = Color.black                            // Black
```

## Real-World Example: Task Management

```swift
struct Task {
    let id: UUID = UUID()
    var title: String
    var description: String
    var isCompleted: Bool = false
    var priority: Priority = .medium
    var dueDate: Date?
    
    private var createdAt: Date = Date()
    
    enum Priority: String, CaseIterable {
        case low = "Low"
        case medium = "Medium"
        case high = "High"
        case urgent = "Urgent"
    }
    
    var isOverdue: Bool {
        guard let dueDate = dueDate else { return false }
        return Date() > dueDate && !isCompleted
    }
    
    var daysSinceCreated: Int {
        Calendar.current.dateComponents([.day], from: createdAt, to: Date()).day ?? 0
    }
    
    mutating func toggleCompletion() {
        isCompleted.toggle()
    }
    
    mutating func updatePriority(to newPriority: Priority) {
        priority = newPriority
    }
    
    static func createUrgentTask(title: String, description: String, dueDate: Date) -> Task {
        return Task(title: title, 
                   description: description, 
                   priority: .urgent, 
                   dueDate: dueDate)
    }
}

// Usage
var task = Task(title: "Learn Swift Structs", 
               description: "Complete the structures tutorial")
task.updatePriority(to: .high)
task.toggleCompletion()

let urgentTask = Task.createUrgentTask(
    title: "Fix critical bug", 
    description: "App crashes on startup",
    dueDate: Calendar.current.date(byAdding: .day, value: 1, to: Date())!
)
```

---

## 🛫 Next Steps

#### What You've Learned
- ✅ Creating structures with various property types
- ✅ Implementing computed properties and property observers
- ✅ Using mutating methods to modify struct properties
- ✅ Working with static properties and methods
- ✅ Understanding memberwise and custom initializers

#### Where to Go Next
**Continue to** [Deep Dive to Classes](/Swift%20Fundamentals/Intermediate/02-Structures%20and%20Classes/03-Deep%20Dive%20to%20Classes.md)

---

## 📚 Resources 
- [Structures - The Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures#Structures)
- [Properties - The Swift Programming Language](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties)