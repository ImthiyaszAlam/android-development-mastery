

## **📌 1. What is the difference between LiveData and StateFlow?**
✅ **Answer:**  
| Feature | LiveData | StateFlow |
|---------|---------|-----------|
| Lifecycle-aware | Yes | No |
| Hot/Cold | Cold (Emits only when active) | Hot (Always active) |
| State retention | Keeps only the latest value | Always holds state |
| Use case | UI updates (Activity/Fragment) | Background data streams |

📝 **Example Usage:**  
```kotlin
val liveData = MutableLiveData<String>()  // LiveData
val stateFlow = MutableStateFlow("Initial")  // StateFlow
```
👉 **Tip:** Use **LiveData** for UI-bound data and **StateFlow** for business logic.

---

## **📌 2. What is the difference between Parcelable and Serializable?**
✅ **Answer:**  
| Feature | Parcelable | Serializable |
|---------|------------|-------------|
| Performance | Faster | Slower |
| Implementation | Manual (writeToParcel, createFromParcel) | Automatic |
| Use case | Android-specific | General Java serialization |

📝 **Example:**  
```kotlin
@Parcelize
data class User(val id: Int, val name: String) : Parcelable
```
👉 **Tip:** Always use **Parcelable** in Android as it’s optimized.

---

## **📌 3. How does WorkManager work, and when should you use it?**
✅ **Answer:**  
**WorkManager** is used for scheduling background tasks that must be executed **even if the app is closed**.

✔ Uses **JobScheduler, AlarmManager, BroadcastReceiver** internally  
✔ Ensures **guaranteed execution** of tasks  

📝 **Example Usage:**  
```kotlin
val workRequest = OneTimeWorkRequestBuilder<MyWorker>().build()
WorkManager.getInstance(context).enqueue(workRequest)
```
👉 **Tip:** Use **WorkManager** for long-running background tasks like **data syncing**.

---

## **📌 4. What are the different types of Services in Android?**
✅ **Answer:**  
1. **Foreground Service** – Runs in the foreground with a **notification** (e.g., music player).  
2. **Background Service** – Runs in the background without user interaction.  
3. **Bound Service** – Allows **communication** between components (e.g., Messenger service).  

📝 **Example Usage:**  
```kotlin
class MyService : Service() {
    override fun onStartCommand(intent: Intent, flags: Int, startId: Int): Int {
        return START_STICKY
    }
}
```
👉 **Tip:** Use **Foreground Service** for **long-running tasks** (e.g., Location tracking).

---

## **📌 5. What is the difference between launch and async in Coroutines?**
✅ **Answer:**  
| Feature | launch | async |
|---------|--------|-------|
| Returns | `Job` (no result) | `Deferred<T>` (returns result) |
| Use case | Fire-and-forget tasks | Tasks that return a value |
| Exception Handling | Throws exceptions | Must use `await()` |

📝 **Example Usage:**  
```kotlin
// launch (No result needed)
GlobalScope.launch {
    delay(1000)
    println("Task finished")
}

// async (Returns result)
val result = async { fetchData() }.await()
```
👉 **Tip:** Use **async** when you need a return value, otherwise use **launch**.

---

## **📌 6. What is Dependency Injection, and why is Hilt recommended?**
✅ **Answer:**  
**Dependency Injection (DI)** helps manage dependencies efficiently.  
✔ **Hilt** is recommended because:  
✔ Simplifies DI in Android  
✔ Reduces boilerplate code  
✔ Works with ViewModel  

📝 **Example Usage:**  
```kotlin
@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    fun provideRetrofit(): Retrofit = Retrofit.Builder()
        .baseUrl("https://api.example.com")
        .build()
}
```
👉 **Tip:** Hilt is built on **Dagger**, making DI easier in Android.

---

## **📌 7. What is Paging 3, and why is it useful?**
✅ **Answer:**  
**Paging 3** is a Jetpack library for **efficiently loading large data sets** in chunks.  
✔ Reduces memory usage  
✔ Supports **Room, Retrofit, and Coroutines**  
✔ Provides **automatic data refresh**  

📝 **Example Usage:**  
```kotlin
val pagingSource = object : PagingSource<Int, User>() { 
    override suspend fun load(params: LoadParams<Int>): LoadResult<Int, User> {
        return LoadResult.Page(data = getUsersFromApi(), prevKey = null, nextKey = 2)
    }
}
```
👉 **Tip:** Use **Paging 3** for **infinite scrolling lists**.

---

## **📌 8. What is ProGuard, and why is it used?**
✅ **Answer:**  
**ProGuard** is a tool for:  
✔ **Shrinking** (removes unused code)  
✔ **Obfuscation** (renames classes & methods)  
✔ **Optimization** (improves performance)  

📝 **Example ProGuard Rules:**  
```pro
-keep class com.example.MyClass { *; }
-dontwarn okhttp3.**
```
👉 **Tip:** Use ProGuard to **reduce APK size** and **protect source code**.

---

## **📌 9. How do you handle memory leaks in Android?**
✅ **Answer:**  
✔ **Avoid strong references** to Activities in long-running tasks  
✔ Use **WeakReferences** where necessary  
✔ Use **Lifecycle-aware components**  
✔ Detect leaks using **LeakCanary**  

📝 **Example:**  
```kotlin
val contextRef = WeakReference(context)
contextRef.get()?.let { safeContext ->
    // Use safeContext here
}
```
👉 **Tip:** Always unregister listeners & close database connections to avoid leaks.

---

## **📌 10. What is the difference between SharedPreferences and DataStore?**
✅ **Answer:**  
| Feature | SharedPreferences | DataStore |
|---------|------------------|----------|
| Storage Type | XML File | Jetpack DataStore |
| Performance | Slower | Faster (Uses Kotlin Coroutines) |
| Type Safety | Not type-safe | Type-safe |

📝 **Example Usage:**  
```kotlin
val dataStore = context.createDataStore(name = "settings")
val USERNAME_KEY = preferencesKey<String>("username")

suspend fun saveUserName(name: String) {
    dataStore.edit { it[USERNAME_KEY] = name }
}
```
👉 **Tip:** **Use DataStore** instead of SharedPreferences for **better performance**.

---

## **🔥 Final Tips to Crack the Interview**
✅ **Be confident** while explaining concepts  
✅ **Use real-life examples** from your past projects  
✅ **Showcase your problem-solving skills**  
✅ **Prepare a few questions** to ask the interviewer  

Let me know if you need **coding questions** or **system design concepts**! 🚀
