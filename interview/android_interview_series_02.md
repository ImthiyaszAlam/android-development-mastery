Here are **10 more advanced Android interview questions and answers** to help you crack the interview:  

---

## **📌 11. What is the difference between MVVM, MVP, and MVC?**
✅ **Answer:**  
| Feature | MVC | MVP | MVVM |
|---------|-----|-----|------|
| Separation of Concerns | Low | Medium | High |
| Testability | Low | Medium | High |
| Data Binding Support | No | No | Yes |
| Used In | Legacy Android | Older Android Apps | Modern Android Apps |

📝 **MVVM Example:**  
```kotlin
class MyViewModel : ViewModel() {
    val data = MutableLiveData<String>()

    fun fetchData() {
        data.value = "Hello, MVVM!"
    }
}
```
👉 **Tip:** **MVVM** is preferred in modern Android apps due to **better separation of concerns**.

---

## **📌 12. What are Coroutines Scopes, and how do they work?**
✅ **Answer:**  
Coroutines scopes define **where and how long coroutines will run**.  

✔ **GlobalScope** – Runs throughout the app lifecycle  
✔ **ViewModelScope** – Runs until ViewModel is cleared  
✔ **LifecycleScope** – Tied to the UI lifecycle  

📝 **Example Usage:**  
```kotlin
class MyViewModel : ViewModel() {
    fun fetchData() {
        viewModelScope.launch {
            val result = async { getDataFromApi() }.await()
            println(result)
        }
    }
}
```
👉 **Tip:** Use **ViewModelScope** for UI-related tasks and **GlobalScope** for long-running background tasks.

---

## **📌 13. What is the difference between MutableStateFlow and SharedFlow?**
✅ **Answer:**  
| Feature | MutableStateFlow | SharedFlow |
|---------|-----------------|------------|
| Stores the latest value | Yes | No |
| Default replay behavior | Always holds a value | Can replay n values |
| Used for | UI State | Events (e.g., navigation) |

📝 **Example Usage:**  
```kotlin
val stateFlow = MutableStateFlow("Initial State")
val sharedFlow = MutableSharedFlow<String>(replay = 1)
```
👉 **Tip:** Use **StateFlow** for UI updates and **SharedFlow** for one-time events.

---

## **📌 14. How does ViewBinding differ from DataBinding?**
✅ **Answer:**  
| Feature | ViewBinding | DataBinding |
|---------|------------|------------|
| Performance | Faster | Slightly slower |
| Binding Expressions | No | Yes (Supports expressions) |
| Requires XML Changes | No | Yes (Uses `<layout>` tag) |

📝 **Example Usage:**  
```kotlin
val binding = ActivityMainBinding.inflate(layoutInflater)
setContentView(binding.root)
binding.textView.text = "Hello, ViewBinding!"
```
👉 **Tip:** Use **ViewBinding** for better performance unless you need **DataBinding expressions**.

---

## **📌 15. How does Jetpack Compose differ from XML-based UI?**
✅ **Answer:**  
✔ Jetpack Compose is a **declarative UI framework**  
✔ Reduces **boilerplate code**  
✔ Uses **Kotlin functions instead of XML layouts**  

📝 **Example Usage:**  
```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```
👉 **Tip:** Use **Jetpack Compose** for **modern Android UI development**.

---

## **📌 16. How do you implement offline caching in Retrofit?**
✅ **Answer:**  
Use **OkHttp Interceptors** to cache responses.  

📝 **Example Usage:**  
```kotlin
val cache = Cache(File(context.cacheDir, "http_cache"), 10 * 1024 * 1024) // 10MB Cache

val okHttpClient = OkHttpClient.Builder()
    .cache(cache)
    .addInterceptor { chain ->
        var request = chain.request()
        request = if (hasNetwork()) request.newBuilder()
            .header("Cache-Control", "public, max-age=5").build()
        else request.newBuilder()
            .header("Cache-Control", "public, only-if-cached, max-stale=604800").build()
        chain.proceed(request)
    }.build()
```
👉 **Tip:** Cache API responses for **offline access**.

---

## **📌 17. What are BroadcastReceivers, and how do they work?**
✅ **Answer:**  
A **BroadcastReceiver** listens for system-wide events (e.g., battery low, network changes).  

📝 **Example Usage:**  
```kotlin
class MyReceiver : BroadcastReceiver() {
    override fun onReceive(context: Context, intent: Intent) {
        println("Broadcast received!")
    }
}

// Register Receiver in AndroidManifest.xml
<receiver android:name=".MyReceiver">
    <intent-filter>
        <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
    </intent-filter>
</receiver>
```
👉 **Tip:** Use **LocalBroadcastManager** to avoid security issues.

---

## **📌 18. How do you optimize RecyclerView performance?**
✅ **Answer:**  
✔ Use **ViewHolder pattern**  
✔ Use **DiffUtil** for list updates  
✔ Use **setHasFixedSize(true)** for static lists  
✔ Use **RecycledViewPool** for better view reuse  

📝 **Example Usage:**  
```kotlin
val diffCallback = object : DiffUtil.ItemCallback<MyItem>() {
    override fun areItemsTheSame(old: MyItem, new: MyItem) = old.id == new.id
    override fun areContentsTheSame(old: MyItem, new: MyItem) = old == new
}
val adapter = ListAdapter(diffCallback)
```
👉 **Tip:** Use **ListAdapter** instead of regular RecyclerView adapters for performance.

---

## **📌 19. How does WorkManager handle constraints like network availability?**
✅ **Answer:**  
WorkManager lets you define constraints using `Constraints.Builder()`.  

📝 **Example Usage:**  
```kotlin
val constraints = Constraints.Builder()
    .setRequiredNetworkType(NetworkType.CONNECTED)
    .setRequiresCharging(true)
    .build()

val workRequest = OneTimeWorkRequestBuilder<MyWorker>()
    .setConstraints(constraints)
    .build()

WorkManager.getInstance(context).enqueue(workRequest)
```
👉 **Tip:** Use WorkManager when **jobs need constraints** (e.g., run only on Wi-Fi).

---

## **📌 20. How do you handle deep linking in Android?**
✅ **Answer:**  
Deep linking allows an app to be **opened via a URL**.  

✔ **Explicit Deep Linking:** Uses Intent filters  
✔ **App Links:** Uses Digital Asset Links  
✔ **Firebase Dynamic Links:** Supports deferred deep linking  

📝 **Example Usage:**  
```xml
<intent-filter>
    <action android:name="android.intent.action.VIEW"/>
    <category android:name="android.intent.category.DEFAULT"/>
    <category android:name="android.intent.category.BROWSABLE"/>
    <data android:scheme="https" android:host="www.example.com" android:pathPrefix="/product"/>
</intent-filter>
```
👉 **Tip:** Use **Firebase Dynamic Links** for better cross-platform deep linking.

---

## **🔥 Final Tips to Crack the Interview**
✅ **Practice coding problems** related to **multi-threading, UI optimizations, and APIs**  
✅ **Understand the lifecycle** of components (Activity, Fragment, ViewModel)  
✅ **Know Jetpack libraries** like WorkManager, Paging, DataStore, Navigation  
✅ **Prepare real-world examples** from your projects  
✅ **Ask questions** to the interviewer  

---

Let me know if you need **coding challenges or DSA questions**! 🚀
