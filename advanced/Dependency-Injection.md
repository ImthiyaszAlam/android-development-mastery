# Dependency Injection (DI)

## Overview

### **What is Dependency Injection?**
Dependency Injection is a design pattern that allows an object to receive its dependencies from an external source rather than creating them internally. This promotes loose coupling, better code maintainability, and easier testing.

### **Why Dependency Injection?**
1. **Loose Coupling:** Reduces dependencies between objects, making the code easier to modify or extend.
2. **Reusability:** Promotes reusable components.
3. **Testing:** Simplifies unit testing by allowing mock dependencies.
4. **Readability:** Enhances code readability by clearly defining dependencies.

### **How Dependency Injection Works**
DI frameworks (e.g., Hilt, Dagger) manage the creation and provision of dependencies. They use annotations and configuration files to bind the required dependencies.

---

## Types of Dependency Injection

1. **Constructor Injection**
   - Dependencies are provided through the object's constructor.
   - **Example:**
     ```java
     public class Engine {
         public Engine() { }
     }

     public class Car {
         private Engine engine;

         public Car(Engine engine) {
             this.engine = engine;
         }
     }
     ```

2. **Field Injection**
   - Dependencies are injected directly into the fields of a class.
   - **Example (with Dagger):**
     ```java
     public class Car {
         @Inject
         Engine engine;
     }
     ```

3. **Method Injection**
   - Dependencies are provided via setter or custom methods.
   - **Example:**
     ```java
     public class Car {
         private Engine engine;

         @Inject
         public void setEngine(Engine engine) {
             this.engine = engine;
         }
     }
     ```

---

## Prebuilt Classes, Interfaces, and Annotations

### **Hilt (Modern DI Framework for Android)**

#### Key Components:
1. **@HiltAndroidApp**
   - Marks the application class as the entry point for Hilt.
   - **Usage:**
     ```java
     @HiltAndroidApp
     public class MyApp extends Application { }
     ```

2. **@Inject**
   - Marks a constructor, field, or method as a dependency injection target.
   - **Usage:**
     ```java
     public class Engine {
         @Inject
         public Engine() { }
     }
     ```

3. **@Module**
   - Defines a class that provides dependencies.
   - **Usage:**
     ```java
     @Module
     @InstallIn(ActivityComponent.class)
     public class AppModule {
         @Provides
         public Engine provideEngine() {
             return new Engine();
         }
     }
     ```

4. **@Provides**
   - Annotates methods inside a `@Module` to specify how to create a dependency.
   - **Usage:** See `@Module` example.

5. **@Singleton**
   - Ensures a single instance of a dependency is created.
   - **Usage:**
     ```java
     @Provides
     @Singleton
     public Engine provideEngine() {
         return new Engine();
     }
     ```

6. **@InstallIn**
   - Specifies where the module should be installed (e.g., ActivityComponent, ApplicationComponent).

---

### **Dagger 2 (Predecessor of Hilt)**

#### Key Components:
1. **@Component**
   - Defines the bridge between the module and the class that requires dependencies.
   - **Usage:**
     ```java
     @Component
     public interface CarComponent {
         Car getCar();
     }
     ```

2. **@Subcomponent**
   - Used for creating child components.
   - **Usage:**
     ```java
     @Subcomponent
     public interface EngineComponent {
         Engine getEngine();
     }
     ```

3. **@Binds**
   - Replaces `@Provides` for abstract methods.
   - **Usage:**
     ```java
     @Module
     public abstract class AppModule {
         @Binds
         abstract Engine bindEngine(PetrolEngine engine);
     }
     ```

---

### Comparison: Hilt vs. Dagger
| **Aspect**           | **Hilt**                     | **Dagger**                   |
|-----------------------|------------------------------|------------------------------|
| **Ease of Use**       | Easier, requires fewer lines | Requires manual setup        |
| **Integration**       | Built for Android           | General-purpose DI framework |
| **Annotation Count**  | Fewer annotations           | More verbose                 |

---

## Real-Life Example: API Client with Hilt

### Scenario: Injecting a Retrofit Instance

#### Step 1: Add Dependencies
Add Hilt dependencies in `build.gradle`:
```gradle
implementation "com.google.dagger:hilt-android:2.44"
kapt "com.google.dagger:hilt-compiler:2.44"
```

#### Step 2: Application Class
```java
@HiltAndroidApp
public class MyApplication extends Application { }
```

#### Step 3: Create a Module
```java
@Module
@InstallIn(SingletonComponent.class)
public class NetworkModule {
    @Provides
    @Singleton
    public Retrofit provideRetrofit() {
        return new Retrofit.Builder()
                .baseUrl("https://api.example.com")
                .addConverterFactory(GsonConverterFactory.create())
                .build();
    }
}
```

#### Step 4: Inject Dependency
```java
@AndroidEntryPoint
public class MainActivity extends AppCompatActivity {
    @Inject
    Retrofit retrofit;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Use the injected Retrofit instance
    }
}
```

---

## Summary

### Key Concepts:
1. **DI Frameworks:** Hilt (recommended), Dagger (advanced).
2. **Annotations:** `@Inject`, `@Module`, `@Provides`, `@Singleton`, etc.
3. **Injection Types:** Constructor, Field, Method.
4. **Benefits:** Loose coupling, better testing, reusability.

