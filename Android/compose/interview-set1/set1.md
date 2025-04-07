# 🧩 Jetpack Compose

### 1. What is Jetpack Compose and how is it different from XML-based UI?
- modern, declarative UI toolkit
- introduced by google, part of android jetpack
- 100% in kotlin, no need xml layout resource file 
### 2. Why did Google introduce Jetpack Compose?
- better performance
- easy to customize UI dynamically
- higher code reusability 
### 3. What are Composables in Jetpack Compose?
- building block of compose
- defined hierarchically
- instruct system to create UI components
### 4. What are Modifiers and how do you use them?
- decorate and configure UI elements
- chain multiple modifier functions to apply multiple effects in sequence
- eg. height, width, padding, background, clickable 
### 5. How do Box, Row, and Column differ in Compose layouts?
- Box: simple, layering and alignment
- Row, Column: need both alignment and arrangement, can manage the scroll state
### 6. What is the use of Scaffold in Compose?
- automatic insets and innerPadding handling
- smart layout arrangement
- works well with TopAppBar, BottomNavigation, FAB and Drawer
### 7. How does Compose handle theming and Material Design?
- Material theme: apply consistent colors, typography and shapes across the app
- built-in support for Light and Dark Themes
- fully supports material and meterial3 components
- can adjust custom styling
### 8. How do you manage state in Jetpack Compose?
- state change, recomposition
- mutableStateOf
- remember, remembersavable
- external state, observeAsState(), collectAsState()
### 9. What is state hoisting in Compose and why is it important?
- moving the state variables to higher level composable and and pass it as para
- higher reusability of UI components
- more clear state management
- better separation of concern and testability 
### 10. What’s the difference between `remember` and `rememberSaveable`?
- remember: retain state across recomposition
- rememberSavable: also survive the configuation change
### 11. What is a SideEffect in Jetpack Compose? What types are available (`LaunchedEffect`, `DisposableEffect`, etc.)?
- trigger external oprations
- LaunchedEffect: launch a coroutine tied to current composable's lifecycle
- rememberCoroutineScope: run some suspend function in composable
- DisposableEffect: do some clean up in onDispose{} 
### 12. Does Jetpack Compose have a lifecycle?
- implicit: composition -> recomposition -> dispose
### 13. How do you create a custom Composable?
- pass the modifier or some other specific style argument and lambda as para to a reusable composable
### 14. How do you use `LazyColumn` in Compose and how does it differ from `RecyclerView`?
- easier syntax, no need adapter and viewholder
- better state management, and recomposition, no need notifyDataSetChanged()
- can use key attribute in lazyitems to recompose only affected items rather than whole list
- no layoutmanager, need to use different composables to achieve grid and staggered
### 15. How can you add headers or footers in a `LazyColumn`?
- item() before or after the items()
### 16. How does Compose handle navigation?
- navigation graph
- navhost
- navcontroller
- existing UI components like: top bar, bottom navigation bar, drawer, etc.
### 17. What is `ComposeView` and `AndroidView` in Compose?
- use AndroidView to embed xml layout resourcefile into a composable function
- use ComposeView to embed an exsiting composable into xml as a tag

🧩 Write syntax examples for:
BottomSheet
Top Tabs
DropdownMenu
Bottom Navigation Bar
Swipe to Delete

🧩 MVVM, MVI & Clean Architecture
What is MVVM? How is it implemented in Android?
What are the key responsibilities of ViewModel in MVVM?
How does Jetpack Compose work with ViewModel?
What is MVI architecture? How is it different from MVVM?
What is Unidirectional Data Flow (UDF) and how does MVI enforce it?
Can you explain Clean Architecture and its layers?
How do repositories fit in Clean Architecture?
How do you separate concerns in a Compose + MVVM + Clean Architecture project?

🧩 Kotlin Flows & Async Programming
What is Kotlin Flow and how is it different from LiveData?
How do you collect a Flow in Jetpack Compose?
What are StateFlow and SharedFlow? When do you use them?
How do you handle errors in Kotlin Flow?
What are the different operators in Kotlin Flow (map, flatMapConcat, etc.)?
What are some ways to perform asynchronous programming in Android?
What is collectAsState() used for in Compose?

🧩 Kotlin Core & Best Practices
What are Kotlin scope functions: let, run, with, apply, also?
Explain with and let functions with examples.
What are the advantages of Kotlin over Java?
How do you write clean, testable, and maintainable code in Android?
How do you handle side effects in a clean architecture?
