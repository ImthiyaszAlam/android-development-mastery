# Jetpack Compose

## What is Jetpack Compose?

Jetpack Compose is a modern toolkit for building native UI in Android. It simplifies and accelerates UI development on Android with less code, powerful tools, and intuitive Kotlin APIs. Compose is fully declarative, meaning you describe your UI with composable functions that update automatically when the data changes.

## Why Use Jetpack Compose?

- **Declarative Syntax:** Compose uses a declarative syntax to define UI elements, making it more intuitive and easier to understand.
- **Less Code:** Reduces boilerplate code compared to traditional XML-based layouts.
- **Kotlin Integration:** Leverages Kotlin language features for a more concise and expressive API.
- **Reactivity:** Automatically updates the UI when the underlying data changes.
- **Interoperability:** Can be used alongside existing Android views and libraries.

## How to Use Jetpack Compose?

1. **Setup:**
   - Add Jetpack Compose dependencies to your `build.gradle` file.
   - Enable Jetpack Compose in your project.

   ```gradle
   android {
       ...
       buildFeatures {
           compose true
       }
       composeOptions {
           kotlinCompilerExtensionVersion "1.5.0" // Update to the latest version
       }
   }

   dependencies {
       implementation "androidx.compose.ui:ui:1.5.0"
       implementation "androidx.compose.material:material:1.5.0"
       implementation "androidx.compose.ui:ui-tooling-preview:1.5.0"
       implementation "androidx.lifecycle:lifecycle-runtime-ktx:2.6.0"
       implementation "androidx.activity:activity-compose:1.7.0"
   }
   ```

2. **Create Composables:**
   - Define composable functions to build your UI components.

   ```kotlin
   @Composable
   fun Greeting(name: String) {
       Text(text = "Hello, $name!")
   }
   ```

3. **Use Composables in a UI:**
   - Set up your app’s main UI using composables.

   ```kotlin
   @Composable
   fun MyApp() {
       MaterialTheme {
           Greeting(name = "World")
       }
   }

   @Preview(showBackground = true)
   @Composable
   fun DefaultPreview() {
       MyApp()
   }
   ```

## Prebuilt Classes and Interfaces

### 1. **Composable**
- **Description:** Annotation to define a composable function.
- **Usage:** Annotate functions to make them composable.
- **Code Example:**
  ```kotlin
  @Composable
  fun MyComposable() {
      // Composable content
  }
  ```

### 2. **MaterialTheme**
- **Description:** Provides a set of Material Design styles for composables.
- **Usage:** Wrap your UI with `MaterialTheme` to use Material Design components.
- **Code Example:**
  ```kotlin
  @Composable
  fun MyApp() {
      MaterialTheme {
          // UI content
      }
  }
  ```

### 3. **Text**
- **Description:** Displays a piece of text with customizable styling.
- **Usage:** Use this composable to show text on the screen.
- **Code Example:**
  ```kotlin
  @Composable
  fun Greeting(name: String) {
      Text(text = "Hello, $name!")
  }
  ```

### 4. **Button**
- **Description:** A button that users can interact with.
- **Usage:** Create buttons that handle user clicks.
- **Code Example:**
  ```kotlin
  @Composable
  fun MyButton(onClick: () -> Unit) {
      Button(onClick = onClick) {
          Text("Click Me")
      }
  }
  ```

### 5. **Column, Row, Box**
- **Description:** Layout composables for arranging child composables in vertical or horizontal order.
- **Usage:** Use these to build your layout structure.
- **Code Example:**
  ```kotlin
  @Composable
  fun MyLayout() {
      Column {
          Text("Item 1")
          Text("Item 2")
      }
  }
  ```

### 6. **Modifier**
- **Description:** Allows you to modify the appearance or behavior of composables.
- **Usage:** Apply styles, padding, and other attributes.
- **Code Example:**
  ```kotlin
  @Composable
  fun StyledText() {
      Text(
          text = "Styled Text",
          modifier = Modifier.padding(16.dp)
      )
  }
  ```

### 7. **State**
- **Description:** Represents mutable state that is observed by composables.
- **Usage:** Use `remember` and `mutableStateOf` to handle state changes.
- **Code Example:**
  ```kotlin
  @Composable
  fun Counter() {
      var count by remember { mutableStateOf(0) }
      Column {
          Text("Count: $count")
          Button(onClick = { count++ }) {
              Text("Increment")
          }
      }
  }
  ```

### 8. **LiveData and StateFlow**
- **Description:** Provides reactive state handling.
- **Usage:** Observe LiveData or StateFlow for state changes.
- **Code Example:**
  ```kotlin
  @Composable
  fun MyLiveDataObserver(viewModel: MyViewModel) {
      val state by viewModel.myLiveData.observeAsState()
      Text(text = state ?: "Loading...")
  }
  ```

## Real-Life Examples

1. **Simple User Interface:**
   - Create a screen with a text greeting and a button.

   **Code Example:**
   ```kotlin
   @Composable
   fun GreetingScreen() {
       Column(modifier = Modifier.padding(16.dp)) {
           Text("Hello, Jetpack Compose!")
           Button(onClick = { /* Handle click */ }) {
               Text("Click Me")
           }
       }
   }
   ```

2. **List Display:**
   - Display a list of items using `LazyColumn`.

   **Code Example:**
   ```kotlin
   @Composable
   fun ItemList(items: List<String>) {
       LazyColumn {
           items(items) { item ->
               Text(text = item, modifier = Modifier.padding(8.dp))
           }
       }
   }
   ```

3. **State Management:**
   - Implement a counter with state management.

   **Code Example:**
   ```kotlin
   @Composable
   fun Counter() {
       var count by remember { mutableStateOf(0) }
       Column {
           Text("Count: $count")
           Button(onClick = { count++ }) {
               Text("Increment")
           }
       }
   }
   ```

## Summary

Jetpack Compose is a modern toolkit that simplifies UI development on Android by providing a declarative API. It enables faster development with less code and integrates seamlessly with Kotlin features.

---

### Category
Jetpack Compose falls into the **Advanced** category due to its modern and powerful approach to UI development and its integration with Kotlin features.
