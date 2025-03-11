# **RxKotlin in Android (ReactiveX for Kotlin)**  

## **What is RxKotlin?**  
RxKotlin is a Kotlin extension for **RxJava**, which is a Reactive Programming library for composing asynchronous and event-based programs. RxKotlin simplifies working with **observables**, **streams**, and **functional reactive programming** in Kotlin.  

It provides a **declarative way** to handle asynchronous data streams and transformations, making it useful for handling API calls, UI events, database queries, and more.  

## **Why Use RxKotlin?**  
- **Simplifies Asynchronous Programming** – Handles threading efficiently using **Schedulers**.  
- **Functional & Declarative** – Avoids callback hell with operators like `map()`, `flatMap()`, `filter()`, etc.  
- **Composable** – Multiple data streams can be combined easily.  
- **Error Handling** – Built-in error handling using `onError()` or `retry()`.  
- **Thread Management** – Easy thread switching with `Schedulers.io()` and `AndroidSchedulers.mainThread()`.  

---

## **How to Use RxKotlin in an Android App?**  
1. **Add Dependencies:**  
   ```kotlin
   implementation("io.reactivex.rxjava3:rxjava:3.x.x")
   implementation("io.reactivex.rxjava3:rxandroid:3.x.x")
   implementation("io.reactivex.rxjava3:rxkotlin:3.x.x")
   ```

2. **Create an Observable:**  
   ```kotlin
   val observable = Observable.create<String> { emitter ->
       emitter.onNext("Hello")
       emitter.onNext("RxKotlin")
       emitter.onComplete()
   }
   ```

3. **Create an Observer:**  
   ```kotlin
   val observer = object : Observer<String> {
       override fun onSubscribe(d: Disposable) {
           Log.d("RxKotlin", "Subscribed")
       }

       override fun onNext(t: String) {
           Log.d("RxKotlin", "Received: $t")
       }

       override fun onError(e: Throwable) {
           Log.e("RxKotlin", "Error: ${e.message}")
       }

       override fun onComplete() {
           Log.d("RxKotlin", "Completed")
       }
   }
   ```

4. **Subscribe Observer to Observable:**  
   ```kotlin
   observable.subscribe(observer)
   ```

---

# **Key Components in RxKotlin**  

## **1. Observables & Flowables**  
### **Observables (`Observable<T>`)**
- Emits **multiple** data items over time.  
- Can be **hot** or **cold**.
- Handles **backpressure poorly** (use `Flowable` if backpressure handling is needed).  

**Example:**
```kotlin
Observable.just("A", "B", "C")
    .subscribe { value -> Log.d("RxKotlin", "Received: $value") }
```

### **Flowable (`Flowable<T>`)**
- Handles **backpressure** efficiently.  
- Used when a **large amount of data** is emitted rapidly.  
- Requires a **BackpressureStrategy** (`BUFFER`, `DROP`, `LATEST`).  

**Example:**
```kotlin
Flowable.range(1, 1000000)
    .onBackpressureBuffer()
    .observeOn(Schedulers.io())
    .subscribe { Log.d("RxKotlin", "Received: $it") }
```

## **2. Single, Maybe, and Completable**  
| Type | Description | Example |
|------|------------|---------|
| `Single<T>` | Emits **a single value** or an error | `Single.just("Success").subscribe { Log.d("RxKotlin", it) }` |
| `Maybe<T>` | Emits **a single value or nothing** | `Maybe.just("Data").subscribe { Log.d("RxKotlin", it) }` |
| `Completable` | Only **completes or errors**, no data emission | `Completable.fromAction { Log.d("RxKotlin", "Done") }.subscribe()` |

---

# **Key Prebuilt Classes & Interfaces in RxKotlin**  

## **1. Key Classes**
| Class | Description |
|-------|-------------|
| `Observable<T>` | Represents an observable data stream. |
| `Flowable<T>` | Handles streams with **backpressure** support. |
| `Single<T>` | Emits **one** value or an error. |
| `Maybe<T>` | Emits **one** value, **or nothing**, or an error. |
| `Completable` | Signals when **an operation is complete** without emitting data. |
| `Disposable` | Represents a connection to an `Observable`, can be disposed to cancel emissions. |
| `Scheduler` | Manages **threading**, like `Schedulers.io()`, `Schedulers.computation()`. |

---

# **2. Key Interfaces**
| Interface | Description |
|-----------|-------------|
| `Observer<T>` | Observer that receives emissions from an `Observable`. |
| `DisposableObserver<T>` | Observer that automatically disposes when completed. |
| `FlowableSubscriber<T>` | Used for handling `Flowable` with **backpressure support**. |
| `Subject<T>` | Acts as **both** an Observable and an Observer. |
| `Scheduler` | Defines execution threads for Rx operations. |

---

# **Key Prebuilt Functions in RxKotlin**  

## **1. Common Operators**
| Function | Description |
|----------|-------------|
| `map {}` | Transforms emitted items. |
| `flatMap {}` | Converts an item into another Observable. |
| `filter {}` | Filters emissions based on a condition. |
| `merge()` | Combines multiple Observables. |
| `zip()` | Combines two or more Observables and emits a single item. |
| `buffer(n)` | Collects items into **lists of n** items. |
| `throttleFirst()` | Emits only **one item per time interval**. |
| `debounce()` | Emits an item only if a certain **time period has passed**. |

**Example:**
```kotlin
Observable.just(1, 2, 3, 4)
    .map { it * 10 }
    .filter { it > 20 }
    .subscribe { Log.d("RxKotlin", "Value: $it") }
```

---

## **Threading in RxKotlin**
RxKotlin provides **Schedulers** to manage **background and main thread execution**.  

| Scheduler | Description |
|-----------|-------------|
| `Schedulers.io()` | Runs on **I/O threads** (for networking, file access, databases). |
| `Schedulers.computation()` | Used for **CPU-intensive tasks** (like calculations, image processing). |
| `Schedulers.newThread()` | Creates a new thread for each task. |
| `AndroidSchedulers.mainThread()` | Runs on the **main UI thread**. |

**Example:**
```kotlin
Observable.just("Hello")
    .subscribeOn(Schedulers.io())  // Runs in background
    .observeOn(AndroidSchedulers.mainThread())  // Updates UI
    .subscribe { Log.d("RxKotlin", "Received: $it") }
```

---

# **Real-Life Example: Handling API Requests with RxKotlin**
Using **Retrofit** with RxKotlin for an API request:

### **1. Define API Interface**
```kotlin
interface ApiService {
    @GET("users")
    fun getUsers(): Single<List<User>>
}
```

### **2. Create Retrofit Instance**
```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .addCallAdapterFactory(RxJava3CallAdapterFactory.create()) // RxJava adapter
    .build()

val apiService = retrofit.create(ApiService::class.java)
```

### **3. Call API & Handle Response**
```kotlin
apiService.getUsers()
    .subscribeOn(Schedulers.io())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe({ users ->
        Log.d("RxKotlin", "Users: $users")
    }, { error ->
        Log.e("RxKotlin", "Error: ${error.message}")
    })
```

---

# **Conclusion**
RxKotlin is a powerful tool for managing **asynchronous operations** in Android. It provides **functional, declarative, and thread-safe programming**, making it perfect for **API calls, UI updates, event handling, and data manipulation**.

