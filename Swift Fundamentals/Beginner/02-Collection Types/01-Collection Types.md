# Collection Types

## 🎯 Learning Objectives
By the end of this lesson you will:
- Understand the three main collection types in Swift: **Arrays**, **Sets**, and **Dictionaries**
- Learn the difference between **mutable** and **immutable** collections using var and let
- Master **Array** operations including creation, modification, iteration, and subscript access
- Work with **Sets** for storing unique values and performing set operations like union and intersection
- Understand **hash values** and the requirements for storing custom types in Sets
- Implement **Dictionary** operations for key-value storage and retrieval
- Choose the appropriate collection type based on your data requirements and use cases
- Apply collection iteration techniques using **for-in** loops and enumeration methods

--- 

##  Mutability of Collections
If you create an array, a set, or a dictionary, and assign it to a variable, the collection that’s created will be mutable. This means that you can change (or mutate) the collection after it’s created by adding, removing, or changing items in the collection. If you assign an array, a set, or a dictionary to a constant, that collection is immutable, and its size and contents can’t be changed.

> Note
> It's good practice to create immutable collections in all cases where the collection doesn't need to change. Doing so makes it easier for you to reason about your code and enables the Swift compiler to optimize the performance of the collections you create.

---

## Arrays
An array stores values of the **same** type in an **ordered** list. The same value can appear in an array multiple times at different positions.

```swift
let fruits = ["Apple", "Orange", "Banana", "Apple"]
```

### Creating an Array
You can create an empty array using two approaches: array literal or by using explicit initializer syntax.

#### Array literal
It is written as [ ] (an empty pair of square brackets)

```swift
var someInts: [Int] = []
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```
#### Explicit initializer syntax
You can create an empty array by writing the element type in square brackets followed by parentheses:

```swift
var someInts = [Int]()
print("someInts is of type [Int] with \(someInts.count) items.")
// Prints "someInts is of type [Int] with 0 items."
```

### Accessing and Modifying an Array
You can access and modify an array through its methods and properties, or by using subscript syntax.

#### `count` property
You can find out the number of items in an array checking its read-only `count` property:

```swift
var shoppingList = ["Eggs", "Milk"]
print("The shopping list contains \(shoppingList.count) items.")
// Prints "The shopping list contains 2 items."
```

#### Add new item to the end of the array
You can add a new item to the end of the array by using the `append(_:)` method:

```swift
shoppingList.append("Flour")
// shoppingList now contains 3 items
```
Alternatively, you can append an array of one or more compatible items with the addition assignment operator (+=):

```swift
shoppingList += ["Baking Powder"]
// shoppingList now contains 4 items

shoppingList += ["Chocolate", "Cheese", "Butter"]
// shoppingList now contains 7 items
```
#### Retrieving items
You can retrieve a value from the array by using *subscript syntax*, passing the index of the value you want to retrieve within square brackets immediately after the name of the array:

```swift
var firstItem = shoppingList[0]
// firstItem is equal to Eggs
```
> Note
> The first item in the array has an index of 0, not 1. Arrays in Swift are always zero-indexed.

#### Modifying an item
You can use subscript syntax to change an existing value at a given index:

```swift
shoppingList[0] = "Six eggs"
// The first item in the list is now equal to "Six eggs" rather than "Eggs"
```

You can also use subscript syntax to change a range of values at once, even if the replacement set of values has a different length than the range you are replacing. The following example replaces "Chocolate", "Cheese", and "Butter" with "Bananas" and "Apples":

```swift
shoppingList[4...6] = ["Bananas", "Apples"]
// shoppingList now contains 6 items
```

#### Inserting an item at a specified index
You can insert an item at a specified index by using the `insert(_:at:)` method.

```swift
shoppingList.insert("Maple Syrup", at: 0)
// shoppingList now contains 7 items
// "Maple Syrup" is now the first item in the list
```

### Iterating Over an Array
You can iterate over the entire set of values in an array with the `for-in` loop:

```swift
for item in shoppingList {
    print(item)
}
// Maple Syrup
// Six Eggs
// Milk
// Flour
// Baking Powder
// Bananas
// Apples
```

