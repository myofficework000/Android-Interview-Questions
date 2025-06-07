# Kotlin Flow – Interview Questions (2025)

## ✅ Beginner-Level Kotlin Flow Questions  
These test your foundational understanding.

- What is Kotlin Flow?  
- How is Flow different from LiveData?  
- How is Flow different from RxJava?  
- What is a cold stream in Flow?  
- How do you create a Flow?  
- What are the common Flow builders in Kotlin?  
- What is the `flow {}` builder used for?  
- What is the difference between `flowOf()` and `asFlow()`?  
- What is the `collect()` function in Kotlin Flow?  
- Can you collect a Flow multiple times?  
- How do you cancel a Flow collection?  
- What is the role of `suspend` in Kotlin Flow?  
- What is the default thread a Flow runs on?

## ✅ Intermediate-Level Kotlin Flow Questions  
These involve use cases, threading, error handling, and transformation.

- What is the `collectLatest()` function? How is it different from `collect()`?  
- What is the purpose of the `map`, `filter`, and `transform` operators in Flow?  
- How does `flowOn()` work? What does it affect?  
- What is the difference between `withContext` and `flowOn`?  
- What is the `catch` operator in Flow?  
- How do you handle exceptions in Kotlin Flow?  
- What is the difference between `onEach` and `collect`?  
- What is the purpose of `launchIn()` and `onEach()` combination?  
- How can you debounce a Flow?  
- How can you combine multiple flows? (e.g., `combine`, `zip`, `flatMapMerge`)  
- What is `flatMapConcat`, `flatMapMerge`, and `flatMapLatest`? When do you use each?  
- What is backpressure and how does Flow handle it?  
- What are `StateFlow` and `SharedFlow`?  
- Difference between `StateFlow`, `SharedFlow`, and `Flow`?  
- How do you convert `LiveData` to `Flow` and vice versa?  
- How do you make a Flow emit values every X seconds?

## ✅ Advanced-Level Kotlin Flow Questions  
These are for experienced candidates and test deep understanding, architecture, and performance.

- What is the difference between `StateFlow` and `LiveData`?  
- Why is `SharedFlow` hot and `Flow` cold?  
- When would you prefer `SharedFlow` over `StateFlow`?  
- What is replay in `SharedFlow`?  
- How do you use `shareIn()` and `stateIn()`?  
- Explain how to use Flow with MVVM and Repository pattern.  
- How to test a Kotlin Flow?  
- How can you collect from a Flow in a lifecycle-aware way?  
- How do you prevent memory leaks when using Flow in Android?  
- How do you implement pagination using Kotlin Flow?  
- How do you collect a Flow safely from a ViewModel in Compose or XML-based UI?  
- What is conflation in Flow? What does `conflate()` operator do?  
- How do you cache a Flow result and prevent recomputation?  
- What is the difference between cold flow, hot flow, and shared flow in real-life architecture?  
- What does `distinctUntilChanged()` do in Flow?  
- What are common performance pitfalls with Flow in Android?  
- How does Flow behave in structured concurrency? What happens when the parent coroutine is cancelled?  
- What are the advantages of Flow over RxJava or LiveData in modern Android development?  
- In a real-time chat app, how would you use Flow to manage incoming messages?  
- How do you combine Room and Retrofit using Kotlin Flow?  
- Can you explain the internals of Flow? How does it suspend, resume, and propagate?
