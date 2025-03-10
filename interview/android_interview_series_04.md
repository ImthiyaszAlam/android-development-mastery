

## **📌 31. What is ViewModel, and why is it used?**  
✅ **Answer:**  
A **ViewModel** is a lifecycle-aware component that stores UI-related data and survives configuration changes like screen rotations.  

### **Key Benefits:**  
✔ Prevents memory leaks  
✔ Survives configuration changes  
✔ Stores UI-related data efficiently  

📝 **Example Usage:**  
```kotlin
class MyViewModel : ViewModel() {
    private val _text = MutableLiveData("Hello ViewModel")
    val text: LiveData<String> = _text
}
```
👉 **Tip:** Use `viewModelScope` with `Coroutines` to handle background tasks.

---

## **📌 32. What is Coroutines, and how does it improve performance in Android?**  
✅ **Answer:**  
Coroutines are **lightweight, non-blocking** threads for performing asynchronous tasks in Android.  

### **Benefits:**  
✔ Avoids blocking the UI thread  
✔ Improves efficiency by using suspend functions  
✔ Works well with `LiveData` and `ViewModelScope`  

📝 **Example (Using Coroutines in ViewModel):**  
```kotlin
class MyViewModel : ViewModel() {
    fun fetchData() {
        viewModelScope.launch {
            val data = repository.getData()
            _liveData.postValue(data)
        }
    }
}
```
👉 **Tip:** Use `Dispatchers.IO` for background work and `Dispatchers.Main` for UI updates.

---

## **📌 33. What is the difference between Fragment and Activity?**  
✅ **Answer:**  
| Feature | Activity | Fragment |
|---------|---------|----------|
| Lifecycle | Independent | Dependent on Activity |
| UI Component | Full-screen UI | Part of an Activity |
| Navigation | Starts a new Activity | Replaces within an Activity |
| Flexibility | Less flexible | More reusable |

👉 **Tip:** Use **Fragments** for modular and flexible UI design.

---

## **📌 34. What are the different types of Broadcast Receivers?**  
✅ **Answer:**  
1️⃣ **Static Receiver:** Declared in `AndroidManifest.xml`, receives broadcasts even when the app is closed.  
2️⃣ **Dynamic Receiver:** Registered at runtime inside an Activity or Service.  

📝 **Example (Dynamic BroadcastReceiver):**  
```kotlin
val receiver = object : BroadcastReceiver() {
    override fun onReceive(context: Context?, intent: Intent?) {
        Log.d("Receiver", "Received Intent: ${intent?.action}")
    }
}

registerReceiver(receiver, IntentFilter(Intent.ACTION_BATTERY_LOW))
```
👉 **Tip:** Use **LocalBroadcastManager** for internal app broadcasts.

---

## **📌 35. What is the difference between implicit and explicit intents?**  
✅ **Answer:**  
| Type | Description | Example |
|------|------------|---------|
| **Implicit Intent** | Used to perform an action without specifying the component | Open a URL in a browser |
| **Explicit Intent** | Directly specifies the target component | Open a specific Activity |

📝 **Example (Implicit Intent to open a URL):**  
```kotlin
val intent = Intent(Intent.ACTION_VIEW, Uri.parse("https://www.google.com"))
startActivity(intent)
```
👉 **Tip:** Use **Explicit Intent** for navigating between Activities in your app.

---

## **📌 36. What is WorkManager, and when should you use it?**  
✅ **Answer:**  
`WorkManager` is used to schedule **background tasks** that must run reliably, even after the app is closed or the device restarts.  

### **Use Cases:**  
✔ Uploading logs to a server  
✔ Sending analytics data  
✔ Periodic background syncing  

📝 **Example (WorkManager OneTimeWorkRequest):**  
```kotlin
val workRequest = OneTimeWorkRequestBuilder<MyWorker>().build()
WorkManager.getInstance(context).enqueue(workRequest)
```
👉 **Tip:** Use `PeriodicWorkRequest` for recurring tasks.

---

## **📌 37. How does Data Binding work in Android?**  
✅ **Answer:**  
Data Binding allows UI components to **bind directly to data sources** without requiring `findViewById()`.  

### **Benefits:**  
✔ Reduces boilerplate code  
✔ Improves UI performance  
✔ Increases code maintainability  

📝 **Example Usage in XML:**  
```xml
<layout xmlns:android="http://schemas.android.com/apk/res/android">
    <data>
        <variable name="user" type="com.example.User"/>
    </data>
    <TextView android:text="@{user.name}" />
</layout>
```
👉 **Tip:** Enable Data Binding in `build.gradle` with `dataBinding { enabled = true }`.

---

## **📌 38. What are SharedPreferences, and how do you use them?**  
✅ **Answer:**  
`SharedPreferences` is used for storing **small amounts of key-value data** such as user settings and preferences.  

📝 **Example Usage:**  
```kotlin
val sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE)
val editor = sharedPreferences.edit()
editor.putString("username", "JohnDoe")
editor.apply()
```
👉 **Tip:** Use `EncryptedSharedPreferences` for storing sensitive data securely.

---

## **📌 39. What is the difference between Service and IntentService?**  
✅ **Answer:**  
| Feature | Service | IntentService |
|---------|---------|--------------|
| Thread | Runs on Main Thread | Runs on Background Thread |
| Stops Automatically? | No | Yes, after completing work |
| Use Case | Long-running tasks | Short background tasks |

📝 **Example (IntentService Usage):**  
```kotlin
class MyIntentService : IntentService("MyIntentService") {
    override fun onHandleIntent(intent: Intent?) {
        Log.d("IntentService", "Service Running")
    }
}
```
👉 **Tip:** Use **WorkManager** instead of IntentService for better background task handling.

---

## **📌 40. How do you handle configuration changes like screen rotation in Android?**  
✅ **Answer:**  
✔ Use **ViewModel** to retain data  
✔ Use `onSaveInstanceState()` to save UI state  
✔ Use `configChanges` in the manifest  

📝 **Example (Saving Data in ViewModel):**  
```kotlin
class MyViewModel : ViewModel() {
    val text = MutableLiveData<String>("Hello")
}
```

📝 **Example (Using configChanges in Manifest):**  
```xml
<activity
    android:name=".MainActivity"
    android:configChanges="orientation|screenSize"/>
```
👉 **Tip:** Use **Fragments with retainedInstance = true** for complex UI state handling.

---

## **🔥 Final Tips to Crack the Interview**
✅ **Prepare real-world coding challenges**  
✅ **Understand how Jetpack libraries improve app architecture**  
✅ **Know best practices for background tasks & performance optimization**  
✅ **Practice system design questions related to large-scale Android apps**  
