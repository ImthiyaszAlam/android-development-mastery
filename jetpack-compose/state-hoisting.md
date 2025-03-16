# **State Hoisting in Jetpack Compose**  

## **What is State Hoisting?**  
State Hoisting is a design pattern in **Jetpack Compose** where you lift (hoist) the state from a composable function to its parent. Instead of keeping state inside a UI component, you move it up to allow better reusability, testing, and state management.  

### **Simple Definition:**  
- State hoisting means **lifting the state up** from a UI component to its parent.  
- The **parent** manages the state and passes it down to its child.  
- The **child** only displays data and notifies the parent about changes.  

## **Why Use State Hoisting?**  
1. **Separation of Concerns:** UI components (composables) should **only display** data, while the parent manages logic and state.  
2. **Better Reusability:** The child composable can be used with different state values.  
3. **Easy Testing:** Since state logic is in the parent, testing becomes simpler.  
4. **Improved Maintainability:** Keeping UI and logic separate makes debugging easier.  
5. **Efficient State Management:** Helps avoid unnecessary recompositions, improving performance.  

---

## **How State Hoisting Works?**  
State hoisting follows a simple principle:  
- **Instead of storing state inside a composable, move it to its parent.**  
- The parent **owns** the state and passes it as a parameter to the child.  
- The child **only displays** the data and informs the parent when it changes.  

### **General Structure**  
- **Parent Composable**: Stores and manages the state.  
- **Child Composable**: Receives the state and updates it through a callback.  

---

## **Example of State Hoisting**  
Let's say we have a **TextField** where a user can enter their name.

### ❌ **Without State Hoisting (Bad Practice)**  
Here, the state is **inside** the child composable (`NameInput`). This is not reusable.

```kotlin
@Composable
fun NameInput() {
    var name by remember { mutableStateOf("") } // State inside the child

    TextField(
        value = name,
        onValueChange = { name = it }, // Updates local state
        label = { Text("Enter your name") }
    )
}
```
### ✅ **With State Hoisting (Good Practice)**  
Here, the parent (`UserScreen`) manages the state and passes it to the child (`NameInput`).

```kotlin
@Composable
fun UserScreen() {
    var name by remember { mutableStateOf("") } // State in the parent

    Column {
        NameInput(name = name, onNameChange = { name = it }) // Passing state & callback
        Text("Hello, $name!") // Display the updated name
    }
}

@Composable
fun NameInput(name: String, onNameChange: (String) -> Unit) {
    TextField(
        value = name,
        onValueChange = onNameChange, // Parent manages state update
        label = { Text("Enter your name") }
    )
}
```

### **Key Differences**
| Without Hoisting | With Hoisting |
|----------------|-------------|
| State is inside the child | State is in the parent |
| Harder to reuse | Can reuse in multiple places |
| Difficult to test | Easier to test |
| UI and logic mixed | UI and logic separated |

---

## **Prebuilt Classes, Interfaces, and Functions Related to State Hoisting**  

### **1. remember**
- **What:** Stores state in a composable.  
- **Why:** Keeps state across recompositions.  
- **Usage:** Wraps a state variable so it doesn’t reset.  
- **Example:**  
  ```kotlin
  val count by remember { mutableStateOf(0) }
  ```

### **2. mutableStateOf**
- **What:** Creates a state variable.  
- **Why:** Allows UI to react to changes.  
- **Example:**  
  ```kotlin
  var text by remember { mutableStateOf("") }
  ```

### **3. rememberSaveable**
- **What:** Same as `remember`, but **preserves state** during configuration changes (e.g., screen rotation).  
- **Example:**  
  ```kotlin
  var name by rememberSaveable { mutableStateOf("") }
  ```

### **4. State<T> & MutableState<T>**
- **What:** Represents **read-only** (`State`) and **mutable** (`MutableState`) state values.  
- **Example:**  
  ```kotlin
  val count: State<Int> = remember { mutableStateOf(0) }
  ```

### **5. CompositionLocal**
- **What:** Shares state across multiple composables **without** passing parameters.  
- **Why:** Useful for themes, user preferences, etc.  
- **Example:**  
  ```kotlin
  val MyLocalState = compositionLocalOf { "Default Value" }
  ```

---

## **Different Types of State Hoisting (if any)**  

### **1. Single Source of Truth**
- Always **keep state in one place** (usually the highest possible parent).  

### **2. Unidirectional Data Flow (UDF)**
- **Data flows down** (from parent to child).  
- **Events flow up** (from child to parent).  

### **3. ViewModel + State Hoisting**
- Store state in a `ViewModel` instead of a composable to persist it across screen changes.  
- Example:  
  ```kotlin
  class UserViewModel : ViewModel() {
      var name by mutableStateOf("")
  }

  @Composable
  fun UserScreen(viewModel: UserViewModel = viewModel()) {
      NameInput(name = viewModel.name, onNameChange = { viewModel.name = it })
  }
  ```

---

## **Real-Life Examples**
### **1. Login Form with State Hoisting**
```kotlin
@Composable
fun LoginScreen() {
    var email by remember { mutableStateOf("") }
    var password by remember { mutableStateOf("") }

    Column {
        TextField(value = email, onValueChange = { email = it }, label = { Text("Email") })
        TextField(value = password, onValueChange = { password = it }, label = { Text("Password") })
        Button(onClick = { /* Handle Login */ }) {
            Text("Login")
        }
    }
}
```

### **2. Counter App with State Hoisting**
```kotlin
@Composable
fun CounterScreen() {
    var count by remember { mutableStateOf(0) }

    Column {
        Counter(count = count, onIncrement = { count++ })
        Text("Current Count: $count")
    }
}

@Composable
fun Counter(count: Int, onIncrement: () -> Unit) {
    Button(onClick = onIncrement) {
        Text("Increase Count")
    }
}
```

---

## **Summary**
- **What?** State Hoisting lifts state from a composable to its parent.  
- **Why?** Improves reusability, testing, and maintainability.  
- **How?** Parent stores the state and passes it to the child.  
- **Prebuilt Functions & Classes:** `remember`, `mutableStateOf`, `rememberSaveable`, `State`, `MutableState`, `ViewModel`.  
- **Different Types:** Single Source of Truth, Unidirectional Data Flow, ViewModel Hoisting.  
- **Real-Life Examples:** Login Forms, Counter Apps, Text Inputs.  

