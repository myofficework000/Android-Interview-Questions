# Clean code

1. How do you ensure separation of concerns and maintainability in an MVVM-based Android app? Can you provide an example where improper separation caused issues?
Answer:
MVVM Structure: The View handles UI, the ViewModel manages state and business logic, and the Repository interacts with data sources.
Maintainability: Ensures modularity, making code testable and reusable.
Example of Improper Separation: If a ViewModel directly accesses a database instead of using a repository, it violates separation, making testing and refactoring difficult.
Fix: Introduce a Repository layer to decouple data handling from the ViewModel.

2. In a complex app with multiple ViewModels sharing business logic, how would you avoid code duplication while adhering to the Clean Code principles?
Answer:
Use a Base ViewModel: Extract common logic (e.g., error handling, loading states) into a BaseViewModel that other ViewModels extend.
Create a UseCase Layer: Implement UseCase classes to encapsulate business logic, ensuring reusability across multiple ViewModels.
Repository Abstraction: Provide shared repository methods to handle common data operations.
Example: Instead of duplicating API calls in multiple ViewModels, create a FetchDataUseCase that is injected wherever needed.

3. How do you handle long-running operations in an MVVM architecture without blocking the UI, and what are the potential pitfalls of incorrect coroutine scope usage?
Answer:
Use Coroutines & Flows: Run background tasks in viewModelScope.launch or LiveData with Flow to prevent UI blocking.
Pitfalls of Incorrect Scope Usage: Using GlobalScope may cause memory leaks, and launching coroutines in viewModelScope without handling lifecycle changes may lead to crashes.
Structured Concurrency: Use SupervisorJob and try-catch to handle failures gracefully.
Example: Fetching user data via Retrofit should be done using viewModelScope.launch { repository.getUserData() }.

4. Describe a scenario where the repository pattern introduced unnecessary complexity, and how would you refactor it to align with Clean Architecture?
Answer:
Problem: A repository that simply delegates API calls without adding value introduces redundancy.
Refactor Approach:
Remove the repository and inject the API service directly into UseCases if no local caching is needed.
If data transformation is needed, Refactor the repository to act as a single source of truth by managing local cache and remote data.
Example: If a repository just calls apiService.getData(), it can be replaced with a UseCase directly invoking the API.

5. Explain how to efficiently manage the ViewModel lifecycle in scenarios such as configuration changes, background tasks, and process death.
Answer:
Handling Configuration Changes: Use ViewModelProviders (in Activity) to retain ViewModel state across rotations.
Handling Background Tasks: Use WorkManager for persistent background tasks rather than Coroutines if the task should survive app termination.
Managing Process Death: Save state using SavedStateHandle in ViewModel to restore data when the process is recreated.
Example: When handling user authentication, store session data in SavedStateHandle and persist essential data in Room for long-term state retention.

6. What is Clean Architecture, and why is it used in Android?
Answer:
Definition: Clean Architecture is a software design pattern that separates concerns by organizing code into independent layers, improving maintainability and scalability.
Key Principle: It follows the Dependency Inversion Principle (DIP), ensuring inner layers don’t depend on outer layers.
Benefits: Increases testability, modularity, and separation of concerns, making the app easier to extend and modify.
Usage in Android: Helps manage UI, business logic, and data separately, avoiding tight coupling between components.

7. How do you structure an Android project using Clean Architecture?
Answer:
Divide into three primary layers: Presentation, Domain, and Data.
Follow the Dependency Rule: The inner layer (Domain) should not depend on external layers (Presentation, Data).
Use interfaces and dependency injection: To decouple business logic from framework dependencies.
Organize files properly: Keep each layer in separate packages for better modularization.

8. What are the different layers in Clean Architecture, and what belongs in each?
Answer:
Presentation Layer: Contains UI elements (Activities, Fragments, Jetpack Compose) and ViewModels that interact with Use Cases.
Domain Layer: Holds business logic with Use Cases (Interactors) and Entities (core models).
Data Layer: Manages data sources (APIs, databases, repositories) and provides data to the Domain layer.
Dependency Flow: Data → Domain → Presentation (UI never directly accesses Data).

9. How does Use Case (or Interactor) layer improve code maintainability?
Answer:
Encapsulates Business Logic: Ensures logic is independent of UI and data layers.
Reusability: Use Cases can be reused across multiple ViewModels or UI components.
Testability: Business logic can be unit-tested without UI or database dependencies.
Single Responsibility: Keeps UI and Data layers clean by separating logic into Use Cases.

10. How should ViewModel interact with Use Cases in Clean Architecture?
Answer:
Uses Dependency Injection: ViewModel calls Use Cases via constructor injection.
Asynchronous Execution: Use Cases return results via coroutines (suspend) or reactive streams (Flow).
State Management: ViewModel exposes UI state (LiveData or StateFlow) based on Use Case results.
Decoupling UI from Business Logic: ViewModel only handles UI logic, delegating business logic to Use Cases.

11. How do you pass data between layers while maintaining separation of concerns?
Answer:
Use Data Models: Convert data from APIs/DB into domain models before passing to Use Cases.
DTOs vs. Domain Models: Avoid exposing raw data models (like API responses) directly to the UI.
Repository Pattern: Acts as a bridge between Data and Domain layers to provide clean data handling.
Unidirectional Flow: Data flows in one direction (Data → Domain → Presentation), ensuring loose coupling.

12. What strategies do you use to handle business logic in Clean Architecture?
Answer:
Use Case Pattern: Encapsulate logic inside Use Cases instead of ViewModel or Repositories.
Error Handling & Validation: Centralize exception handling in Use Cases to keep UI layer clean.
State Management: Emit states (Loading, Success, Error) via Flow or LiveData.
Repository Abstraction: Keep Repositories responsible for data fetching, not for applying business logic.

13. How do you manage dependency injection in a clean architecture setup?
Answer:
Use Dagger-Hilt or Koin: Popular DI frameworks for injecting dependencies in Android.
Provide Dependencies per Layer: Inject Use Cases into ViewModels, and Repositories into Use Cases.
Follow Constructor Injection: Ensures dependencies are passed explicitly and tested easily.
Singletons & Scoped Instances: Use singletons for app-wide dependencies and scoped instances for lifecycle-specific components.

