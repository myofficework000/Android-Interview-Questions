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

## 8. What is @JvmOverloads?
Used to generate overloads for default parameter functions for Java interoperability.
```kotlin
@JvmOverloads
fun greet(name: String = "Guest", age: Int = 18) {
    println("Hello $name, age $age")
}
```

## 9. What is a Lambda Function?
Anonymous function used for functional programming.
```kotlin
val square = { x: Int -> x * x }
println(square(4)) // 16
```

## 10. How to Declare Lambda Function?
```kotlin
val sum: (Int, Int) -> Int = { a, b -> a + b }
```

## 11. What is a Higher-Order Function?
Takes functions as parameters or returns them.
```kotlin
fun calculate(a: Int, b: Int, op: (Int, Int) -> Int): Int {
    return op(a, b)
}

val result = calculate(4, 2) { x, y -> x * y }
```

## 12. What is an Inline Function?
Suggests compiler to inline the function's bytecode to avoid overhead.
```kotlin
inline fun runTimed(block: () -> Unit) {
    val start = System.currentTimeMillis()
    block()
    val end = System.currentTimeMillis()
    println("Time taken: ${end - start} ms")
}
```

## 13. What is an Infix Function?
Custom infix notation for better readability.

```kotlin
infix fun Int.times(str: String) = str.repeat(this)
val result = 2 times "Hi " // Hi Hi 
```

## 14. What is a tailrec Function?
Optimized recursive function that prevents stack overflow.
```kotlin
tailrec fun factorial(n: Int, acc: Int = 1): Int {
    return if (n == 0) acc else factorial(n - 1, acc * n)
}
```

## 15. What is Primary, Secondary Constructor and init Block?
```kotlin
class User(val name: String) {
    init {
        println("Init block called")
    }

    constructor(name: String, age: Int) : this(name) {
        println("Secondary constructor called")
    }
}
```
- Primary constructor: Part of class header.
- Secondary constructor: Uses constructor.
- init block: Executes after primary constructor.

## 16. What is the Relationship Between Primary and Secondary Constructors?
Secondary constructors must delegate to the primary one using this(...).

## 17. What is a Data Class?
Special class that automatically generates:
```kotlin
equals()
hashCode()
toString()
copy()
componentN()
data class User(val name: String, val age: Int)
```

## 18. What is a Sealed Class?
Used to represent restricted class hierarchies.

sealed class Result
data class Success(val data: String): Result()
data class Error(val error: String): Result()
Ideal with when expressions for exhaustive checks.

## 19. What is open, final, and abstract?
open: Allows inheritance/overriding
final: Prevents inheritance (default)
abstract: Must be overridden

## 20. What is a Companion Object?
Static-like members for a class.
```kotlin
class Logger {
    companion object {
        fun log(msg: String) = println(msg)
    }
}

Logger.log("Hello")
```