If you need the integer index of each item as well as its value, use the `enumerated()` method to iterate over the array instead. For each item in the array, the `enumerated()` method returns a tuple composed of an integer and the item. The integers start at zero and count up by one for each item.

```swift
for (index, value) in shoppingList.enumerated() {
    print("Item \(index + 1): \(value))
}

// Item 1: Maple Syrup
// Item 2: Six Eggs
// Item 3: Milk
// Item 4: Flour
// Item 5: Baking Powder
// Item 6: Bananas
// Item 7: Apples
```
---

## Sets
A set stores **distinct values** of the **same type** in a collection with **no defined ordering**. You can use a set instead of an array when the **order** of items is not important, or when you need to ensure that an item only appears **once**.

### Hash Values for Set Types
A type must be *hashable* in order to be stored in a set - that is, the type must provide a way to compute a *hash value* for itself. A hash value is an Int value that's the same for all objects that compare equally, such that if a == b, the hash value of a is equal to the has value of b.

All of Swift's basic types (such as String, Int, Double, and Bool) are hashable by default, and can be used as set value types or dictionary key types.

> Note
> You can use your own custom types as set value types or dictionary key types by making them conform to the `Hashable` protocol from the Swift standard library. For information about implementing the required `hash(into:)` method, see [Hashable](https://developer.apple.com/documentation/swift/hashable).

### Creating and Initializing an Empty Set
You can create an empty set of a certain type using initializer syntax:

```swift
var letters = Set<Character>()
print("letters is of type Set<Character> with \(letters.count) items.")
// Prints "letters is of type Set<Character> with 0 items.
```

### Creating a Set with an Array Literal
You can also initialize a set with an array literal, as a shorthand way to write one or more values as a set collection:

```swift
var favoriteGenres: Set<String> = ["Rock", "Classical",  "Hip-Hop"]
// favoriteGenres has bee initialized with three initial items
```
### Accessing and Modifying a Set
You access and modify a set through its methods and properties

#### Number of items in a set
To find out the number of items in a set, check its read-only `count` property

```swift
print("I have \(favoriteGenres.count) favorite music genres")
// Prints "I have 3 favorite music genres
```

#### Check whether the `count` property is equal to 0
Use the Boolean `isEmpty` property as a shortcut for checking whether the `count` property is equal to 0:

```swift
if favoriteGenres.isEmpty {
    print("As far as music goes, I'm not picky")
} else {
    print("I have particular music preferences")
}
// Prints "I have particular music preferences"
```

#### Inserting items
You can add a new item into a set by calling the set's `insert(_:)` method:
```swift
favoriteGenres.insert("Jazz")
// favoriteGenres now contains 4 items
```

#### Removing items
You can remove an item from a set by calling the set's `remove(_:)` method, which removes the item if it's a member of the set, and returns the removed value, or returns `nil` if the set didn't contain it. Alternatively, all items in a set can be removed with its `removeAll()` method.

```swift
if let removedGenre = favoriteGenres.remove("Rock") {
    print("\(removedGenre)? I'm over it")
} else {
    print("I never much cared for that")
}
// Prints "Rock? I'm over it"
```

#### Check if a set contains a particular item
Use the `contains(_:)` method:
```swift
if favoriteGenres.contains("Funk") {
    print("I get up on the good foot")
} else {
    print("It's too funky in here")
}
// Prints "It's too funky in here"
```

### Iterating Over a Set
You can iterate over the values in a set with a `for-in` loop

```swift
for genre in favoriteGenres {
    print("\(genre)")
}
// Classical
// Jazz
// Hip Hop
```

Swift's `Set` type doesn't have a defined ordering. To iterate over the values of a set in a specific order, user the `sorted()` method, which returns the set's elements as an array sorted using the < operator.

```swift
for genre in favoriteGenres.sorted() {
    print("\(genre))
}
// Classical
// Hip Hop
// Jazz
```
### Performing Set Operations
You can efficiently perform fundamental set operations, such as combining two sets together, determining which values two sets have in common, or determining whether two sets contain all, some, or none of the same values.


#### Fundamental Set Operations
The illustration below depicts two sets — a and b — with the results of various set operations represented by the shaded regions.

![Set Operations](/Swift%20Fundamentals/02-Collection%20Types/assets/setVennDiagram@2x.png)

- Use the `intersection(_:)` method to create a new set with only the values common to both sets
- Use the `symmetricDifference(_:)` method to create a new set with values in either set, but not both
- Use the `union(_:)` method to create a new set with all of the values in both sets
- Use the `subtracting(_:)` method to create a new set with values not in the specified set

```swift
let oddDigits: Set = [1, 3, 5, 7, 9]
let evenDigits: Set = [0, 2, 4, 6, 8]
let singleDigitPrimeNumbers: Set = [2, 3, 5, 7]


oddDigits.union(evenDigits).sorted()
// [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
oddDigits.intersection(evenDigits).sorted()
// []
oddDigits.subtracting(singleDigitPrimeNumbers).sorted()
// [1, 9]
oddDigits.symmetricDifference(singleDigitPrimeNumbers).sorted()
// [1, 2, 9]

```

#### Set Membership and Equality
The illustration below depicts three sets — a, b and c — with overlapping regions representing elements shared among sets. Set a is a superset of set b, because a contains all elements in b. Conversely, set b is a subset of set a, because all elements in b are also contained by a. Set b and set c are disjoint with one another, because they share no elements in common.

![MembershipAndEquality](/Swift%20Fundamentals/02-Collection%20Types/assets/setEulerDiagram@2x.png)

- Use the “is equal” operator (==) to determine whether two sets contain all of the same values.

- Use the `isSubset(of:)` method to determine whether all of the values of a set are contained in the specified set.

- Use the `isSuperset(of:)` method to determine whether a set contains all of the values in a specified set.

- Use the `isStrictSubset(of:)` or isStrictSuperset(of:) methods to determine whether a set is a subset or superset, but not equal to, a specified set.

- Use the `isDisjoint(with:)` method to determine whether two sets have no values in common.

```swift
let houseAnimals: Set = ["🐶", "🐱"]
let farmAnimals: Set = ["🐮", "🐔", "🐑", "🐶", "🐱"]
let cityAnimals: Set = ["🐦", "🐭"]

houseAnimals.isSubset(of: farmAnimals)
// true
farmAnimals.isSuperset(of: houseAnimals)
// true
farmAnimals.isDisjoint(with: cityAnimals)
// true
```
---

## Dictionaries
A *dictionary* stores associations between keys of the same type and values of the same type in a collection with no defined ordering. Each value is associated with a unique *key*, which acts as an identifier for that value within the dictionary. Unlike items in an array, items in a dictionary don’t have a specified order. You use a dictionary when you need to look up values based on their identifier, in much the same way that a real-world dictionary is used to look up the definition for a particular word.
### Creating an Empty Dictionary
#### By using initializer syntax
```swift
var namesOfIntegers: [Int: String] = [:]
// namesOfIntegers is an empty [Int: String] dictionary
```

#### By using an empty dictionary literal
```swift
namesOfIntegers[16] = "sixteen"
// namesOfIntegers now contains 1 key-value pair
namesOfIntegers = [:]
// namesOfIntegers is once again an empty dictionary of type [Int: String]
```

### Creating a Dictionary with a Dictionary Literal
You can also initialize a dictionary with a dictionary literal, which has a similar syntax to the array literal seen earlier. A dictionary literal is a shorthand way to write one or more key-value pairs as a Dictionary collection.

A key-value pair is a combination of a key and a value.
The example below creates a dictionary to store the names of international airports. In this dictionary, the keys are three-letter International Air Transport Association codes, and the values are airport names:

```swift
var airports: [String: String] = ["YYZ": "Toronto Pearson", "DUB": "Dublin"]
```
### Accessing and Modifying a Dictionary
You access and modify a dictionary through its methods and properties, or by using subscript syntax.

#### Count items
As with an array, you find out the number of items in a Dictionary by checking its read-only count property:

```swift
print("The airports dictionary contains \(airports.count) items.")
// Prints "The airports dictionary contains 2 items."
```

#### Check if items count are equal to 0
Use the Boolean isEmpty property as a shortcut for checking whether the count property is equal to 0:

```
if airports.isEmpty {
    print("The airports dictionary is empty.")
} else {
    print("The airports dictionary isn't empty.")
}
// Prints "The airports dictionary isn't empty."
```

#### Add a new item to a Dictionary
You can add a new item to a dictionary with subscript syntax:
```swift
airports["LHR"] = "London"
// the airports dictionary now contains 3 items
```
#### Update a value for a particular key
You can also use subscript syntax to change the value associated with a particular key:

```swift
airports["LHR"] = "London Heathrow"
// the value for "LHR" has been changed to "London Heathrow"
```

As an alternative to subscription, use a dictionary's `updateValue(_:forKey:)` method to set or update the value for a particular key. It sets a value for a key if none exists, or updates the value if that key already exists. Unlike a subscript, however, the `updateValue(_:forKey:)` method returns the *old* value after performing an update. This enables you to check whether or not an update took place.

The `update(_:forKey:)` method returns an optional value of the dictionary's value type.

```
if let oldValue = airports.updateValue("Dublin Airport", forKey: "DUB") {
    print("The old value for DUB was \(oldValue).")
}
// Prints "The old value for DUB was Dublin."
```

#### Remove a key-value pair
You can use subscript syntax to remove a key-value pair from a dictionary by assigning a value of nil for that key:
```
airports["APL"] = "Apple International"
// "Apple International" isn't the real airport for APL, so delete it
airports["APL"] = nil
// APL has now been removed from the dictionary
```

Alternatively, remove a key-value pair form a dictionary with the `removeValue(forKey:)` method. This method removes the key-value pair if it exists and returns the removed value, or returns `nil` if no value existed:

```swift
if let removedValue = airports.removeValue(forKey: "DUB") {
    print("The removed airport's name is \(removedValue).")
} else {
    print("The airports dictionary doesn't contain a value for DUB.")
}
// Prints "The removed airport's name is Dublin Airport."
```

### Iterating Over a Dictionary
You can iterate over the key-value pairs in a dictionary with a for-in loop. Each item in the dictionary is returned as a (key, value) tuple, and you can decompose the tuple’s members into temporary constants or variables as part of the iteration:
```swift
for (airportCode, airportName) in airports {
    print("\(airportCode): \(airportName)")
}
// LHR: London Heathrow
// YYZ: Toronto Pearson
```


You can also retrieve an iterable collection of a dictionary’s keys or values by accessing its keys and values properties:

```swift
for airportCode in airports.keys {
    print("Airport code: \(airportCode)")
}
// Airport code: LHR
// Airport code: YYZ


for airportName in airports.values {
    print("Airport name: \(airportName)")
}
// Airport name: London Heathrow
// Airport name: Toronto Pearson
```
---

## 🛫 Next Steps

#### What You've Learned
- ✅ **Collection Mutability**: Understanding the difference between mutable (var) and immutable (let) collections and when to use each
- ✅ **Arrays**: Creating, accessing, modifying, and iterating over ordered collections of the same type
- ✅ **Array Operations**: Using methods like append(), insert(), subscript syntax, and enumerated() for comprehensive array manipulation
- ✅ **Sets**: Working with unordered collections of unique values and understanding hash requirements
- ✅ **Set Operations**: Performing union, intersection, symmetric difference, and subset/superset operations
- ✅ **Dictionaries**: Creating and managing key-value pairs for efficient data lookup and storage
- ✅ **Dictionary Methods**: Using updateValue(), removeValue(), and subscript syntax for dictionary manipulation
- ✅ **Collection Iteration**: Mastering for-in loops and specialized iteration methods for all collection types


#### Where to Go Next

**Continue to** [Control Flow - Conditionals](/Swift%20Fundamentals/Beginner/03-Control%20Flow/01-Conditionals.md)


---

## 📚 Resources
- [The Swift Programming Language - Collection Types](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/collectiontypes#app-top)
- [Array | Apple Developer Documentation](https://developer.apple.com/documentation/swift/array)
- [Set | Apple Developer Documentation](https://developer.apple.com/documentation/swift/set)
- [Dictionary | Apple Developer Documentation](https://developer.apple.com/documentation/swift/dictionary)
- [Hashable | Apple Developer Documentation](https://developer.apple.com/documentation/swift/hashable)