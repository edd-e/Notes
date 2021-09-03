# Swift<!-- omit in toc -->

Swift programming language.

## Table of contents<!-- omit in toc -->

- [Basics](#basics)
- [Variables and constants](#variables-and-constants)
- [Numeric types](#numeric-types)
- [Strings](#strings)
- [Comments](#comments)
- [Functions](#functions)
- [Structs and classes](#structs-and-classes)
- [Enumerations](#enumerations)
- [Stored and computed properties](#stored-and-computed-properties)
- [Property observers](#property-observers)
- [Loops](#loops)
- [Control flow](#control-flow)
- [Ternary operator](#ternary-operator)
- [Optionals](#optionals)
- [Closures](#closures)

## Basics

Hello world example;

File: `helloWorld.swift`

Code:

```swift
print("Hello world!")
```

## Variables and constants

Define variables using the `var` keyword:

```swift
var apples = 5
var today = "Friday"
```

Define constants using the `let` keyword:

```swift
let secondsPerMinute = 60, hoursPerDay = 24
```

Swift uses type inference to assign the data type. With type annotation you can specify a data type:

```swift
var highScore: Int = 125
var multiplier: Double = 2.5
var firstName, lastName: String
```

Large numbers can be formatted with underscores to improve readability, examples with and without underscores:

```swift
let largeNumber = 12_500_000
```

## Numeric types

This table contains some of the most common numeric data types:

| Type             | Alias                                      |
| ---------------- | ------------------------------------------ |
| Integer          | `Int` (Also: `Int8`, `Int32`, `Int64`)     |
| Unsigned Integer | `UInt` (Also: `UInt8`, `UInt32`, `UInt64`) |
| Float            | `Float`                                    |
| Double           | `Double`                                   |
| Boolean          | `Bool`                                     |
| String           | `String`                                   |

## Strings

Strings can be assigned to variables or constants.

```swift
var myWord = "Hello"
```

Multi line strings can be declared using three double quotation marks:

```swift
let toDoList = """
Don’t forget to:
- Walk the dog
- Buy groceries
- Do the laundry
"""
```

With `string interpolation` values can be inserted into string literals using `\(value)`:

```swift
var day = "Friday"
var onlineSales = 550
var phoneSales = 200

print("Today is \(day), the sales total is \(onlineSales + phoneSales)!")
```

Output:

```text
Today is Friday, the sales total is 750!
```

## Comments

Comments in Swift are similar to other languages:

```swift
// Example of a single-line comment

/* Example of a
 multi-line comment. */
```

Documentation can be written above classes, structs, properties, and methods. It appears in Xcode popovers.

```swift
/// The players must be nonzero
var players = 2
```

## Functions

Define functions with the `func` keyword.

```swift
func greet(person: String) {
    print("Hello /(person)")
}
```

Parameter names can be omitted with `_` or they can have an external label and an internal name. Return types are specified with `->`:

```swift
func add(_ x: Int, to y: Int) -> Int {
    return x + y
}

print(add(4, to: 6))
```

Functions with a single expression return that expression.

```swift
func multiply(x: Int, y: Int) -> Int {
    x * y
}
```

## Structs and classes

Structs and classes are similar to each other but have a few key differences.

| Struct                                                                                                  | Class                                                                 |
| ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| Value type.                                                                                             | Reference type.                                                       |
| Immutable; a struct is passed by copy, but also supports "copy on write" (mark with `mutable` keyword). | Mutable; classes are passed by reference (pointers).                  |
| Default initializer provided for all vars and properties without a default value.                       | Initializer must be specified for properties without a default value. |
| No inheritance.                                                                                         | Inheritance (single).                                                 |

Struct code sample:

```swift
struct MyStruct {
    let x: Int
    let y: Int
    var z: Int

    func total() {
        print(x + y + z)
    }

    mutating func incrementZ() {
        z += 1
    }
}

var demo1 = MyStruct(x: 5, y: 5, z: 1)
demo1.total() // 11
demo1.incrementZ()
demo1.total() // 12

struct RepeatThrice {
    var word: String

    init(word: String) {
        self.word = word
    }

    func repeatWord() {
        print(word, word, word)
    }
}

let demo2 = RepeatThrice(word: "go")
demo2.repeatWord() // go go go
```

Class code sample:

```swift
class MyClass {
    var propertyA: Int
    let propertyB: String

    init(propertyA: Int, propertyB: String) {
        self.propertyA = propertyA
        self.propertyB = propertyB
    }

    func myFunc(x: Int) -> Int {
        return x + 100
    }

    func modifyProperty() {
        propertyA += 1
    }
}

class SubClass: MyClass {
    var propertyC: Int = 0
}
```

## Enumerations

Enumerations can help group related values:

```swift
enum CoinToss {
    case heads
    case tails
}
```

The values themselves can also have associated values:

```swift
enum Radio {
    case am(Int)
    case fm(Float)
    case off
}

let myRadio = Radio.fm(88.1)

switch myRadio {
case let .am(station):
    print("The radio is tuned in to \(station) am")
case let .fm(station):
    print("The radio is tuned in to \(station) fm")
case .off:
    print("The radio is off")
}
```

## Stored and computed properties

Stored properties are provided by the class or structure.

```swift
struct Coordinate {
    let latitude, longitude: Double
}
```

Computed properties are provided by the class, structure, or enumeration and they are accessed by `get` and/or set with `set`.

```swift
struct Rectangle {
    let length, width: Int
    var area: Int {
        get {
            return length * width
        }
    }
}

struct Circle {
    var radius: Double
    var area: Double {
        get {
            return .pi * radius * radius
        }
        set {
            radius = (newValue / .pi).squareRoot()
        }
    }
}
```

## Property observers

Property observers are called when the value will be or has been set.

```swift
var myProperty = 0 {

    willSet {
        print("The value will be set to \(newValue)")
        print("The current value is \(myProperty)")
    }

    didSet {
        print("The value has been set to \(myProperty)")
        print("The value was \(oldValue)")
    }

}

```

## Loops

For loop example:

```swift
for letter in "ABC" {
    print(letter)
}
```

While loop example:

```swift
var x = 0

while x < 3 {
    print(x)
    x += 1
}
```

## Control flow

If/else statement example:

```swift
if conditionA {
    // ...
} else if conditionB || conditionC {
    // ...
} else if conditionD && conditionE {
    // ...
} else {
    // ...
}
```

Switch statement example:

```swift
var strikeNumber = 3

switch strikeNumber {
case 1:
    print("Strike one!")
case 2:
    print("Strike two!")
default:
    print("Strikeout!")
}
```

## Ternary operator

Example:

```swift
let largest = x > y ? x : y
```

## Optionals

An Optional holds either a value of the specified type or nil. In Swift, `nil` is the absence of a value. Optionals are denoted with `?` next to the data type. An optional without a default value is nil by default.

```swift
struct GuestInformation {
    let firstName, lastName: String
    let creditCardNumber: Int?
    let emailAddress: String?
}
```

If an optional contains a value, you can use force unwrapping to access the value with `!` at the end of the name. Note: Force unwrapping a nil value will result in a runtime error. Check an optional against nil before force unwrapping.

```swift
var sampleOptional: Int?

if sampleOptional == nil {
    print("sampleOptional is nil")
}

sampleOptional = 1

if sampleOptional =! nil {
    // force unwrap safe
    print(sampleOptional!)
}
```

With optional binding you can temporarily assign a value to a variable.

```swift
if let safeValue = sampleOptional {
    print(safeValue)
}
```

Use the nil-coalescing operator to unwrap a value or, if it is nil, provide a default value.

```swift
let safeValue = sampleOptional ?? 0
```

## Closures

Closures are reference types.

Closure syntax:

{ (`parameters`) -> `return type` in `statements` }

Example:

```swift
let product = { (x: Int, y: Int) -> Int in
    return x * y
}

let greeting = { (name: String) in
    print("Hello \(name)")
}
```

Parameter and return types can be implicitly inferred. If there is only one statement, you can omit the `return` keyword.

Closure syntax:

{ `parameters` in `statements` }

Example:

```swift
let product: (Int, Int) -> Int = { x, y in x * y }

let greeting: (String) -> Void = { name in print("Hello \(name)") }
```

Shorthand parameter names are provided to refer to the values of the arguments by the names of `$0`, `$1`, `$2`, and so on. By using these names in the closure expression, you can omit the argument list from the definition and define the closure as a single expression.

Closure syntax:

{ `statements` }

Example:

```swift
let product: (Int, Int) -> Int = { $0 * $1 }

let greeting: (String) -> Void = { print("Hello \($0)") }
```

A `trailing closure` is the final parameter to a function's arguments.

```swift
var numbers = [0, 1, 2]

// Not a trailing closure
numbers = numbers.map({
    $0 + 1
})

// Trailing closure
numbers = numbers.map() { $0 + 1 }
```

When the trailing closure is the only argument to the function, you can omit the function parentheses.

```swift
// Trailing closure shorthand
numbers = numbers.map { $0 + 1 }
```
