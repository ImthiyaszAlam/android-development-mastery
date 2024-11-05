# Activities in Android

## What is an Activity?

An **Activity** is a crucial component in Android applications representing a single screen with a user interface. Activities act as entry points for user interactions and are responsible for managing the user interface and responding to user input.

## Why Use Activities?

Activities are fundamental to building user interfaces in Android apps. They allow developers to create and manage individual screens, handle user interactions, and navigate between different screens. Each Activity serves a specific purpose, such as displaying a list of items or a form to capture user input.

## How to Implement Activities?

### 1. **Define an Activity in the Manifest**

To declare an Activity, you need to add it to the `AndroidManifest.xml` file.

**Code Example:**
```xml
<activity android:name=".MainActivity">
    <intent-filter>
        <action android:name="android.intent.action.MAIN"/>
        <category android:name="android.intent.category.LAUNCHER"/>
    </intent-filter>
</activity>
```

### 2. **Create an Activity Class**

Extend the `Activity` class or one of its subclasses (e.g., `AppCompatActivity`) to create a new Activity.

**Code Example:**
```java
public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```

### 3. **Define the User Interface**

Specify the layout for the Activity in an XML file located in `res/layout/`.

**Code Example (res/layout/activity_main.xml):**
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello, World!" />
</LinearLayout>
```

### 4. **Start an Activity**

Use `Intent` to start a new Activity.

**Code Example:**
```java
Intent intent = new Intent(this, SecondActivity.class);
startActivity(intent);
```

### 5. **Handle Activity Lifecycle**

Implement lifecycle methods to manage the Activity's state, such as `onCreate()`, `onStart()`, `onResume()`, `onPause()`, `onStop()`, and `onDestroy()`.

**Code Example:**
```java
@Override
protected void onPause() {
    super.onPause();
    // Save data or pause operations
}

@Override
protected void onResume() {
    super.onResume();
    // Resume operations or refresh UI
}
```

## Prebuilt Classes and Interfaces

### 1. **Activity**
- **Description:** The base class for all activities.
- **Usage:** Extend this class to create new activities.
- **Code Example:** See `MainActivity` class above.

### 2. **AppCompatActivity**
- **Description:** A subclass of `Activity` that provides backward-compatible features and support for modern Android features.
- **Usage:** Extend this class for better compatibility with different Android versions.
- **Code Example:** See `MainActivity` class above.

### 3. **FragmentActivity**
- **Description:** A subclass of `Activity` that supports Fragments.
- **Usage:** Use this class when you need to use Fragments in your Activity.
- **Code Example:**
  ```java
  public class MyFragmentActivity extends FragmentActivity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_fragment);
      }
  }
  ```

### 4. **Intent**
- **Description:** Used for starting other activities and passing data between them.
- **Usage:** Create and use `Intent` objects to initiate activities.
- **Code Example:** See the example under "Start an Activity."

### 5. **PendingIntent**
- **Description:** A token that you give to another application (e.g., AlarmManager, NotificationManager) that allows the application to execute a predefined piece of code on your behalf.
- **Usage:** Use this class when you need to perform operations in the future.
- **Code Example:**
  ```java
  Intent intent = new Intent(this, MyBroadcastReceiver.class);
  PendingIntent pendingIntent = PendingIntent.getBroadcast(this, 0, intent, 0);
  ```

## Key Methods

### **onCreate()**
- **Description:** Called when the Activity is first created.
- **Usage:** Initialize your activity, set up the UI, and restore state if needed.
- **Code Example:** See `MainActivity` class above.

### **onStart()**
- **Description:** Called when the Activity becomes visible to the user.
- **Usage:** Prepare resources needed while the Activity is visible.
- **Code Example:**
  ```java
  @Override
  protected void onStart() {
      super.onStart();
      // Initialize resources
  }
  ```

### **onResume()**
- **Description:** Called when the Activity starts interacting with the user.
- **Usage:** Resume operations that were paused or stopped.
- **Code Example:** See `MainActivity` class above.

### **onPause()**
- **Description:** Called when the Activity is partially obscured by another activity.
- **Usage:** Save data and release resources that are not needed while the Activity is paused.
- **Code Example:** See `MainActivity` class above.

### **onStop()**
- **Description:** Called when the Activity is no longer visible to the user.
- **Usage:** Release resources that are not needed while the Activity is stopped.
- **Code Example:**
  ```java
  @Override
  protected void onStop() {
      super.onStop();
      // Release resources
  }
  ```

### **onDestroy()**
- **Description:** Called before the Activity is destroyed.
- **Usage:** Perform final cleanup before the Activity is destroyed.
- **Code Example:**
  ```java
  @Override
  protected void onDestroy() {
      super.onDestroy();
      // Final cleanup
  }
  ```

## Real-Life Examples

1. **Login Screen:**
   - An Activity that handles user authentication, takes user input, and validates credentials.

   **Code Example:**
   ```java
   public class LoginActivity extends AppCompatActivity {
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_login);
       }
   }
   ```

2. **Main Menu:**
   - An Activity that serves as the main screen of an app, providing navigation options to other Activities.

   **Code Example:**
   ```java
   public class MainMenuActivity extends AppCompatActivity {
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_main_menu);
       }
   }
   ```

3. **Settings Screen:**
   - An Activity where users can configure application settings and preferences.

   **Code Example:**
   ```java
   public class SettingsActivity extends AppCompatActivity {
       @Override
       protected void onCreate(Bundle savedInstanceState) {
           super.onCreate(savedInstanceState);
           setContentView(R.layout.activity_settings);
       }
   }
   ```

## Summary

Activities are essential components in Android development, representing screens and managing user interactions. Understanding how to create, manage, and navigate between Activities is crucial for building functional and user-friendly Android applications.

---

### Category

The topic of Activities falls into the **Basics** category. This is because understanding and implementing Activities is fundamental to building Android applications, and it covers essential concepts and methods.
