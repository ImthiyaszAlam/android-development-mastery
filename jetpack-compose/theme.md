# **Theme in Jetpack Compose**  

## **What is Theme in Jetpack Compose?**  
A **theme** in Jetpack Compose defines the overall appearance of an app, including **colors, typography, and shapes**. It helps maintain a **consistent design** across the app and makes it easy to switch between **light and dark modes**.  

## **Why Use Themes?**  
- **Consistency:** Ensures all UI components follow the same design.  
- **Easier Maintenance:** Changes to colors or typography can be made in one place.  
- **Dark Mode Support:** Enables automatic switching between light and dark themes.  
- **Customizable:** You can create custom themes to match branding.  

---

## **How to Use Themes in Jetpack Compose?**  

### **1. Creating a Theme**  
Jetpack Compose uses **MaterialTheme**, which provides default values for **colors, typography, and shapes**.  

**Basic Theme Structure:**  
```kotlin
@Composable
fun MyAppTheme(content: @Composable () -> Unit) {
    MaterialTheme(
        colorScheme = lightColorScheme(), // Colors
        typography = Typography,         // Text styles
        shapes = Shapes,                 // Shapes
        content = content
    )
}
```

- `colorScheme`: Defines colors used in the app (background, text, buttons, etc.).  
- `typography`: Defines text styles (font, size, weight, etc.).  
- `shapes`: Defines shapes for buttons, cards, etc.  

---

## **Prebuilt Classes, Functions, and Interfaces Related to Themes**  

### **1. MaterialTheme (Prebuilt Class)**  
- **What:** A wrapper that applies the theme to all UI elements inside it.  
- **Usage:** It should wrap the entire app or screen.  
- **Code Example:**  
  ```kotlin
  @Composable
  fun MyScreen() {
      MaterialTheme {
          Text(text = "Hello, Theme!", style = MaterialTheme.typography.bodyLarge)
      }
  }
  ```

---

### **2. ColorScheme (Prebuilt Class)**  
- **What:** Defines colors used in the app (primary, secondary, background, etc.).  
- **Usage:** Helps in maintaining a uniform color scheme.  
- **Code Example:**  
  ```kotlin
  val myColors = lightColorScheme(
      primary = Color(0xFF6200EE),
      secondary = Color(0xFF03DAC5),
      background = Color.White,
      onPrimary = Color.White
  )

  @Composable
  fun MyTheme(content: @Composable () -> Unit) {
      MaterialTheme(
          colorScheme = myColors,
          content = content
      )
  }
  ```

---

### **3. Typography (Prebuilt Class)**  
- **What:** Defines text styles (font size, weight, etc.).  
- **Usage:** Ensures text styles are consistent across the app.  
- **Code Example:**  
  ```kotlin
  val myTypography = Typography(
      bodyLarge = TextStyle(
          fontSize = 16.sp,
          fontWeight = FontWeight.Normal,
          color = Color.Black
      )
  )

  @Composable
  fun MyTheme(content: @Composable () -> Unit) {
      MaterialTheme(
          typography = myTypography,
          content = content
      )
  }
  ```

---

### **4. Shapes (Prebuilt Class)**  
- **What:** Defines shapes used for UI components like buttons and cards.  
- **Usage:** Helps maintain a uniform look and feel for UI elements.  
- **Code Example:**  
  ```kotlin
  val myShapes = Shapes(
      small = RoundedCornerShape(4.dp),
      medium = RoundedCornerShape(8.dp),
      large = RoundedCornerShape(16.dp)
  )

  @Composable
  fun MyTheme(content: @Composable () -> Unit) {
      MaterialTheme(
          shapes = myShapes,
          content = content
      )
  }
  ```

---

### **5. lightColorScheme() & darkColorScheme() (Prebuilt Functions)**  
- **What:** Defines color schemes for light and dark themes.  
- **Usage:** Helps in implementing light and dark mode themes easily.  
- **Code Example:**  
  ```kotlin
  val LightColors = lightColorScheme(
      primary = Color(0xFF6200EE),
      secondary = Color(0xFF03DAC5),
      background = Color.White
  )

  val DarkColors = darkColorScheme(
      primary = Color(0xFFBB86FC),
      secondary = Color(0xFF03DAC5),
      background = Color.Black
  )

  @Composable
  fun MyAppTheme(darkTheme: Boolean, content: @Composable () -> Unit) {
      val colors = if (darkTheme) DarkColors else LightColors
      MaterialTheme(colorScheme = colors, content = content)
  }
  ```

---

### **Different Types of Themes in Jetpack Compose**  

| Theme Type  | Description | When to Use? |
|-------------|------------|--------------|
| **Light Theme** | Uses bright colors (white backgrounds, dark text). | Default for most apps. |
| **Dark Theme** | Uses dark colors (black backgrounds, white text). | When users enable dark mode. |
| **Dynamic Theme** | Uses system-defined colors. | When you want colors to adapt based on the device. |

---

## **How to Switch Between Light and Dark Themes?**  
You can check the system setting and apply the theme dynamically.  

**Example:**  
```kotlin
@Composable
fun MyApp() {
    val isDarkTheme = isSystemInDarkTheme() // Checks system theme
    MyAppTheme(darkTheme = isDarkTheme) {
        // Your app UI
    }
}
```

---

## **Real-Life Example: Theming a Button**  
Let's apply a theme to a **Button** that changes based on the theme mode.

```kotlin
@Composable
fun ThemedButton() {
    Button(
        onClick = { /* Handle Click */ },
        colors = ButtonDefaults.buttonColors(backgroundColor = MaterialTheme.colorScheme.primary)
    ) {
        Text(text = "Click Me", color = MaterialTheme.colorScheme.onPrimary)
    }
}
```
- In **light mode**, the button will have a purple background.  
- In **dark mode**, it will adapt to a different color.  

---

## **Differences Between Jetpack Compose Theme and XML-based Themes**  

| Feature | Jetpack Compose Theme | XML-based Theme |
|---------|----------------------|----------------|
| Definition | Uses `MaterialTheme` and Kotlin code. | Uses `styles.xml`. |
| Flexibility | Dynamic and easy to modify. | Static and harder to change. |
| Dark Mode | Built-in support. | Requires separate themes. |
| Customization | More control over colors, shapes, and typography. | Limited customization options. |

---

## **Summary**  

- **What is Theme?** A way to define the app's colors, typography, and shapes.  
- **Why Use It?** Ensures consistency, makes maintenance easy, and supports dark mode.  
- **How to Implement?** Use `MaterialTheme`, `ColorScheme`, `Typography`, and `Shapes`.  
- **Types of Themes?** Light, Dark, and Dynamic.  
- **Real-life Example?** Themed buttons, text styles, and dark mode support.  
