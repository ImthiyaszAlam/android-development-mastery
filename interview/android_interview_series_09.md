## **21. How does Clean Architecture improve Android development? How did you implement it in your projects?**  

### **Answer:**  
At **Mela App**, I implemented **Clean Architecture** to separate concerns and improve scalability.  

### **Clean Architecture Layers:**  
1. **Presentation Layer** (UI, ViewModel) – Uses **LiveData/StateFlow**  
2. **Domain Layer** (Use Cases, Business Logic)  
3. **Data Layer** (Repository, API, Database)  

**Example Implementation:**  
```kotlin
// Use Case (Domain Layer)
class GetUserDataUseCase @Inject constructor(private val repository: UserRepository) {
    suspend operator fun invoke(userId: String): User = repository.getUserData(userId)
}

// ViewModel (Presentation Layer)
@HiltViewModel
class UserViewModel @Inject constructor(private val getUserDataUseCase: GetUserDataUseCase) : ViewModel() {
    val userData = liveData { emit(getUserDataUseCase("123")) }
}
```

### **Impact:**  
✅ **Improved testability**  
✅ **Easier to maintain and scale**  
✅ **Decouples UI from business logic**  

---

## **22. How do you handle memory leaks in Android?**  

### **Answer:**  
At **Surveykshan**, I optimized memory usage by:  

✅ **Using WeakReferences** (Prevent activity leaks)  
✅ **Avoiding static context references**  
✅ **Using LeakCanary** (Detect memory leaks)  
✅ **Clearing listeners in onDestroy()**  

**Example Fix:**  
```kotlin
class MyActivity : AppCompatActivity() {
    private val listener = View.OnClickListener { /* do something */ }

    override fun onDestroy() {
        super.onDestroy()
        button.setOnClickListener(null) // Prevent memory leak
    }
}
```

**Impact:**  
- **Reduced memory leaks**, improved **app stability by 30%**.  

---

## **23. Explain MVVM vs MVP. Why did you choose MVVM?**  

### **Answer:**  
At **CloudSect**, I used **MVVM** for better separation of concerns.  

| Feature | MVVM (Used in Projects) | MVP |
|---------|----------------|-----|
| **View Dependency** | UI observes ViewModel | View holds Presenter |
| **Data Binding** | ✅ Supported | ❌ Not Supported |
| **Separation of Concerns** | ✅ Strong | ❌ Weak |
| **Testability** | ✅ Easier | ❌ Difficult |

**Why MVVM?**  
1. **Better UI updates** (LiveData/StateFlow auto-updates UI).  
2. **Decouples UI from business logic**.  
3. **Easier to write unit tests**.  

---

## **24. How do you optimize an API-heavy Android application?**  

### **Answer:**  
At **Mela App**, I optimized API calls by:  

✅ **Using Retrofit with OkHttp Interceptor**  
✅ **Implementing API Response Caching**  
✅ **Using Pagination (Paging 3)**  

**Example of API Caching:**  
```kotlin
val cache = Cache(File(context.cacheDir, "http_cache"), 10 * 1024 * 1024) // 10MB Cache

val client = OkHttpClient.Builder()
    .cache(cache)
    .addInterceptor { chain ->
        val response = chain.proceed(chain.request())
        response.newBuilder().header("Cache-Control", "public, max-age=60").build()
    }.build()
```

**Impact:**  
- **Reduced API load by 40%**, improved **response time**.  

---

## **25. What is the difference between LiveData and StateFlow?**  

### **Answer:**  
| Feature | LiveData | StateFlow |
|---------|---------|-----------|
| **Hot/Cold Stream** | Cold (Starts when observed) | Hot (Always active) |
| **Lifecycle Aware?** | ✅ Yes | ❌ No |
| **Multiple Subscribers?** | ✅ Yes | ✅ Yes |
| **Data Persistence?** | No history | Keeps latest value |

**When to use?**  
- Use **LiveData** for UI updates.  
- Use **StateFlow** for managing state in ViewModel.  

---

## **26. What security measures do you take for Android applications?**  

### **Answer:**  
At **Surveykshan**, I improved security by:  

✅ **Using Encrypted SharedPreferences**  
✅ **Securing API keys (No hardcoded secrets)**  
✅ **ProGuard & R8 for code obfuscation**  

**Example:**  
```kotlin
val masterKey = MasterKey.Builder(context).setKeyScheme(MasterKey.KeyScheme.AES256_GCM).build()
val encryptedPrefs = EncryptedSharedPreferences.create(
    context,
    "secure_prefs",
    masterKey,
    EncryptedSharedPreferences.PrefKeyEncryptionScheme.AES256_SIV,
    EncryptedSharedPreferences.PrefValueEncryptionScheme.AES256_GCM
)
```

**Impact:**  
- **Improved security**, protected **user data** from leaks.  

---

## **27. What are some ways to improve app startup time?**  

### **Answer:**  
At **Mela App**, I reduced app startup time by:  

✅ **Using SplashScreen API** (Preload essential data)  
✅ **Lazy Loading Dependencies**  
✅ **Optimizing Application.onCreate()**  

**Example:**  
```kotlin
override fun onCreate() {
    super.onCreate()
    GlobalScope.launch(Dispatchers.IO) { preloadData() } // Run in background
}
```

**Impact:**  
- **Reduced cold start time by 50%**, improved **user experience**.  

---

## **28. How does Google Maps API work? How did you use it in your project?**  

### **Answer:**  
At **UPAVP-PEMS**, I integrated **Google Maps API** for real-time tracking.  

✅ **Used Marker Clustering** for handling multiple locations.  
✅ **Implemented Geofencing for user location alerts.**  

**Example:**  
```kotlin
mMap.addMarker(MarkerOptions().position(LatLng(28.7041, 77.1025)).title("New Delhi"))
```

**Impact:**  
- **Improved tracking accuracy**, **reduced API calls**.  

---

## **29. What is the purpose of WorkManager’s constraints?**  

### **Answer:**  
Constraints ensure background tasks run **only when required conditions are met**.  

✅ **NetworkType (WiFi only)**  
✅ **Battery level (Avoid low battery execution)**  
✅ **Device Charging (Run only when plugged in)**  

**Example:**  
```kotlin
val constraints = Constraints.Builder()
    .setRequiredNetworkType(NetworkType.CONNECTED)
    .setRequiresCharging(true)
    .build()

val workRequest = OneTimeWorkRequestBuilder<MyWorker>().setConstraints(constraints).build()
WorkManager.getInstance(context).enqueue(workRequest)
```

**Impact:**  
- **Optimized battery usage**, **reduced unnecessary execution**.  

---

## **30. How do you handle app crashes effectively?**  

### **Answer:**  
At **Surveykshan**, I implemented **Firebase Crashlytics** to track and fix crashes.  

✅ **Used Crashlytics for real-time crash reporting**  
✅ **Logged non-fatal errors for debugging**  
✅ **Provided meaningful error messages to users**  

**Example:**  
```kotlin
try {
    val result = riskyOperation()
} catch (e: Exception) {
    FirebaseCrashlytics.getInstance().recordException(e)
}
```

**Impact:**  
- **Reduced crash rate by 40%**, improved **app stability**.  

---

### **Final Strategy to Crack FAANG 🚀**  
✔ **Master Android Core + DSA**  
✔ **Mock Interviews (LLD, HLD, Behaviorals)**  
✔ **Build Scalable Android Apps (Jetpack, Firebase, AWS)**  
