# Call in Android

## Overview

In Android, making phone calls, managing call logs, and handling call states can be done using various classes and APIs. You can:
- Make outgoing calls programmatically.
- Access call logs (incoming, outgoing, and missed).
- Track the state of a call (ringing, off-hook, idle).
  
This functionality requires appropriate permissions to be set in your app.

## Permissions

Before working with calls, you need to add permissions in the `AndroidManifest.xml`:
```xml
<uses-permission android:name="android.permission.CALL_PHONE" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

## Prebuilt Classes and Methods

### 1. **Intent (CALL Intent)**
- **Description:** You can use `Intent.ACTION_CALL` or `Intent.ACTION_DIAL` to initiate a phone call.
  - `ACTION_DIAL`: Opens the dialer without making the call.
  - `ACTION_CALL`: Makes a direct call.
  
- **Usage:**
  ```java
  Intent intent = new Intent(Intent.ACTION_DIAL);
  intent.setData(Uri.parse("tel:" + phoneNumber));
  startActivity(intent);
  ```

  **Direct Call (ACTION_CALL)**:
  ```java
  Intent callIntent = new Intent(Intent.ACTION_CALL);
  callIntent.setData(Uri.parse("tel:" + phoneNumber));
  startActivity(callIntent);
  ```

### 2. **TelephonyManager**
- **Description:** Provides access to information about the telephony services on the device. It allows you to monitor call states.
- **Usage:** Use `TelephonyManager` to get details about the phone network and call states.
  
- **Methods:**
  - **getCallState()**: Returns the state of all phone calls on the device (e.g., ringing, off-hook, or idle).
  - **getLine1Number()**: Returns the phone number string for the device's primary line.
  - **getNetworkOperatorName()**: Returns the name of the network operator.

  **Code Example:**
  ```java
  TelephonyManager telephonyManager = (TelephonyManager) getSystemService(Context.TELEPHONY_SERVICE);
  int callState = telephonyManager.getCallState();
  ```

### 3. **PhoneStateListener**
- **Description:** A listener class that monitors changes in the device’s call state and data connection state.
- **Usage:** Extend this class to handle events like call state changes (e.g., ringing, off-hook).

- **Code Example:**
  ```java
  PhoneStateListener listener = new PhoneStateListener() {
      @Override
      public void onCallStateChanged(int state, String phoneNumber) {
          switch (state) {
              case TelephonyManager.CALL_STATE_IDLE:
                  // Call ended or no call
                  break;
              case TelephonyManager.CALL_STATE_RINGING:
                  // Incoming call is ringing
                  break;
              case TelephonyManager.CALL_STATE_OFFHOOK:
                  // Call is picked up
                  break;
          }
      }
  };
  telephonyManager.listen(listener, PhoneStateListener.LISTEN_CALL_STATE);
  ```

### 4. **CallLog**
- **Description:** Provides access to the call log database, which contains information about incoming, outgoing, and missed calls.
- **Usage:** Use the `CallLog.Calls` class to retrieve the details of the call history.

- **Code Example to Retrieve Call Logs:**
  ```java
  Cursor cursor = getContentResolver().query(CallLog.Calls.CONTENT_URI, null, null, null, null);
  while (cursor.moveToNext()) {
      String number = cursor.getString(cursor.getColumnIndex(CallLog.Calls.NUMBER));
      String type = cursor.getString(cursor.getColumnIndex(CallLog.Calls.TYPE));
      String date = cursor.getString(cursor.getColumnIndex(CallLog.Calls.DATE));
      String duration = cursor.getString(cursor.getColumnIndex(CallLog.Calls.DURATION));

      // Type of call: Incoming, Outgoing, or Missed
      int callType = Integer.parseInt(type);
      switch (callType) {
          case CallLog.Calls.OUTGOING_TYPE:
              // Outgoing call
              break;
          case CallLog.Calls.INCOMING_TYPE:
              // Incoming call
              break;
          case CallLog.Calls.MISSED_TYPE:
              // Missed call
              break;
      }
  }
  ```

### 5. **CallLog.Calls (Columns)**

- **Description:** Key columns used to access call details from the `CallLog.Calls` table.
- **Common Columns:**
  - `NUMBER`: The phone number.
  - `TYPE`: The type of call (incoming, outgoing, missed).
  - `DATE`: The date of the call.
  - `DURATION`: The duration of the call.

### 6. **ContentResolver**
- **Description:** Used to access data from content providers like Call Logs.
- **Usage:** With `ContentResolver`, you can query the call logs or any other system data, such as contacts.

- **Code Example:**
  ```java
  Cursor cursor = getContentResolver().query(CallLog.Calls.CONTENT_URI, null, null, null, null);
  ```

## Real-Life Examples

### 1. **Initiating a Phone Call:**
   You want your app to dial a phone number or call a customer directly.

   **Example:**
   ```java
   Intent intent = new Intent(Intent.ACTION_CALL);
   intent.setData(Uri.parse("tel:" + phoneNumber));
   startActivity(intent);
   ```

### 2. **Retrieving Call History:**
   Your app needs to display a list of recent calls (incoming, outgoing, and missed calls).

   **Example:**
   ```java
   Cursor cursor = getContentResolver().query(CallLog.Calls.CONTENT_URI, null, null, null, null);
   while (cursor.moveToNext()) {
       String number = cursor.getString(cursor.getColumnIndex(CallLog.Calls.NUMBER));
       String type = cursor.getString(cursor.getColumnIndex(CallLog.Calls.TYPE));
       String date = cursor.getString(cursor.getColumnIndex(CallLog.Calls.DATE));
       String duration = cursor.getString(cursor.getColumnIndex(CallLog.Calls.DURATION));
   }
   ```

### 3. **Monitoring Call State:**
   You want to perform a task when a call is received, such as pausing audio playback when a call comes in.

   **Example:**
   ```java
   PhoneStateListener listener = new PhoneStateListener() {
       @Override
       public void onCallStateChanged(int state, String phoneNumber) {
           if (state == TelephonyManager.CALL_STATE_RINGING) {
               // Pause audio playback
           } else if (state == TelephonyManager.CALL_STATE_IDLE) {
               // Resume audio playback
           }
       }
   };
   telephonyManager.listen(listener, PhoneStateListener.LISTEN_CALL_STATE);
   ```

## Summary

Handling calls in Android involves working with different classes like `Intent`, `TelephonyManager`, `PhoneStateListener`, and `CallLog`. These allow you to make calls, retrieve call logs, and monitor call states effectively. Permissions are crucial for accessing these features, and ensuring proper handling of permissions is key for app functionality.

---

### Category

This topic should be categorized as **Advanced** due to the complexity of managing call states, querying call logs, and handling system permissions for telephony functions.
