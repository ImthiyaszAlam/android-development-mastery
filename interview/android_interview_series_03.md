Here are **10 more advanced Android interview questions and answers** to help you crack the interview:  

---

## **📌 21. What are the different launch modes in Android Activities?**
✅ **Answer:**  
Android provides **four launch modes** to control how activities are created and reused:  

| **Launch Mode** | **Behavior** |
|---------------|-------------|
| **standard** | Creates a new instance every time |
| **singleTop** | Reuses existing instance if it's already at the top of the stack |
| **singleTask** | Reuses existing instance if available, otherwise creates a new one in a new task |
| **singleInstance** | Creates a separate task with a single instance |

📝 **Example Usage in Manifest:**  
```xml
<activity android:name=".MyActivity"
    android:launchMode="singleTask"/>
```
👉 **Tip:** Use **singleTask** when you want only one instance of an activity across the app.

---

## **📌 22. What is the difference between Parcelable and Serializable?**
✅ **Answer:**  
| Feature | Parcelable | Serializable |
|---------|------------|-------------|
| Speed | Fast | Slow |
| Memory Usage | Less | More |
| Implementation | Manual (Boilerplate) | Automatic (Java Reflection) |

📝 **Example Usage (Parcelable):**  
```kotlin
@Parcelize
data class User(val name: String, val age: Int) : Parcelable
```
👉 **Tip:** Use **Parcelable** instead of Serializable for **better performance**.

---

## **📌 23. What is the difference between Local, Unbounded, and Shared WorkManager?**
✅ **Answer:**  
| WorkManager Type | Description |
|-----------------|-------------|
| **Local WorkManager** | Work is only accessible within the app |
| **Unbounded WorkManager** | Work can be accessed across app instances |
| **Shared WorkManager** | Shared between multiple processes |

👉 **Tip:** Use **Local WorkManager** for most background tasks unless multi-process support is needed.

---

## **📌 24. How do you handle memory leaks in Android?**
✅ **Answer:**  
✔ Use **WeakReference** for context in long-running tasks  
✔ Avoid **static references** to Activities or Views  
✔ Use **Lifecycle-aware components**  
✔ Use **LeakCanary** to detect leaks  

📝 **Example (Using WeakReference):**  
```kotlin
class MyTask(context: Context) {
    private val contextRef = WeakReference(context)

    fun doSomething() {
        contextRef.get()?.let {
            // Safe to use context here
        }
    }
}
```
👉 **Tip:** **Use LeakCanary** to identify memory leaks.

---

## **📌 25. What is the difference between `LiveData` and `StateFlow`?**
✅ **Answer:**  
| Feature | LiveData | StateFlow |
|---------|---------|-----------|
| Observers | Multiple | Single |
| Requires LifecycleOwner? | Yes | No |
| Retains Latest Value? | Yes | Yes |
| Thread Safety | Main Thread Only | Thread-safe |

📝 **Example Usage (StateFlow):**  
```kotlin
class MyViewModel : ViewModel() {
    private val _state = MutableStateFlow("Hello")
    val state: StateFlow<String> = _state
}
```
👉 **Tip:** Use **LiveData** for UI-related state and **StateFlow** for business logic.

---

## **📌 26. How do you implement Pagination in Android?**
✅ **Answer:**  
Use **Paging 3 Library** for efficient pagination.  

📝 **Example (Paging 3 Implementation):**  
```kotlin
class MyPagingSource : PagingSource<Int, Data>() {
    override suspend fun load(params: LoadParams<Int>): LoadResult<Int, Data> {
        val page = params.key ?: 1
        val response = api.getData(page)
        return LoadResult.Page(
            data = response.items,
            prevKey = if (page == 1) null else page - 1,
            nextKey = if (response.hasNext) page + 1 else null
        )
    }
}
```
👉 **Tip:** Use **RemoteMediator** for caching data with Room.

---

## **📌 27. What are Jetpack Navigation Components, and how do they work?**
✅ **Answer:**  
Jetpack **Navigation Component** simplifies fragment navigation using a navigation graph.

📝 **Example (Navigation Graph in XML):**  
```xml
<fragment
    android:id="@+id/homeFragment"
    android:name="com.example.HomeFragment">
    <action
        android:id="@+id/action_home_to_details"
        app:destination="@id/detailsFragment"/>
</fragment>
```
👉 **Tip:** Use `NavController.navigate(R.id.action_home_to_details)` to navigate between fragments.

---

## **📌 28. What is the difference between Hilt and Dagger?**
✅ **Answer:**  
| Feature | Dagger | Hilt |
|---------|-------|------|
| Manual Boilerplate | More | Less |
| Android Integration | Complex | Simplified |
| Performance | High | High |
| Used For | Large projects | Android apps |

📝 **Example (Hilt ViewModel Injection):**  
```kotlin
@HiltViewModel
class MyViewModel @Inject constructor(
    private val repository: MyRepository
) : ViewModel() {
    fun fetchData() = repository.getData()
}
```
👉 **Tip:** Use **Hilt** for Dependency Injection in modern Android apps.

---

## **📌 29. How does WorkManager differ from JobScheduler?**
✅ **Answer:**  
| Feature | WorkManager | JobScheduler |
|---------|------------|-------------|
| API Level Support | API 14+ | API 21+ |
| Guaranteed Execution? | Yes | No |
| Works with Constraints? | Yes | Yes |

📝 **Example (WorkManager with Constraints):**  
```kotlin
val constraints = Constraints.Builder()
    .setRequiredNetworkType(NetworkType.CONNECTED)
    .build()

val workRequest = OneTimeWorkRequestBuilder<MyWorker>()
    .setConstraints(constraints)
    .build()

WorkManager.getInstance(context).enqueue(workRequest)
```
👉 **Tip:** Use **WorkManager** instead of JobScheduler for **backward compatibility**.

---

## **📌 30. How do you secure an Android app from reverse engineering?**
✅ **Answer:**  
✔ Enable **ProGuard** to obfuscate code  
✔ Use **NDK (Native C++)** for sensitive logic  
✔ Use **Secure SharedPreferences** for storing credentials  
✔ **Encrypt API Keys** using the Android Keystore  

📝 **Example (ProGuard Configuration in `proguard-rules.pro`):**  
```
-keep class com.example.app.** { *; }
-keepclassmembers class * {
    @android.webkit.JavascriptInterface <methods>;
}
```
👉 **Tip:** Use **Google Play App Signing** for extra security.

---

## **🔥 Final Tips to Crack the Interview**
✅ **Practice hands-on coding** with real-world problems  
✅ **Understand Android internals** (Activity lifecycle, memory management)  
✅ **Use Jetpack Libraries** (Navigation, Paging, WorkManager, Hilt)  
✅ **Showcase projects** that use modern Android practices  

---

Let me know if you need **coding challenges or system design questions**! 🚀
