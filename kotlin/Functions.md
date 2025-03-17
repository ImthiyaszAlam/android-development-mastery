# **Functions in Kotlin (Complete Guide)**

## **1. What are Functions?**  
A function is a **block of reusable code** that performs a specific task. It helps to organize and reuse code, making programs **more readable, maintainable, and efficient**.

---

## **2. Why Use Functions?**
- **Code Reusability** → Write once, use multiple times.
- **Modularity** → Break large programs into smaller, manageable parts.
- **Readability** → Code becomes easier to understand.
- **Debugging** → Easier to find and fix errors.
- **Avoid Repetition** → Reduce duplicate code.

---

## **3. How to Define a Function in Kotlin?**
A function in Kotlin is defined using the `fun` keyword. The basic syntax is:

```kotlin
fun functionName(parameters): ReturnType {
    // Function body
    return value
}
```

### **Example: A Simple Function**
```kotlin
fun greet() {
    println("Hello, Kotlin!")
}

fun main() {
    greet() // Calling the function
}
```
**Output:**
```
Hello, Kotlin!
```

---

## **4. Different Types of Functions in Kotlin**
### **1. Standard Functions**
These are normal functions that take input, process it, and return a result.

#### **Example: Function with Parameters and Return Type**
```kotlin
fun add(a: Int, b: Int): Int {
    return a + b
}

fun main() {
    val result = add(5, 10)
    println("Sum: $result")
}
```
**Output:**
```
Sum: 15
```

---

### **2. Single Expression Functions (Compact Function)**
If a function has only **one statement**, it can be written in a **shorter form** using `=`.

#### **Example:**
```kotlin
fun square(n: Int) = n * n

fun main() {
    println(square(4)) // Output: 16
}
```

---

### **3. Inline Functions**
- **Why?** → Improves performance by avoiding function call overhead.
- **What?** → The compiler **copies** the function body to where it’s called.

#### **Example:**
```kotlin
inline fun showMessage() {
    println("Hello, Inline Function!")
}

fun main() {
    showMessage()
}
```

---

### **4. Higher-Order Functions**
- **Why?** → Helps in functional programming.
- **What?** → A function that takes another function as a parameter **or** returns a function.

#### **Example:**
```kotlin
fun operateOnNumbers(a: Int, b: Int, operation: (Int, Int) -> Int): Int {
    return operation(a, b)
}

fun main() {
    val sum = operateOnNumbers(5, 10) { x, y -> x + y }
    println(sum) // Output: 15
}
```

---

### **5. Lambda Functions (Anonymous Functions)**
- **Why?** → Useful when a function is required **only once**.
- **What?** → A function **without a name**.

#### **Example:**
```kotlin
val multiply = { a: Int, b: Int -> a * b }

fun main() {
    println(multiply(4, 5)) // Output: 20
}
```

---

### **6. Extension Functions**
- **Why?** → Add functionality to an **existing class** without modifying it.
- **What?** → A function defined outside a class but acts as if it's part of the class.

#### **Example:**
```kotlin
fun String.reverseText(): String {
    return this.reversed()
}

fun main() {
    println("hello".reverseText()) // Output: olleh
}
```

---

### **7. Recursive Functions**
- **Why?** → When a problem can be **broken down into smaller subproblems**.
- **What?** → A function that calls itself.

#### **Example: Factorial Calculation**
```kotlin
fun factorial(n: Int): Int {
    return if (n == 1) 1 else n * factorial(n - 1)
}

fun main() {
    println(factorial(5)) // Output: 120
}
```

---

## **5. Prebuilt Functions in Kotlin**
Kotlin provides many built-in functions for various tasks.

### **String Functions**
| Function | Description | Example |
|----------|------------|---------|
| `.length` | Returns length of string | `"Kotlin".length` → `6` |
| `.uppercase()` | Converts to uppercase | `"hello".uppercase()` → `"HELLO"` |
| `.lowercase()` | Converts to lowercase | `"HELLO".lowercase()` → `"hello"` |
| `.reversed()` | Reverses the string | `"kotlin".reversed()` → `"niltok"` |

#### **Example:**
```kotlin
fun main() {
    val text = "Kotlin"
    println(text.length)      // 6
    println(text.uppercase()) // KOTLIN
}
```

---

### **List Functions**
| Function | Description | Example |
|----------|------------|---------|
| `.size` | Returns number of elements | `list.size` |
| `.first()` | Returns first element | `list.first()` |
| `.last()` | Returns last element | `list.last()` |
| `.sorted()` | Returns sorted list | `list.sorted()` |

#### **Example:**
```kotlin
fun main() {
    val numbers = listOf(3, 1, 4, 1, 5)
    println(numbers.sorted()) // [1, 1, 3, 4, 5]
}
```

---

### **Math Functions**
| Function | Description | Example |
|----------|------------|---------|
| `max(a, b)` | Returns max of two numbers | `max(5, 10) → 10` |
| `min(a, b)` | Returns min of two numbers | `min(5, 10) → 5` |
| `sqrt(x)` | Returns square root | `sqrt(16.0) → 4.0` |

#### **Example:**
```kotlin
import kotlin.math.*

fun main() {
    println(sqrt(16.0)) // 4.0
}
```

---

## **6. Prebuilt Classes & Interfaces Related to Functions**
| Class | Description |
|-------|------------|
| `Function` | Represents a function type |
| `Lambda` | Represents an anonymous function |
| `inline` | Optimizes function calls |

#### **Example: Using Function Class**
```kotlin
fun main() {
    val add: (Int, Int) -> Int = { a, b -> a + b }
    println(add(5, 10)) // Output: 15
}
```

---

## **7. Differences Between Function Types**
| Type | What it does | Example |
|------|-------------|---------|
| Standard Function | Regular function with name and body | `fun add(a: Int, b: Int): Int { return a + b }` |
| Lambda Function | Anonymous function | `val sum = { a: Int, b: Int -> a + b }` |
| Inline Function | Replaces function call with function body | `inline fun show() { println("Hello") }` |
| Higher-Order Function | Takes a function as a parameter | `fun operate(a: Int, fn: (Int) -> Int) = fn(a)` |

---

## **8. Real-Life Use Cases**
1. **Utility Functions** → String manipulation, mathematical calculations.
2. **Higher-Order Functions** → Filtering lists, sorting, mapping.
3. **Extension Functions** → Custom functionalities on existing classes.
4. **Lambda Expressions** → Event handling in Android.

---

## **9. Summary**
- Functions **make code reusable, readable, and maintainable**.
- Kotlin provides **built-in functions** for Strings, Lists, and Math operations.
- Supports **different types of functions** (Standard, Lambda, Higher-Order, etc.).
- **Understanding functions** is **crucial for Android development**.
