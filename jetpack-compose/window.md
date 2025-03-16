# **Window in Jetpack Compose**  

## **What is a Window in Jetpack Compose?**  
A **Window** in Jetpack Compose refers to the **visual container** that displays UI elements on the screen. It is the space where all **Compose UI components (Composables)** are drawn. A Window can be a full-screen activity, a floating window (like a popup or dialog), or even a multi-window interface in foldable or large-screen devices.

---

## **Why do we use Windows in Jetpack Compose?**  
Windows are essential in **UI design** because:  
✅ They provide a container for **all visual elements**.  
✅ They manage **user interactions** like touch gestures and keyboard inputs.  
✅ They help in building **multi-window experiences** for foldables and large screens.  
✅ They support **dialogs, popups, and tooltips** for better UI/UX.  

---

## **How does Window work in Jetpack Compose?**  
Jetpack Compose does **not** provide a direct "Window" API like in XML-based UI. Instead, it interacts with the **host Activity or Dialog**. The system manages windows through **Compose UI Components** like `Dialog`, `Popup`, and `WindowInsets`.  

---

## **Prebuilt Classes, Interfaces, and Functions Related to Window in Jetpack Compose**  

### **1. Window Class**
- **Description:** Represents a window where Compose UI is drawn.
- **Usage:** Jetpack Compose runs inside an Activity's window.
- **Example:**
  ```kotlin
  val window = (LocalContext.current as Activity).window
  ```
- **Where it is used?**  
  - Getting **window properties** (e.g., status bar, size, soft input mode).

---

### **2. WindowInsets**
- **Description:** Helps manage space occupied by system UI elements like the **status bar, navigation bar, and keyboard**.
- **Prebuilt Functions:**
  - `WindowInsets.statusBars`: Gets the status bar height.
  - `WindowInsets.navigationBars`: Gets the navigation bar height.
  - `WindowInsets.ime`: Gets the keyboard (IME) height.
- **Example:**
  ```kotlin
  val imeInsets = WindowInsets.ime.getBottom(LocalDensity.current)
  ```
- **Where it is used?**  
  - Making sure UI elements **don’t get covered** by system bars.

---

### **3. Dialog in Jetpack Compose**
- **Description:** A **popup window** that appears on top of the main window.
- **Prebuilt Function:**
  - `AlertDialog()`: Shows a simple dialog with title, message, and buttons.
  - `Dialog()`: Creates a fully customizable window/dialog.
- **Example:**
  ```kotlin
  @Composable
  fun MyDialog(showDialog: Boolean, onDismiss: () -> Unit) {
      if (showDialog) {
          AlertDialog(
              onDismissRequest = { onDismiss() },
              title = { Text("Hello!") },
              text = { Text("This is a dialog in Jetpack Compose.") },
              confirmButton = {
                  Button(onClick = { onDismiss() }) {
                      Text("OK")
                  }
              }
          )
      }
  }
  ```
- **Where it is used?**  
  - **Confirmation popups, alerts, custom dialogs.**

---

### **4. Popup in Jetpack Compose**
- **Description:** A floating window that **doesn’t take up the whole screen**.
- **Prebuilt Function:** `Popup()`
- **Example:**
  ```kotlin
  @Composable
  fun MyPopup(showPopup: Boolean, onDismiss: () -> Unit) {
      if (showPopup) {
          Popup(alignment = Alignment.Center) {
              Box(
                  Modifier
                      .size(200.dp)
                      .background(Color.White, shape = RoundedCornerShape(10.dp))
                      .padding(16.dp)
              ) {
                  Text("This is a Popup")
              }
          }
      }
  }
  ```
- **Where it is used?**  
  - **Dropdown menus, tooltips, small floating UI components.**

---

### **5. Multi-Window Support (For Foldables & Large Screens)**
- **Description:** Allows handling multiple windows in large-screen devices like **tablets and foldables**.
- **Prebuilt Function:** `calculateWindowSizeClass()`
- **Example:**
  ```kotlin
  val windowSizeClass = calculateWindowSizeClass(LocalContext.current as Activity)
  ```
- **Where it is used?**  
  - **Handling split-screen & large-screen UI layouts.**

---

## **Different Types of Windows in Jetpack Compose**
### **1. Activity Window (Main Window)**
   - **Description:** The primary window where Compose UI is drawn.
   - **Used for:** Hosting the **main UI** of an app.
   - **Example:** Every `@Composable` function inside `setContent { }` runs inside this window.
     ```kotlin
     class MainActivity : ComponentActivity() {
         override fun onCreate(savedInstanceState: Bundle?) {
             super.onCreate(savedInstanceState)
             setContent {
                 MyAppUI()
             }
         }
     }
     ```

### **2. Dialog Window**
   - **Description:** A separate floating window **on top of the main window**.
   - **Used for:** Showing **alerts, messages, forms**.
   - **Example:** `AlertDialog()`, `Dialog()`. (See example above)

### **3. Popup Window**
   - **Description:** A small window used for **tooltips, dropdowns**.
   - **Used for:** **Menus, hints, and quick info popups.**
   - **Example:** `Popup()`. (See example above)

### **4. Multi-Window Mode**
   - **Description:** Windows that **adjust to screen size changes**.
   - **Used for:** **Foldable devices, tablets, large screens**.
   - **Example:** `calculateWindowSizeClass()`. (See example above)

---

## **Real-Life Example: Adjusting UI for Large Screens**
When designing apps for **tablets & foldables**, you can change the UI based on the **window size**.

```kotlin
@Composable
fun MyResponsiveUI() {
    val windowSize = calculateWindowSizeClass(LocalContext.current as Activity)

    if (windowSize.widthSizeClass == WindowWidthSizeClass.Expanded) {
        // Show a two-pane layout for large screens
        Row {
            Text("Left Pane")
            Text("Right Pane")
        }
    } else {
        // Show a single-column layout for small screens
        Column {
            Text("Single Pane Layout")
        }
    }
}
```

---

## **Differences Between Window Types**
| Type           | Covers Whole Screen? | Supports Custom Layout? | Best Used For |
|---------------|--------------------|----------------------|--------------|
| **Activity Window** | ✅ Yes | ✅ Yes | Main UI |
| **Dialog Window** | ❌ No | ✅ Yes | Alerts, Forms |
| **Popup Window** | ❌ No | ✅ Yes | Tooltips, Menus |
| **Multi-Window** | ✅ Yes | ✅ Yes | Large Screens |

---

## **Conclusion**
- **Windows are essential** for displaying UI in Jetpack Compose.  
- **Jetpack Compose uses the Activity’s Window** to draw UI.  
- **Different types of windows (Activity, Dialog, Popup, Multi-Window)** are used based on the app’s needs.  
- **WindowInsets help manage space taken by system bars.**  
- **Handling multiple windows is crucial for large-screen and foldable devices.**  
