# 📌 Jetpack Components (Android - Kotlin)

## 🔹 What is Jetpack?

Jetpack is a collection of Android libraries and tools designed to **accelerate app development** by providing robust, maintainable, and scalable solutions. These libraries **reduce boilerplate code**, ensure **backward compatibility**, and help in **following best practices**.

---

## 🔹 Why Jetpack?

### ✅ Benefits:
- **Reduces boilerplate code** and improves code quality.
- **Ensures compatibility** across different Android versions.
- **Follows best practices** like MVVM, Clean Architecture.
- **Handles common tasks** such as navigation, data persistence, and lifecycle management.
- **Improves UI/UX consistency** using Material Design Components.

---

## 🔹 How to Use Jetpack Components?

Jetpack libraries are provided as separate **AndroidX** dependencies. You can add them to your `build.gradle.kts` (Kotlin DSL):

```kotlin
dependencies {
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.4.0")
    implementation("androidx.room:room-runtime:2.4.2")
    kapt("androidx.room:room-compiler:2.4.2")
    implementation("androidx.navigation:navigation-fragment-ktx:2.5.3")
}
```

Each component is **modular**, meaning you can integrate only what you need.

---

# 🔥 Jetpack Components and Their Usage

## **1️⃣ Architecture Components**
Help in building robust, testable, and maintainable apps.

### a) **LiveData**
- **What?** A lifecycle-aware observable data holder.
- **Why?** Ensures UI updates only when components are active.
- **How?** Used with ViewModel to update UI reactively.
- **Real-Life Example:** Fetching and displaying a user's profile in real-time.

#### **Code Example**
```kotlin
class UserViewModel : ViewModel() {
    private val _user = MutableLiveData<User>()
    val user: LiveData<User> get() = _user

    fun fetchUser() {
        _user.value = User("John Doe", 25)
    }
}
```
```kotlin
viewModel.user.observe(viewLifecycleOwner) { user ->
    textView.text = user.name
}
```

---

### b) **ViewModel**
- **What?** Stores UI-related data across configuration changes.
- **Why?** Prevents unnecessary recreation of UI data.
- **How?** Used with LiveData and Repository patterns.

#### **Code Example**
```kotlin
class UserViewModel : ViewModel() {
    val user = MutableLiveData<User>()
}
```

---

### c) **Room Database**
- **What?** An abstraction layer over SQLite.
- **Why?** Ensures type safety, reduces boilerplate.
- **How?** Uses `@Entity`, `@Dao`, `@Database` annotations.

#### **Code Example**
```kotlin
@Entity
data class User(@PrimaryKey val id: Int, val name: String)

@Dao
interface UserDao {
    @Insert
    suspend fun insert(user: User)

    @Query("SELECT * FROM User")
    fun getAllUsers(): LiveData<List<User>>
}
```

---

### d) **DataStore (Alternative to SharedPreferences)**
- **What?** Stores key-value pairs efficiently using Coroutines.
- **Why?** Provides safer and faster data storage.
- **How?** Uses Proto DataStore for typed objects.

#### **Code Example**
```kotlin
val Context.dataStore: DataStore<Preferences> by preferencesDataStore(name = "settings")
```

---

## **2️⃣ UI Components**
Improve UI and navigation management.

### a) **Jetpack Compose**
- **What?** A modern UI toolkit for declarative UI.
- **Why?** Eliminates XML, uses Kotlin for UI definition.
- **How?** Uses `@Composable` functions.

#### **Code Example**
```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Hello, $name!")
}
```

---

### b) **Navigation Component**
- **What?** Manages navigation between fragments/activities.
- **Why?** Ensures consistency, simplifies deep linking.
- **How?** Uses a `NavController`.

#### **Code Example**
```kotlin
findNavController().navigate(R.id.action_home_to_profile)
```

---

### c) **Paging**
- **What?** Handles large datasets efficiently.
- **Why?** Loads data incrementally to optimize memory usage.
- **How?** Uses `PagingSource` and `PagingData`.

#### **Code Example**
```kotlin
val pagingSource = UserPagingSource(apiService)
val pager = Pager(PagingConfig(pageSize = 20)) { pagingSource }
```

---

## **3️⃣ Behavior Components**
Handle user interactions efficiently.

### a) **WorkManager**
- **What?** Manages background tasks with constraints.
- **Why?** Ensures tasks run even after app restarts.
- **How?** Uses `OneTimeWorkRequest` and `PeriodicWorkRequest`.

#### **Code Example**
```kotlin
val workRequest = OneTimeWorkRequestBuilder<MyWorker>().build()
WorkManager.getInstance(context).enqueue(workRequest)
```

---

### b) **CameraX**
- **What?** Simplifies camera integration.
- **Why?** Provides a consistent API for different devices.
- **How?** Uses `PreviewView` and `ImageCapture`.

#### **Code Example**
```kotlin
val cameraProvider = ProcessCameraProvider.getInstance(context).get()
cameraProvider.bindToLifecycle(this, CameraSelector.DEFAULT_BACK_CAMERA, preview)
```

---

### c) **ML Kit**
- **What?** Provides machine learning features.
- **Why?** Supports text recognition, face detection, etc.
- **How?** Uses on-device and cloud APIs.

#### **Code Example**
```kotlin
val textRecognizer = TextRecognition.getClient(TextRecognizerOptions.DEFAULT_OPTIONS)
```

---

## **4️⃣ Security Components**
Enhance security and authentication.

### a) **Biometric Authentication**
- **What?** Supports fingerprint, face unlock.
- **Why?** Adds an extra layer of security.
- **How?** Uses `BiometricPrompt`.

#### **Code Example**
```kotlin
BiometricPrompt(activity, executor, callback).authenticate(promptInfo)
```

---

# 🔍 **Comparison of Different Jetpack Components**

| Feature | Jetpack Component | Alternative |
|---------|------------------|------------|
| UI | Jetpack Compose | XML |
| Database | Room | SQLite |
| Navigation | Navigation Component | Fragment Transactions |
| Background Work | WorkManager | AsyncTask, JobScheduler |
| Data Storage | DataStore | SharedPreferences |
| Paging | Paging 3 | RecyclerView with manual pagination |

---

# ✅ Conclusion

### **📌 Summary**
- **Jetpack Components** simplify Android development.
- They **ensure efficiency, modularity, and maintainability**.
- Using Jetpack allows for **better app architecture and performance**.
