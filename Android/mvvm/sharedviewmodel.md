# SharedViewModel in Android – Interview Q&A

## Q1. What is a SharedViewModel, and in which scenarios is it typically used in Android development?

A **SharedViewModel** is a `ViewModel` scoped to an `Activity` and shared across its `Fragments`.

### Use Cases
- Share data between Fragments.
- Avoid interface-based communication or bundles.
- Maintain consistent state across Fragment transactions and configuration changes.

### Example
```kotlin
class SharedViewModel : ViewModel() {
    val selectedItem = MutableLiveData<String>()
}

// Fragment A
private val sharedViewModel: SharedViewModel by activityViewModels()
sharedViewModel.selectedItem.value = "Hello"

// Fragment B
private val sharedViewModel: SharedViewModel by activityViewModels()
sharedViewModel.selectedItem.observe(viewLifecycleOwner) {
    // Use the shared value
}
```

## Q2. How does activityViewModels() differ from viewModels() when retrieving a ViewModel in a Fragment?
| Function               | Scope    | Behavior                                                          |
| ---------------------- | -------- | ----------------------------------------------------------------- |
| `viewModels()`         | Fragment | Creates separate instance for each Fragment                       |
| `activityViewModels()` | Activity | Shares single ViewModel across all Fragments within that Activity |

```kotlin
private val viewModel1: MyViewModel by viewModels() // Fragment scoped
private val sharedViewModel: SharedViewModel by activityViewModels() // Activity scoped
```

### Q3. How do you share data between Fragments using a SharedViewModel scoped to the parent Activity?
Use activityViewModels() in both Fragments to observe and update shared data.

🧪 Example
```kotlin
// Fragment A
sharedViewModel.userName.value = "John"

// Fragment B
sharedViewModel.userName.observe(viewLifecycleOwner) {
    textView.text = it
}
```

### Q4. What are the lifecycle implications of using a SharedViewModel across multiple Fragments?
- Lives as long as the Activity is alive.
- Survives configuration changes.
- Destroyed only when the Activity is permanently finished (e.g. back press or finish()).

### Q5. How do you observe LiveData or StateFlow from a SharedViewModel in multiple Fragments?
🧪 LiveData Example

```kotlin
sharedViewModel.data.observe(viewLifecycleOwner) {
    // React to change
}
```
 StateFlow Example
 ```kotlin
 lifecycleScope.launchWhenStarted {
    sharedViewModel.dataFlow.collect {
        // React to new value
    }
}
```

### Q6. What is the best way to clear or reset SharedViewModel data when navigating between screens or on back press?
Create a method in ViewModel like clearData()

Call it from onDestroyView() or when needed

🧪 Example
 ```kotlin
fun clearData() {
    selectedItem.value = null
}

override fun onDestroyView() {
    super.onDestroyView()
    sharedViewModel.clearData()
}
```

### Q7. Can we have a SharedViewModel between two Activities? Why or why not?
No, ViewModels are scoped to a ViewModelStoreOwner (Activity or Fragment).
You cannot share a ViewModel instance across Activities directly.

✅ Alternatives
- Application-level ViewModel with a custom ViewModelStore
- Repository pattern
- Singleton
- SharedPreferences or local storage

### Q8. How does ViewModel lifecycle behave when scoped to an Activity in a single-activity architecture?
"The ViewModel remains in memory until the ViewModelStoreOwner to which it's scoped goes away permanently."
#### Explanation
- In a single-activity setup, ViewModel behaves like a singleton.
- It persists through all Fragment recreations.
- Data is maintained until the Activity is completely destroyed.

🧪 Example
 ```kotlin
// Always returns the same instance until the activity is finished
private val sharedViewModel: SharedViewModel by activityViewModels()
```


