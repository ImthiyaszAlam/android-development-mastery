# Activity Lifecycle

## Overview

An **Activity** in Android is a single screen with a user interface, and it represents one key component of an Android app. The **Activity Lifecycle** defines the states or stages an Activity goes through during its lifecycle, from creation to destruction. These lifecycle stages are important for managing app resources efficiently and ensuring smooth user experiences.

### What is the Activity Lifecycle?

The Activity Lifecycle consists of several stages that an Activity moves through as it’s created, paused, resumed, and destroyed. Managing these states is essential to properly handle user interactions, memory management, and app behavior across different configurations (e.g., device rotations).

### Why is the Activity Lifecycle important?

- **Resource Management**: Ensure that resources (like CPU, memory) are efficiently managed. For example, an app should release heavy resources when the activity is paused or stopped.
- **State Management**: Maintain the UI state and data when an activity is interrupted (e.g., phone calls, notifications).
- **User Experience**: Handle transitions smoothly between activities and states, improving overall app performance.

### How to Implement and Manage the Activity Lifecycle?

Android provides several **callback methods** that are triggered during the different lifecycle states of an activity. By overriding these methods, you can handle transitions between states effectively.

---

## Prebuilt Functions (Lifecycle Callback Methods)

### 1. **onCreate()**
- **Description**: Called when the activity is first created. This is where you should initialize your activity, inflate the UI, and set up any required resources.
- **Usage**: Initialize components, create UI, and restore saved instance state.
- **Code Example**:
  ```java
  @Override
  protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
      // Initialize your components here
  }
  ```

### 2. **onStart()**
- **Description**: Called when the activity is becoming visible to the user.
- **Usage**: Begin any visual effects or UI-related tasks.
- **Code Example**:
  ```java
  @Override
  protected void onStart() {
      super.onStart();
      // Activity is visible and about to start interacting
  }
  ```

### 3. **onResume()**
- **Description**: Called when the activity will start interacting with the user.
- **Usage**: Resume any paused activities (like playing video, animations) or start actions that require user interaction.
- **Code Example**:
  ```java
  @Override
  protected void onResume() {
      super.onResume();
      // Activity is interacting with the user
  }
  ```

### 4. **onPause()**
- **Description**: Called when the system is about to pause the activity, meaning the activity is still visible but partially obscured (e.g., a dialog appears).
- **Usage**: Pause ongoing actions, such as animations or media playback.
- **Code Example**:
  ```java
  @Override
  protected void onPause() {
      super.onPause();
      // Activity is partially obscured, pause animations
  }
  ```

### 5. **onStop()**
- **Description**: Called when the activity is no longer visible to the user.
- **Usage**: Stop heavy operations, save state, or release resources.
- **Code Example**:
  ```java
  @Override
  protected void onStop() {
      super.onStop();
      // Activity is no longer visible, release resources
  }
  ```

### 6. **onDestroy()**
- **Description**: Called before the activity is destroyed. The activity can be destroyed either by the user finishing it or by the system to save resources.
- **Usage**: Clean up all resources, terminate background tasks, and handle final shutdown.
- **Code Example**:
  ```java
  @Override
  protected void onDestroy() {
      super.onDestroy();
      // Cleanup resources
  }
  ```

### 7. **onRestart()**
- **Description**: Called when the activity is stopped and then started again.
- **Usage**: Refresh resources or UI components.
- **Code Example**:
  ```java
  @Override
  protected void onRestart() {
      super.onRestart();
      // Activity is restarting after being stopped
  }
  ```

### 8. **onSaveInstanceState()**
- **Description**: Called to save the current state of the activity before it's stopped.
- **Usage**: Store UI-related data to restore later.
- **Code Example**:
  ```java
  @Override
  protected void onSaveInstanceState(Bundle outState) {
      super.onSaveInstanceState(outState);
      // Save UI state changes to the outState
      outState.putString("USER_INPUT", userInput);
  }
  ```

### 9. **onRestoreInstanceState()**
- **Description**: Called when the activity is being recreated after it was previously destroyed, and there is saved state to restore.
- **Usage**: Retrieve the UI state saved by `onSaveInstanceState`.
- **Code Example**:
  ```java
  @Override
  protected void onRestoreInstanceState(Bundle savedInstanceState) {
      super.onRestoreInstanceState(savedInstanceState);
      // Restore saved UI state
      String userInput = savedInstanceState.getString("USER_INPUT");
  }
  ```

---

## Prebuilt Classes

### 1. **Activity**
- **Description**: The base class for all activities in Android. Every screen of your app is typically a subclass of `Activity`.
- **Usage**: Extend this class to create a new screen in your app.
- **Code Example**:
  ```java
  public class MainActivity extends Activity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
      }
  }
  ```

### 2. **FragmentActivity**
- **Description**: A subclass of `Activity` that supports `Fragment` management.
- **Usage**: Use this when your activity needs to manage fragments.
- **Code Example**:
  ```java
  public class MyFragmentActivity extends FragmentActivity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_fragment);
      }
  }
  ```

---

## Related Android Concepts

### 1. **Fragment Lifecycle**
- Fragments have their own lifecycle, which is tightly integrated with the Activity lifecycle. Similar callback methods exist for fragments like `onCreateView()`, `onDestroyView()`, `onAttach()`, and `onDetach()`.
  
### 2. **ViewModel and LiveData**
- Manage UI-related data in a lifecycle-conscious way using `ViewModel` and `LiveData`. This helps to decouple UI and data logic, making sure that data is retained even when the activity is recreated (e.g., during screen rotation).

### 3. **Configuration Changes**
- When a configuration change (like screen orientation) happens, the activity is destroyed and recreated. You can handle these configuration changes by managing the activity lifecycle effectively.

### 4. **Lifecycle-Aware Components**
- Use `LifecycleObserver` and `LifecycleOwner` to create components that automatically adjust their behavior based on the lifecycle of the activity or fragment. This helps prevent memory leaks and crashes by properly managing lifecycle transitions.

### 5. **Intent and Activity Result**
- Use `Intent` to start new activities, and manage activity results using `startActivityForResult()` (deprecated) or `ActivityResultLauncher` (modern approach using `ActivityResultContracts`).

---

## Real-Life Example

Let’s say you are developing an app that tracks user fitness data (e.g., steps taken, calories burned). To save battery and optimize performance, you may want to stop tracking data when the app goes into the background.

```java
public class FitnessActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_fitness);
        // Initialize tracking services
    }

    @Override
    protected void onResume() {
        super.onResume();
        // Resume step counting
    }

    @Override
    protected void onPause() {
        super.onPause();
        // Pause step counting to save battery
    }

    @Override
    protected void onStop() {
        super.onStop();
        // Stop tracking completely
    }
}
```

---

## Summary

The **Activity Lifecycle** is fundamental for creating efficient, well-functioning Android applications. Managing activity states effectively ensures that your app uses resources optimally and provides a smooth user experience. By handling lifecycle events, you can maintain data consistency, manage resources, and create more flexible apps that adapt to different scenarios.
