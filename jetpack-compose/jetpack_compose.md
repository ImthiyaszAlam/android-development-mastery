# 📌 Jetpack Compose (Android-Kotlin)

## 📖 What is Jetpack Compose?

Jetpack Compose is **Android’s modern UI toolkit** for building native UI using a **declarative programming model**. It simplifies UI development, making it faster and more efficient compared to XML-based layouts.

## ❓ Why Jetpack Compose?

### ✅ Benefits:
1. **Declarative UI:** Define the UI with composable functions instead of using XML.
2. **Less Boilerplate Code:** No need for XML + View Binding. Everything is done in Kotlin.
3. **Easier UI State Management:** Uses **State Hoisting** and `remember` to manage UI state efficiently.
4. **Better Performance:** Reduces unnecessary recompositions.
5. **Built-in Animation Support:** Provides an intuitive animation API.
6. **Interoperability with Views:** Can be used alongside existing XML-based views.
7. **Theme & Styling:** Uses `MaterialTheme` for easy theming.

---

## 🔄 How Jetpack Compose Works?

Jetpack Compose relies on **Composable Functions** that describe UI in a declarative way. These functions:
- Take in data as input.
- Automatically update when data changes.
- Are **recomposable**, meaning the UI updates dynamically.

**Example of a simple Composable function:**
```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```

To display this in an app:
```kotlin
setContent {
    Greeting(name = "Jetpack Compose")
}
```

---

# 🏗️ Jetpack Compose Components

## 📌 1. Composable Functions (`@Composable`)
- **Definition:** Functions annotated with `@Composable` build UI elements.
- **Example:**
  ```kotlin
  @Composable
  fun MyButton() {
      Button(onClick = { /* Handle Click */ }) {
          Text("Click Me")
      }
  }
  ```

---

## 📌 2. Prebuilt Classes, Functions & Interfaces

### ✅ UI Components (Widgets)
Jetpack Compose provides ready-made UI components to replace traditional `View` components.

| Jetpack Compose Component | Equivalent in XML |
|----------------------------|------------------|
| `Text()` | `TextView` |
| `Button()` | `Button` |
| `Image()` | `ImageView` |
| `Column()` | `LinearLayout (Vertical)` |
| `Row()` | `LinearLayout (Horizontal)` |
| `Box()` | `FrameLayout` |
| `LazyColumn()` | `RecyclerView` |
| `Card()` | `CardView` |

---

### ✅ 3. Layouts
Layouts in Jetpack Compose determine how UI elements are positioned.

| Layout | Description | Example |
|--------|------------|---------|
| `Column()` | Stacks elements vertically. | `Column { Text("Item 1") }` |
| `Row()` | Stacks elements horizontally. | `Row { Text("Item 1") }` |
| `Box()` | Overlaps elements. | `Box { Text("On Top") }` |
| `LazyColumn()` | Efficient scrolling list. | `LazyColumn { items(list) { Text(it) } }` |

#### **Example: Row + Column + Box**
```kotlin
@Composable
fun MyLayout() {
    Column {
        Text("First Item")
        Row {
            Text("Left")
            Spacer(modifier = Modifier.width(8.dp))
            Text("Right")
        }
        Box {
            Text("Overlapping Text")
        }
    }
}
```

---

### ✅ 4. State Management
**Jetpack Compose re-renders UI automatically when state changes.**

| State Concept | Description | Example |
|--------------|------------|---------|
| `remember { mutableStateOf() }` | Stores UI state. | `val count = remember { mutableStateOf(0) }` |
| `LaunchedEffect()` | Runs a function once when composable is created. | `LaunchedEffect(Unit) { fetchData() }` |
| `rememberUpdatedState()` | Preserves state when recomposing. | `val text = rememberUpdatedState(newText)` |

#### **Example: Counter App with State**
```kotlin
@Composable
fun Counter() {
    var count by remember { mutableStateOf(0) }
    Column {
        Text("Count: $count")
        Button(onClick = { count++ }) {
            Text("Increase")
        }
    }
}
```

---

### ✅ 5. Navigation in Jetpack Compose
Jetpack Compose uses `NavHost` for navigation between screens.

#### **Navigation Example**
```kotlin
@Composable
fun MyApp() {
    val navController = rememberNavController()
    NavHost(navController, startDestination = "home") {
        composable("home") { HomeScreen(navController) }
        composable("details") { DetailsScreen() }
    }
}
```

---

### ✅ 6. Animations
Jetpack Compose provides easy-to-use animations.

#### **Example: Fade-in Animation**
```kotlin
@Composable
fun FadeInText() {
    val alpha = remember { Animatable(0f) }
    LaunchedEffect(Unit) {
        alpha.animateTo(1f, animationSpec = tween(durationMillis = 1000))
    }
    Text("Hello", modifier = Modifier.alpha(alpha.value))
}
```

---

### ✅ 7. Gesture Handling
Jetpack Compose handles gestures like clicks, drags, and swipes.

#### **Example: Clickable Modifier**
```kotlin
@Composable
fun ClickableText() {
    Text(
        "Click Me",
        modifier = Modifier.clickable { println("Clicked!") }
    )
}
```

---

### ✅ 8. Material Design
Jetpack Compose supports **Material Design** with `MaterialTheme`.

#### **Example: Themed Button**
```kotlin
@Composable
fun ThemedButton() {
    Button(
        onClick = {},
        colors = ButtonDefaults.buttonColors(backgroundColor = MaterialTheme.colors.primary)
    ) {
        Text("Material Button")
    }
}
```

---

# 🎯 Real-Life Example: Notes App with Jetpack Compose

#### **1. Define Model**
```kotlin
data class Note(val title: String, val content: String)
```

#### **2. Define UI**
```kotlin
@Composable
fun NoteItem(note: Note) {
    Column {
        Text(text = note.title, fontWeight = FontWeight.Bold)
        Text(text = note.content)
    }
}
```

#### **3. List of Notes**
```kotlin
@Composable
fun NotesList(notes: List<Note>) {
    LazyColumn {
        items(notes) { note ->
            NoteItem(note)
        }
    }
}
```

#### **4. Main App**
```kotlin
@Composable
fun MyApp() {
    val notes = listOf(
        Note("Meeting", "Discuss project"),
        Note("Shopping", "Buy groceries")
    )
    NotesList(notes)
}
```

---

# 🚀 Differences: Jetpack Compose vs XML UI

| Feature | Jetpack Compose | XML UI |
|---------|---------------|--------|
| Code Length | Less Code | More Boilerplate Code |
| UI Creation | Declarative (Composable Functions) | Imperative (XML + View Binding) |
| Performance | Faster Rendering | Requires Manual Optimization |
| State Handling | Built-in (`remember`) | Requires ViewModel & LiveData |
| Integration | Works with XML Views | Only XML |

---

# 🔥 Conclusion
Jetpack Compose is **the future of Android UI development**. It simplifies UI building with **less code, better performance, and seaml
