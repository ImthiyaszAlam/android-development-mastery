# Broadcast Receiver

## Overview

A **Broadcast Receiver** in Android allows apps to listen for system-wide or app-specific broadcasts. These broadcasts are messages or events that are sent when something significant happens (e.g., when the device battery is low or when the screen is turned on).

Broadcast Receivers can be declared in the manifest file or registered dynamically in the code.

## Prebuilt Classes

### 1. **BroadcastReceiver**
- **Description:** A base class for receiving broadcast intents. When a broadcast event occurs, the `onReceive()` method of the receiver is invoked.
- **Usage:** Extend this class to create your own receiver that handles the events you're interested in.
- **Code Example:**
  ```java
  public class MyBroadcastReceiver extends BroadcastReceiver {
      @Override
      public void onReceive(Context context, Intent intent) {
          String action = intent.getAction();
          if (Intent.ACTION_BATTERY_LOW.equals(action)) {
              // Handle battery low event
          }
      }
  }
  ```

### 2. **Intent**
- **Description:** The message object that is broadcasted. It contains details of the event or action that is taking place.
- **Usage:** An `Intent` is sent or received with specific actions or data.
- **Common Actions:**
  - `Intent.ACTION_BATTERY_LOW`
  - `Intent.ACTION_BOOT_COMPLETED`
  - `Intent.ACTION_AIRPLANE_MODE_CHANGED`

### 3. **PendingIntent**
- **Description:** A token that you give to another application to allow it to perform an action on your app’s behalf, such as sending a broadcast.
- **Usage:** Used when you need to send a broadcast at a specific time in the future.
- **Code Example:**
  ```java
  PendingIntent pendingIntent = PendingIntent.getBroadcast(context, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
  ```

## Prebuilt Methods

### **onReceive()**
- **Description:** This method is triggered when the BroadcastReceiver receives an intent broadcast. The logic for handling the broadcast goes inside this method.
- **Usage:** Every BroadcastReceiver must implement this method.
- **Code Example:**
  ```java
  @Override
  public void onReceive(Context context, Intent intent) {
      String action = intent.getAction();
      if (Intent.ACTION_AIRPLANE_MODE_CHANGED.equals(action)) {
          boolean isAirplaneModeOn = intent.getBooleanExtra("state", false);
          // Perform actions when airplane mode changes
      }
  }
  ```

### **registerReceiver()**
- **Description:** Registers a receiver dynamically in the code. The receiver starts listening when this method is called.
- **Usage:** Use this method when you only want to listen to broadcasts while the app is running.
- **Code Example:**
  ```java
  IntentFilter filter = new IntentFilter(Intent.ACTION_BATTERY_LOW);
  MyBroadcastReceiver receiver = new MyBroadcastReceiver();
  context.registerReceiver(receiver, filter);
  ```

### **unregisterReceiver()**
- **Description:** Unregisters a previously registered receiver.
- **Usage:** Always unregister a receiver when it's no longer needed, to avoid memory leaks.
- **Code Example:**
  ```java
  context.unregisterReceiver(receiver);
  ```

### **sendBroadcast()**
- **Description:** Sends a broadcast to any registered receivers.
- **Usage:** If your app wants to send its own broadcast, use this method.
- **Code Example:**
  ```java
  Intent intent = new Intent("com.example.MY_CUSTOM_ACTION");
  context.sendBroadcast(intent);
  ```

## Real-Life Examples

1. **Battery Low Notification:**
   - Your app can monitor battery status and show a notification when the battery is low by listening for the `ACTION_BATTERY_LOW` broadcast.

   **Code Example:**
   ```java
   public class BatteryLowReceiver extends BroadcastReceiver {
       @Override
       public void onReceive(Context context, Intent intent) {
           if (Intent.ACTION_BATTERY_LOW.equals(intent.getAction())) {
               // Notify the user that the battery is low
           }
       }
   }
   ```

   Register the receiver in the manifest:
   ```xml
   <receiver android:name=".BatteryLowReceiver">
       <intent-filter>
           <action android:name="android.intent.action.BATTERY_LOW"/>
       </intent-filter>
   </receiver>
   ```

2. **Connectivity Change:**
   - Monitor network connectivity changes in the app by using a Broadcast Receiver to listen for `android.net.conn.CONNECTIVITY_CHANGE`.

   **Code Example:**
   ```java
   public class ConnectivityReceiver extends BroadcastReceiver {
       @Override
       public void onReceive(Context context, Intent intent) {
           // Check connectivity status and handle accordingly
       }
   }
   ```

   Register dynamically in the activity:
   ```java
   IntentFilter filter = new IntentFilter(ConnectivityManager.CONNECTIVITY_ACTION);
   registerReceiver(new ConnectivityReceiver(), filter);
   ```

3. **Scheduled Tasks:**
   - Use `AlarmManager` to send a broadcast at a specific time using `PendingIntent`.

   **Code Example:**
   ```java
   AlarmManager alarmManager = (AlarmManager) getSystemService(ALARM_SERVICE);
   Intent intent = new Intent(context, MyBroadcastReceiver.class);
   PendingIntent pendingIntent = PendingIntent.getBroadcast(context, 0, intent, 0);
   alarmManager.setExact(AlarmManager.RTC_WAKEUP, triggerAtMillis, pendingIntent);
   ```

## Manifest Declaration

If you want your `BroadcastReceiver` to be triggered even when the app is not running, declare it in the `AndroidManifest.xml`:

```xml
<receiver android:name=".MyBroadcastReceiver">
    <intent-filter>
        <action android:name="android.intent.action.AIRPLANE_MODE"/>
    </intent-filter>
</receiver>
```

## Summary

Broadcast Receivers enable your app to respond to system-wide events like connectivity changes, battery status updates, and custom application events. They play a crucial role in interacting with the Android system's event-driven architecture.

---

### Category
Broadcast Receiver should be categorized as **Advanced**, as it requires a solid understanding of Android's event-driven system, lifecycle, and background processes.
