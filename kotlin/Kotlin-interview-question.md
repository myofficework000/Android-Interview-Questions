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
println(name?.length)  // Prints null
