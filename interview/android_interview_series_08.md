

## **21. What are the different scopes in Kotlin Coroutines? When would you use each?**  

### **Answer:**  
Kotlin Coroutines have **four main scopes**, each suited for different use cases:  

| Scope            | Best for                     | Lifecycle |
|-----------------|-----------------------------|-----------|
| **GlobalScope** | Background tasks (rarely used) | Exists until app is killed |
| **viewModelScope** | UI-related tasks in ViewModel | Cancels when ViewModel is cleared |
| **lifecycleScope** | UI-bound tasks in Activity/Fragment | Cancels on Lifecycle event (e.g., onDestroy) |
| **CoroutineScope** | Custom scope (for libraries, custom logic) | User-defined |

**Example (Using `viewModelScope` in MVVM):**  
```kotlin
class MyViewModel : ViewModel() {
    fun fetchData() {
        viewModelScope.launch(Dispatchers.IO) {
            val data = api.getData()
            withContext(Dispatchers.Main) {
                updateUI(data)
            }
        }
    }
}
```

**Impact:**  
- **Prevents memory leaks** by canceling coroutines when the ViewModel is cleared.  

---

## **22. How does the Paging 3 library handle data loading states?**  

### **Answer:**  
Paging 3 provides **LoadState** objects for handling **loading, error, and retry states**.  

✅ **`LoadState.Loading`** – When data is being fetched  
✅ **`LoadState.Error`** – When API call fails  
✅ **`LoadState.NotLoading`** – When data is successfully loaded  

**Example Handling Loading State in RecyclerView:**  
```kotlin
adapter.addLoadStateListener { loadState ->
    when (loadState.refresh) {
        is LoadState.Loading -> showLoadingSpinner()
        is LoadState.NotLoading -> hideLoadingSpinner()
        is LoadState.Error -> showRetryButton()
    }
}
```

**Impact:**  
- **Improved UI experience** with proper state management.

---

## **23. How do you handle multi-module architecture in Android?**  

### **Answer:**  
At **Mela App**, I used **multi-module architecture** to improve scalability.  

✅ **Feature Modules** – Separate modules for independent features  
✅ **Core Module** – Shared utilities (networking, database, logging)  
✅ **App Module** – Handles dependency injection and app-wide configurations  

**Example Project Structure:**  
```
- app (Depends on feature and core modules)
- core (Networking, DB, Utilities)
- feature_auth (Authentication Module)
- feature_profile (User Profile Module)
```

**Impact:**  
- Reduced **build time by 30%**  
- Improved **code reusability and separation of concerns**

---

## **24. How would you optimize an Android app for low-memory devices?**  

### **Answer:**  
At **CloudSect**, I optimized an app for **low-memory devices** using:  

✅ **Use Jetpack Memory Profiler** – To identify memory leaks  
✅ **Avoid Bitmap Overuse** – Used Glide with `.diskCacheStrategy(DiskCacheStrategy.ALL)`  
✅ **Use ViewBinding instead of findViewById** – Reduced **view inflation time**  
✅ **Use WorkManager for Background Tasks** – Prevented unnecessary wakeups  

**Impact:**  
- Reduced **memory footprint by 40%**, improved **app stability**.

---

## **25. How does Firebase Authentication work?**  

### **Answer:**  
Firebase Authentication **simplifies user login with SDK-based authentication**.  

✅ Supports **Email/Password, Google, Facebook, Phone OTP**  
✅ Stores user info in **FirebaseAuth**  
✅ Provides **JWT-based authentication tokens**  

**Example Email Login:**  
```kotlin
FirebaseAuth.getInstance().signInWithEmailAndPassword(email, password)
    .addOnCompleteListener { task ->
        if (task.isSuccessful) {
            Log.d("Login", "Success: ${task.result?.user?.uid}")
        } else {
            Log.e("Login", "Error: ${task.exception}")
        }
    }
```

**Impact:**  
- Reduced **authentication time by 30%**, improved **security** with **JWT tokens**.

---

## **26. How do you handle push notifications in Android using Firebase Cloud Messaging (FCM)?**  

### **Answer:**  
At **Surveykshan**, I implemented **FCM for push notifications**.  

✅ **Set up Firebase SDK**  
✅ **Handle foreground & background messages**  
✅ **Use Data Payload for custom actions**  

**Example: Handling Notification in Foreground:**  
```kotlin
override fun onMessageReceived(remoteMessage: RemoteMessage) {
    remoteMessage.notification?.let {
        showNotification(it.title, it.body)
    }
}
```

**Impact:**  
- Improved **user engagement by 35%** with **personalized notifications**.

---

## **27. What are the differences between Room Database and SQLite?**  

### **Answer:**  
At **Mela App**, I used **Room** instead of SQLite for better efficiency.  

| Feature | Room Database | SQLite |
|---------|--------------|--------|
| **Query Writing** | Uses **DAO & LiveData** | Uses raw SQL |
| **Boilerplate Code** | ✅ Less | ❌ More |
| **Compile-time Validation** | ✅ Yes | ❌ No |
| **Coroutines Support** | ✅ Yes | ❌ No |

**Impact:**  
- **Reduced database errors by 50%**, improved **code maintainability**.

---

## **28. How do you implement Dark Mode in Android?**  

### **Answer:**  
✅ **Use `values-night` folder for themes**  
✅ **Use `AppCompatDelegate` to switch themes**  
✅ **Save user preference in SharedPreferences**  

**Example Code to Switch Dark Mode:**  
```kotlin
AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_YES)
```

**Impact:**  
- **Improved UX by providing theme customization**.

---

## **29. How does Retrofit handle API errors, and how do you implement global error handling?**  

### **Answer:**  
At **Surveykshan**, I implemented **global API error handling** with Retrofit.  

✅ **Use Response Wrapping** – To handle **error states**  
✅ **Use OkHttp Interceptors** – To log & modify requests  
✅ **Use Coroutines & try-catch**  

**Example Global Error Handling:**  
```kotlin
suspend fun safeApiCall(call: suspend () -> Response<T>): Result<T> {
    return try {
        val response = call()
        if (response.isSuccessful) {
            Result.Success(response.body()!!)
        } else {
            Result.Error(response.errorBody()?.string() ?: "Unknown Error")
        }
    } catch (e: Exception) {
        Result.Error(e.localizedMessage ?: "Network Error")
    }
}
```

**Impact:**  
- **Reduced API errors by 40%**, improved **app stability**.

---

## **30. How do you handle large data sets efficiently in RecyclerView?**  

### **Answer:**  
At **Mela App**, I optimized **RecyclerView performance** using:  

✅ **DiffUtil for Efficient Updates**  
✅ **ViewHolder Pattern to Reuse Views**  
✅ **Paging 3 for Large Data Handling**  

**Example Using DiffUtil:**  
```kotlin
class MyDiffCallback : DiffUtil.ItemCallback<MyData>() {
    override fun areItemsTheSame(old: MyData, new: MyData) = old.id == new.id
    override fun areContentsTheSame(old: MyData, new: MyData) = old == new
}
```

**Impact:**  
- Improved **scrolling performance by 50%**, **reduced UI lag**.
