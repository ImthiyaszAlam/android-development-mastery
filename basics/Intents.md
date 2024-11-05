# Intents in Android

## What

An **Intent** in Android is a messaging object used to request an action from another application component. Intents can be used to start activities, send broadcasts, start services, and more.

## Why

- **Inter-Component Communication:** Intents allow different components (activities, services, broadcast receivers) within an application or across applications to communicate with each other.
- **Flexibility:** They provide a flexible mechanism to perform tasks and pass data between components.
- **Decoupling:** Intents help in decoupling components, which makes your app more modular and easier to maintain.

## How

1. **Creating an Intent:** You create an intent to perform a specific action, such as starting an activity or sending a broadcast.
2. **Specifying the Action:** Define the action you want to perform (e.g., opening a new activity, starting a service).
3. **Starting the Component:** Use the `startActivity()`, `startService()`, or `sendBroadcast()` methods to execute the action defined by the intent.

## Prebuilt Classes and Interfaces

### 1. **Intent**
- **Description:** The main class used to create and manage intents. It allows you to specify the action and data associated with the intent.
- **Usage:** Use this class to create and configure intents for various purposes.
- **Code Example:**
  ```java
  Intent intent = new Intent(context, NewActivity.class);
  intent.putExtra("key", "value");
  startActivity(intent);
  ```

### 2. **PendingIntent**
- **Description:** A token that you give to a foreign application (e.g., a notification manager or alarm manager), which allows the foreign application to execute the specified intent.
- **Usage:** Use this class for cases where you need to execute an intent later, such as in notifications or alarms.
- **Code Example:**
  ```java
  Intent intent = new Intent(context, BroadcastReceiver.class);
  PendingIntent pendingIntent = PendingIntent.getBroadcast(context, 0, intent, 0);
  ```

### 3. **BroadcastReceiver**
- **Description:** A class used to listen for and respond to broadcast messages from other applications or from the system.
- **Usage:** Implement this class to handle broadcasted intents.
- **Code Example:**
  ```java
  public class MyReceiver extends BroadcastReceiver {
      @Override
      public void onReceive(Context context, Intent intent) {
          // Handle the broadcast
      }
  }
  ```

### 4. **Service**
- **Description:** A component that performs operations in the background and does not provide a user interface.
- **Usage:** Start or bind to a service using intents to perform background operations.
- **Code Example:**
  ```java
  Intent intent = new Intent(context, MyService.class);
  context.startService(intent);
  ```

### 5. **Activity**
- **Description:** A component that provides a user interface for interacting with the user.
- **Usage:** Start a new activity or switch between activities using intents.
- **Code Example:**
  ```java
  Intent intent = new Intent(context, AnotherActivity.class);
  startActivity(intent);
  ```

## Key Methods

### **startActivity(Intent intent)**
- **Description:** Starts a new activity.
- **Usage:** Use this method to launch a new activity from an existing activity.
- **Code Example:** See `Activity` example above.

### **startService(Intent intent)**
- **Description:** Starts a service.
- **Usage:** Use this method to start a service that performs background operations.
- **Code Example:** See `Service` example above.

### **sendBroadcast(Intent intent)**
- **Description:** Sends a broadcast to all interested broadcast receivers.
- **Usage:** Use this method to send a broadcast message.
- **Code Example:**
  ```java
  Intent intent = new Intent("com.example.ACTION");
  sendBroadcast(intent);
  ```

### **registerReceiver(BroadcastReceiver receiver, IntentFilter filter)**
- **Description:** Registers a broadcast receiver to listen for specific intents.
- **Usage:** Use this method to start listening for broadcast messages.
- **Code Example:**
  ```java
  IntentFilter filter = new IntentFilter("com.example.ACTION");
  BroadcastReceiver receiver = new MyReceiver();
  registerReceiver(receiver, filter);
  ```

### **PendingIntent.getBroadcast(Context context, int requestCode, Intent intent, int flags)**
- **Description:** Creates a PendingIntent that will perform a broadcast.
- **Usage:** Use this method for pending intents that perform broadcast actions.
- **Code Example:** See `PendingIntent` example above.

## Real-Life Examples

1. **Starting a New Activity:**
   - Use intents to navigate from one screen to another in your app.

   **Code Example:**
   ```java
   Intent intent = new Intent(CurrentActivity.this, NewActivity.class);
   intent.putExtra("data", "value");
   startActivity(intent);
   ```

2. **Sending a Broadcast:**
   - Send a broadcast to notify other parts of your app or other apps about a specific event.

   **Code Example:**
   ```java
   Intent intent = new Intent("com.example.ACTION");
   intent.putExtra("key", "value");
   sendBroadcast(intent);
   ```

3. **Starting a Service:**
   - Start a service to perform background tasks even when the user is not interacting with your app.

   **Code Example:**
   ```java
   Intent intent = new Intent(context, MyService.class);
   context.startService(intent);
   ```

4. **Pending Intents for Notifications:**
   - Use pending intents to trigger actions when a notification is tapped.

   **Code Example:**
   ```java
   Intent intent = new Intent(context, NotificationReceiver.class);
   PendingIntent pendingIntent = PendingIntent.getBroadcast(context, 0, intent, 0);
   NotificationCompat.Builder builder = new NotificationCompat.Builder(context, CHANNEL_ID)
           .setContentTitle("Title")
           .setContentText("Text")
           .setContentIntent(pendingIntent)
           .setAutoCancel(true);
   ```

## Summary

Intents are a fundamental component of Android that facilitate communication between different parts of an application or between different applications. They provide a flexible mechanism for starting activities, services, and broadcasting messages, allowing for a wide range of interactions and operations within Android apps.
