# Kotlin Interview Questions and Answers

## 1. Kotlin vs Java - Advantages of Kotlin over Java

| Feature               | Kotlin                                | Java                                   |
|----------------------|----------------------------------------|----------------------------------------|
| Null Safety          | Built-in null safety                   | NullPointerExceptions common           |
| Extension Functions  | Supported                              | Not supported                          |
| Type Inference       | Smart type inference                   | Verbose type declarations              |
| Coroutines           | Native support for async programming   | Requires external libraries            |
| Data Classes         | Single-line model classes              | Requires boilerplate code              |
| Interoperability     | 100% Java interoperable                | Not applicable                         |
| Smart Casts          | Automatically casts types              | Manual casting required                |

## 2. What is Null Safety and How is it Achieved in Kotlin?

Null safety helps avoid `NullPointerException`. Kotlin distinguishes between nullable (`String?`) and non-nullable (`String`) types.

### Safe Calls

```kotlin
val name: String? = null

// Safe call
println(name?.length)

// Elvis operator
val length = name?.length ?: 0

// Not-null assertion (throws if null)
val forceLength = name!!.length
```

## 3. Difference Between Safe Call (?.) and Null Check (!!)
| Operator | Description                    | Example          |
| -------- | ------------------------------ | ---------------- |
| `?.`     | Returns null if object is null | `obj?.property`  |
| `!!`     | Throws NPE if object is null   | `obj!!.property` |

## 4. val vs var vs const val
val name = "John"         // Immutable at runtime
var age = 30              // Mutable
const val PI = 3.14       // Immutable and compile-time constant

val: Runtime constant
var: Mutable
const val: Compile-time constant (top-level or in object)


## 5. What is an Extension Function?
Adds functionality to existing classes without inheritance.
```kotlin
fun String.reverse(): String {
    return this.reversed()
}

val result = "hello".reverse() // olleh
```
## 6. Can Extension Functions Access Private Properties?
❌ No, extension functions cannot access private or protected members.

## 7. How to Use Extension Function from Java?
Extension functions are compiled as static functions:
```kotlin
fun String.hello() = "Hello $this"
```

