# **Composition in Jetpack Compose**  

## **What is Composition in Jetpack Compose?**  
Composition in Jetpack Compose refers to the process of building a UI by combining smaller UI elements (Composables) together. It allows us to create reusable and modular UI components efficiently.  

## **Why Use Composition in Jetpack Compose?**  
- **Declarative UI:** Compose follows a declarative UI approach, making it easier to design and update UI components.  
- **Reusable Components:** UI elements can be reused and composed together, reducing redundant code.  
- **Efficient Rendering:** Compose only updates the parts of the UI that change, improving performance.  
- **Modular Design:** Helps in structuring UI in a clean and maintainable way.  

---

## **How Does Composition Work?**  
In Jetpack Compose, UI elements are built using **Composables**—functions annotated with `@Composable`.  

1. **You define a small Composable function**  
2. **You call these functions inside other Composable functions to build complex UIs**  
3. **The UI updates automatically when data changes**  

---

## **Prebuilt Classes, Functions, and Interfaces in Jetpack Compose (Composition Related)**  

### **1. `@Composable` Annotation**  
- **What?**: Marks a function as a composable function, meaning it can be used to define UI.  
- **Usage:**  
  ```kotlin
  @Composable
  fun Greeting(name: String) {
      Text(text = "Hello, $name!")
  }
  ```

---

### **2. Composition Functions in Jetpack Compose**  

| Function | Description | Example |
|----------|------------|---------|
| `remember` | Used to retain state during recomposition | `val count = remember { mutableStateOf(0) }` |
| `rememberSaveable` | Persists state even after configuration changes (e.g., screen rotation) | `val text = rememberSaveable { mutableStateOf("") }` |
| `mutableStateOf` | Creates a state variable that triggers UI updates when changed | `val isChecked = mutableStateOf(false)` |
| `LaunchedEffect` | Runs a side-effect only when dependencies change | `LaunchedEffect(key1) { /* Effect Code */ }` |
| `SideEffect` | Runs after every recomposition (used in debugging) | `SideEffect { println("Recomposition happened!") }` |
| `DisposableEffect` | Cleans up resources when the Composable leaves the composition | `DisposableEffect(Unit) { onDispose { /* Cleanup */ } }` |

---

### **3. Composition Scopes & Lifecycle**  
- **Composition**: The initial creation of UI from composables.  
- **Recomposition**: When UI is updated in response to state changes.  
- **Decomposition**: When a composable is removed from the UI.  

**Real-Life Example:**  
Imagine a **music player app** where the play button changes its icon dynamically when clicked.  

```kotlin
@Composable
fun PlayPauseButton() {
    var isPlaying by remember { mutableStateOf(false) }

    IconButton(onClick = { isPlaying = !isPlaying }) {
        Icon(
            imageVector = if (isPlaying) Icons.Default.Pause else Icons.Default.PlayArrow,
            contentDescription = "Play/Pause"
        )
    }
}
```
**How it works:**  
- The `remember { mutableStateOf(false) }` keeps track of whether the button is in the playing state.  
- When clicked, the UI **recomposes**, updating the icon dynamically.  

---

### **4. Composition Types in Jetpack Compose**  

#### **1. Stateful Composables**  
- A Composable that **holds and manages its own state**.  
- Example:  
  ```kotlin
  @Composable
  fun Counter() {
      var count by remember { mutableStateOf(0) }

      Column {
          Text(text = "Count: $count")
          Button(onClick = { count++ }) {
              Text("Increase Count")
          }
      }
  }
  ```
- **Why?**: It simplifies logic when managing internal state within a single UI component.  

---

#### **2. Stateless Composables**  
- A Composable that **does not manage its own state** but instead receives state as parameters.  
- Example:  
  ```kotlin
  @Composable
  fun Counter(count: Int, onIncrement: () -> Unit) {
      Column {
          Text(text = "Count: $count")
          Button(onClick = onIncrement) {
              Text("Increase Count")
          }
      }
  }
  ```
- **Why?**: It promotes reusability and better separation of concerns.  

---

### **5. Composition in Lazy Composables**  
Jetpack Compose provides `LazyColumn` and `LazyRow` for handling lists efficiently.  

```kotlin
@Composable
fun NamesList(names: List<String>) {
    LazyColumn {
        items(names) { name ->
            Text(text = name)
        }
    }
}
```
- **Why?**: Unlike `Column`, `LazyColumn` only renders visible items, improving performance.  

---

### **6. Effects in Composition**  
Jetpack Compose provides different effect handlers to manage side-effects in UI.  

| Effect | Description | Example |
|--------|------------|---------|
| `LaunchedEffect` | Runs suspending functions in Composable | `LaunchedEffect(Unit) { delay(1000) }` |
| `SideEffect` | Executes after every recomposition | `SideEffect { println("UI updated!") }` |
| `DisposableEffect` | Cleans up when the Composable leaves the UI | `DisposableEffect(Unit) { onDispose { /* Cleanup */ } }` |
| `ProduceState` | Produces a state from a coroutine | `val data = produceState(0) { value = fetchData() }` |

---

### **7. Composition vs View System (XML-based UI)**  

| Feature | Jetpack Compose (Composition) | XML-Based Views |
|---------|------------------------------|-----------------|
| UI Definition | Kotlin Code (`@Composable` functions) | XML Layouts (`activity_main.xml`) |
| Performance | More efficient (Recomposition) | Less efficient (View invalidation) |
| State Management | Uses `remember` and `mutableStateOf` | Uses `LiveData` or `ViewModel` |
| Reusability | High (Composable functions) | Moderate (Fragments, Custom Views) |
| Complexity | Simplified UI updates | Requires manual UI updates |

---

## **Conclusion**  

### **Summary of Key Concepts**  
- **Composition** in Jetpack Compose means **building UI using Composable functions**.  
- Uses **State Management (`remember`, `mutableStateOf`)** to update UI efficiently.  
- Supports **Stateless and Stateful Composables** for better reusability.  
- `LazyColumn` and `LazyRow` optimize list rendering.  
- Provides **effect handlers** (`LaunchedEffect`, `SideEffect`, `DisposableEffect`) for side-effects.  
- More **efficient and flexible** than XML-based UI.  
