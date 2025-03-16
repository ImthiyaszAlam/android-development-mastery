# **State & Effect in Jetpack Compose**

## **1. What is State in Jetpack Compose?**  
State in Jetpack Compose represents **mutable data** that can change over time and trigger UI recompositions. Unlike traditional Android Views where UI updates are imperative, Compose follows a **declarative UI paradigm**, meaning the UI automatically updates when the state changes.

---

## **2. Why is State Important?**  
- **Reactivity:** The UI updates automatically when state changes.  
- **Performance:** Reduces unnecessary UI redraws by updating only the affected parts.  
- **Decoupling UI & Logic:** Encourages separation of concerns by keeping business logic separate from UI.  

---

## **3. How Does State Work?**  
- In Jetpack Compose, state is stored in **Composables** and observed automatically.  
- When the state updates, only the necessary UI elements recompose.  
- **State Hoisting** is used to lift the state from a child to a parent Composable for better management.

### **Basic Example of State in Jetpack Compose**
```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }

    Column(
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Text(text = "Count: $count", fontSize = 24.sp)
        Button(onClick = { count++ }) {
            Text("Increase Count")
        }
    }
}
```
🔹 `mutableStateOf(0)`: Holds the current state of `count`.  
🔹 `remember {}`: Keeps the state alive during recompositions.  
🔹 `by` keyword: Delegates the state variable for cleaner syntax.

---

## **4. Types of State in Jetpack Compose**
### **1. Remembered State**
- `remember` helps retain a state across recompositions.
- Example:
  ```kotlin
  @Composable
  fun RememberExample() {
      val textState = remember { mutableStateOf("Hello") }

      TextField(
          value = textState.value,
          onValueChange = { textState.value = it }
      )
  }
  ```
  
### **2. Hoisted State**
- Moves state to the parent Composable for better state management.
- Example:
  ```kotlin
  @Composable
  fun ParentComposable() {
      var name by remember { mutableStateOf("") }

      ChildComposable(name, onNameChange = { name = it })
  }

  @Composable
  fun ChildComposable(name: String, onNameChange: (String) -> Unit) {
      TextField(value = name, onValueChange = onNameChange)
  }
  ```

### **3. ViewModel State**
- Stores state across configuration changes.
- Example:
  ```kotlin
  class CounterViewModel : ViewModel() {
      var count by mutableStateOf(0)
          private set

      fun increaseCount() {
          count++
      }
  }

  @Composable
  fun CounterScreen(viewModel: CounterViewModel = viewModel()) {
      Column {
          Text("Count: ${viewModel.count}")
          Button(onClick = { viewModel.increaseCount() }) {
              Text("Increase")
          }
      }
  }
  ```

### **4. Flow & LiveData with State**
- `collectAsState()` and `observeAsState()` help integrate Compose with `Flow` and `LiveData`.

#### **Using Flow in Compose**
```kotlin
@Composable
fun FlowExample(viewModel: MyViewModel) {
    val state by viewModel.flowData.collectAsState(initial = "")
    Text(text = state)
}
```

#### **Using LiveData in Compose**
```kotlin
@Composable
fun LiveDataExample(viewModel: MyViewModel) {
    val state by viewModel.liveData.observeAsState("")
    Text(text = state)
}
```

---

## **5. What are Side Effects in Jetpack Compose?**
**Effects in Compose** handle operations that don’t directly change UI but interact with other components like APIs, databases, or timers.

### **Common Effects**
1. **LaunchedEffect**
2. **rememberCoroutineScope**
3. **SideEffect**
4. **DisposableEffect**
5. **produceState**
6. **derivedStateOf**

---

## **6. Prebuilt Classes & Functions in Jetpack Compose Related to State & Effects**

| **Function/Class**  | **Usage**  | **Example**  |
|---------------------|------------|--------------|
| `remember` | Retains state across recompositions | `val text = remember { mutableStateOf("Hello") }` |
| `mutableStateOf` | Creates a mutable state | `var count by remember { mutableStateOf(0) }` |
| `rememberSaveable` | Retains state across configuration changes | `val name = rememberSaveable { mutableStateOf("") }` |
| `collectAsState` | Converts a `Flow` into a state | `val data by flow.collectAsState(initial = "")` |
| `observeAsState` | Converts `LiveData` into a state | `val data by liveData.observeAsState(initial = "")` |
| `LaunchedEffect` | Executes code when a key changes | `LaunchedEffect(Unit) { fetchData() }` |
| `rememberCoroutineScope` | Gets a coroutine scope | `val scope = rememberCoroutineScope()` |
| `SideEffect` | Runs an operation after recomposition | `SideEffect { Log.d("Recomposition", "Triggered") }` |
| `DisposableEffect` | Cleans up when a Composable leaves the UI | `DisposableEffect(key) { onDispose { cleanup() } }` |
| `produceState` | Converts asynchronous data into a state | `val data by produceState(initialValue = "") { value = fetchData() }` |
| `derivedStateOf` | Optimizes recomposition based on derived states | `val derived = remember { derivedStateOf { someCalculation() } }` |

---

## **7. Real-Life Examples of Side Effects in Jetpack Compose**

### **Example 1: Fetching Data from an API (LaunchedEffect)**
```kotlin
@Composable
fun ApiCallExample() {
    var data by remember { mutableStateOf("Loading...") }

    LaunchedEffect(Unit) {
        data = fetchDataFromApi()
    }

    Text(text = data)
}
```
🔹 **Why?** Ensures API calls are triggered once when the Composable appears.

---

### **Example 2: Timer using rememberCoroutineScope**
```kotlin
@Composable
fun TimerExample() {
    val scope = rememberCoroutineScope()
    var time by remember { mutableStateOf(0) }

    Button(onClick = {
        scope.launch {
            while (true) {
                delay(1000)
                time++
            }
        }
    }) {
        Text("Time: $time sec")
    }
}
```
🔹 **Why?** Ensures the coroutine launches only when needed.

---

## **8. Differences Between State & Effects**
| **Feature**         | **State**                                | **Effect**                              |
|---------------------|----------------------------------------|----------------------------------------|
| **Purpose**        | Holds UI-related data | Handles external operations |
| **Triggers Recomposition?** | Yes | No (used for side effects) |
| **Common Use Cases** | UI updates, state management | API calls, logging, lifecycle events |
| **Examples**        | `remember`, `mutableStateOf` | `LaunchedEffect`, `SideEffect` |

---

### **Summary**
- **State**: Stores and manages UI data, ensuring UI updates automatically.  
- **Effects**: Executes non-UI logic, such as API calls, coroutines, and logging.  
- **Types of State**: Remembered state, hoisted state, ViewModel state, Flow & LiveData.  
- **Side Effects**: `LaunchedEffect`, `SideEffect`, `DisposableEffect`, etc.  
- **Real-Life Examples**: API calls, timers, animations.
