
# **Hilt (Android-Kotlin)**

## **What is Hilt?**
Hilt is a **dependency injection** (DI) library built on top of **Dagger** for Android apps. It simplifies DI by managing component lifecycles and providing a standardized way to inject dependencies across an application.

## **Why Use Hilt?**
- **Reduces Boilerplate Code**: Hilt automates much of the dependency injection setup.
- **Manages Dependencies Efficiently**: Hilt takes care of component lifecycles.
- **Standardized Dependency Injection**: Hilt provides a consistent DI setup for Android apps.
- **Works with Jetpack Components**: It integrates well with ViewModels, Navigation, WorkManager, etc.
- **Improved Testability**: Hilt makes it easy to inject test dependencies.

## **How Does Hilt Work?**
Hilt works by generating and managing dependency injection components automatically. It provides **scoped components** that match the lifecycle of Android classes (Application, Activity, Fragment, ViewModel, etc.).

---

# **Prebuilt Classes, Interfaces, and Concepts in Hilt**

## **1. @HiltAndroidApp**
- **Description:** Marks the `Application` class as the Hilt container.
- **Usage:** Required to enable Hilt in the application.
- **Code Example:**
  ```kotlin
  @HiltAndroidApp
  class MyApplication : Application()
  ```

## **2. @Inject**
- **Description:** Used to inject dependencies automatically.
- **Usage:** Annotate constructor or fields where Hilt should inject dependencies.
- **Code Example:**
  ```kotlin
  class UserRepository @Inject constructor(private val apiService: ApiService)
  ```

## **3. @Module and @InstallIn**
- **Description:** Defines a module that provides dependencies.
- **Usage:** Used to create dependencies that cannot be constructor-injected.
- **Code Example:**
  ```kotlin
  @Module
  @InstallIn(SingletonComponent::class)
  object AppModule {
      @Provides
      fun provideApiService(): ApiService {
          return ApiService.create()
      }
  }
  ```

## **4. @Provides**
- **Description:** Used inside a module to manually provide a dependency.
- **Usage:** Use when the dependency cannot be constructor-injected.
- **Code Example:**
  ```kotlin
  @Provides
  fun provideDatabase(app: Application): AppDatabase {
      return Room.databaseBuilder(app, AppDatabase::class.java, "app_db").build()
  }
  ```

## **5. @Singleton**
- **Description:** Ensures a dependency is a singleton.
- **Usage:** Applied to methods inside modules.
- **Code Example:**
  ```kotlin
  @Provides
  @Singleton
  fun provideRetrofit(): Retrofit {
      return Retrofit.Builder()
          .baseUrl("https://api.example.com")
          .addConverterFactory(GsonConverterFactory.create())
          .build()
  }
  ```

## **6. @ActivityScoped, @FragmentScoped, @ViewModelScoped**
- **Description:** Defines the lifecycle of injected dependencies.
- **Usage:**
  - `@ActivityScoped`: Single instance in an activity.
  - `@FragmentScoped`: Single instance in a fragment.
  - `@ViewModelScoped`: Single instance in a ViewModel.

- **Code Example:**
  ```kotlin
  @Provides
  @ActivityScoped
  fun provideUserManager(): UserManager {
      return UserManager()
  }
  ```

## **7. @EntryPoint**
- **Description:** Used to inject dependencies into classes that Hilt does not support natively.
- **Usage:** Used in BroadcastReceivers, ContentProviders, and custom classes.
- **Code Example:**
  ```kotlin
  @EntryPoint
  @InstallIn(ApplicationComponent::class)
  interface MyEntryPoint {
      fun getUserRepository(): UserRepository
  }
  ```

## **8. @Binds**
- **Description:** Used when injecting an interface implementation.
- **Usage:** Replaces `@Provides` when returning an instance of an interface.
- **Code Example:**
  ```kotlin
  @Module
  @InstallIn(SingletonComponent::class)
  abstract class RepositoryModule {
      @Binds
      abstract fun bindUserRepository(
          userRepositoryImpl: UserRepositoryImpl
      ): UserRepository
  }
  ```

---

# **Different Types of Components in Hilt**
Hilt provides several built-in components to manage dependencies based on lifecycle.

| Component               | Scope       | Example Use Case |
|-------------------------|------------|------------------|
| `SingletonComponent`    | Application-wide | Network service, Database |
| `ActivityComponent`     | Activity lifecycle | ViewModels, UI-related classes |
| `FragmentComponent`     | Fragment lifecycle | Fragment-specific dependencies |
| `ViewModelComponent`    | ViewModel lifecycle | Repositories for ViewModels |
| `ServiceComponent`      | Service lifecycle | Background tasks, WorkManager |
| `ViewComponent`         | View lifecycle | Custom Views, UI elements |

**Example: Using `SingletonComponent` for Global Dependencies**
```kotlin
@Module
@InstallIn(SingletonComponent::class)
object NetworkModule {
    @Provides
    @Singleton
    fun provideRetrofit(): Retrofit {
        return Retrofit.Builder()
            .baseUrl("https://example.com/")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
    }
}
```

---

# **Real-Life Example: Using Hilt in an Android App**
## **Step 1: Add Dependencies**
Add these dependencies in `build.gradle (Module: app)`:
```gradle
dependencies {
    implementation "com.google.dagger:hilt-android:2.48"
    kapt "com.google.dagger:hilt-compiler:2.48"
}
```

## **Step 2: Create Application Class**
```kotlin
@HiltAndroidApp
class MyApp : Application()
```

## **Step 3: Create Repository**
```kotlin
class UserRepository @Inject constructor(private val apiService: ApiService) {
    fun getUsers() = apiService.getUsers()
}
```

## **Step 4: Provide Dependencies in a Module**
```kotlin
@Module
@InstallIn(SingletonComponent::class)
object AppModule {
    @Provides
    @Singleton
    fun provideApiService(): ApiService {
        return Retrofit.Builder()
            .baseUrl("https://api.example.com")
            .addConverterFactory(GsonConverterFactory.create())
            .build()
            .create(ApiService::class.java)
    }
}
```

## **Step 5: Inject Dependencies into ViewModel**
```kotlin
@HiltViewModel
class UserViewModel @Inject constructor(private val repository: UserRepository) : ViewModel() {
    fun fetchUsers() = repository.getUsers()
}
```

## **Step 6: Inject ViewModel into Activity**
```kotlin
@AndroidEntryPoint
class MainActivity : AppCompatActivity() {
    private val viewModel: UserViewModel by viewModels()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        viewModel.fetchUsers().observe(this) { users ->
            // Update UI with user data
        }
    }
}
```

---

# **Differences: Hilt vs. Dagger**
| Feature | Hilt | Dagger |
|---------|------|--------|
| **Boilerplate** | Minimal | High |
| **Ease of Use** | Simple | Complex |
| **Component Management** | Automatic | Manual |
| **Integration with Android** | Built-in | Requires setup |
| **Testing Support** | Built-in | Manual setup |

---

# **Conclusion**
Hilt simplifies dependency injection in Android by automating DI setup, lifecycle management, and dependen
