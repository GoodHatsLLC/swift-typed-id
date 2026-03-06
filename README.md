# `swift-typed-id`

## *`“Make your IDs type-safe with this One Simple Trick.”`*

Turn interchangeable ID types like `UUID` or `String` into
types differentiated at compile time — like `UserID` and `DeviceID`.

## Usage

1. Adding the dependency to your target:

```swift
/// Package.swift, top-level
dependencies: [
    .package(url: "https://github.com/GoodHatsLLC/swift-typed-id.git", from: "1.1.0"),
],

/// Package.swift, in targets
.target(
    name: "MyTarget",
    dependencies: [
        .product(name: "TypedID", package: "swift-typed-id")
    ]
)
```

2. Using the library:

```swift
import TypedID

struct MyCustomID: TypedID {
  let raw: String
}
```

```swift
let myID = UserID("usr99999")
let otherID = UserID("usr11111")

// Equatabilty
let isSameUser = myID == otherID

// Hashability
let users = Set([myID, otherID])

// Codability
let encoded = try JSONEncoder().encode(myID)
let decoded = String(data: encoded, encoding: .utf8)
// The encoding is transparent. Serialized values remain the same.
assert(decoded == "usr99999")
```

`TypeID` works with common ID types, including `String`, `Int`, `UUID`, `UInt`, `Double`. 
Adding new types is simple. See `UUID` for an example.
