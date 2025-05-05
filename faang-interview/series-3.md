
### ❓11. How do you optimize app performance and reduce unnecessary recompositions or memory usage?

**🧠 How to Answer:**

* Discuss tools (e.g., **Profiler**, **LeakCanary**, **StrictMode**, **Crashlytics**).
* Talk about Compose performance (e.g., `remember`, `derivedStateOf`, avoiding key recompositions).
* Mention improvements made and their impact.

**✅ Ideal Answer:**

> I use tools like **Android Profiler**, **LeakCanary**, and **Crashlytics** to monitor memory usage and performance bottlenecks.
>
> In the **MELA App**, we:
>
> * Used `remember` and `derivedStateOf` in Jetpack Compose to avoid unnecessary recompositions.
> * Deferred expensive API calls using `LaunchedEffect(Unit)` only once on screen launch.
> * Implemented image loading via **Glide** with caching enabled, reducing network calls by **40%**.
>
> These optimizations improved scroll smoothness and reduced memory-related crashes by **30%**.

---

### ❓12. How do you handle background tasks in Android?

**🧠 How to Answer:**

* Explain tools like **WorkManager**, **Coroutines**, **Foreground Services**, or **AlarmManager**.
* Mention when you choose each and why.
* Share a project where background work was critical.

**✅ Ideal Answer:**

> I use different tools based on the use-case:
>
> * **WorkManager**: For guaranteed and battery-friendly tasks (e.g., offline sync).
> * **Coroutines**: For lightweight async background operations.
> * **AlarmManager**: For precise periodic jobs.
>
> In **Surveykshan App**, I used WorkManager to sync form data with the server in the background, even if the app was killed.
>
> * This helped maintain data integrity and offline usability in poor network areas.
> * We reduced manual sync errors by **70%**.

---

### ❓13. How do you manage secure API communication in your Android apps?

**🧠 How to Answer:**

* Talk about **HTTPS**, **JWT**, **OAuth**, and best practices like **network interceptors**.
* Mention sensitive data handling (e.g., using **EncryptedSharedPreferences** or **Keystore**).

**✅ Ideal Answer:**

> I follow industry best practices for secure communication:
>
> * All APIs are accessed via **HTTPS**.
> * In the **MELA App**, I implemented **OAuth 2.0 with JWT tokens** for role-based access.
> * Stored tokens using **EncryptedSharedPreferences** to prevent plain-text storage.
> * Used Retrofit interceptors to auto-refresh expired tokens securely.
>
> This ensured secure logins and **99.9% success rate** in role-based authentication.

---

### ❓14. How do you test your Android apps? What types of testing do you focus on?

**🧠 How to Answer:**

* Talk about **Unit Testing**, **UI Testing**, **Integration Testing**, and tools like **JUnit**, **Espresso**, **Mockito**, etc.
* Mention layers tested (ViewModel, Repository, UI).

**✅ Ideal Answer:**

> I write **unit tests** for ViewModels and business logic using **JUnit** and **Mockito**, and **UI tests** with **Espresso**.
>
> In the **UPAVP-PEMS App**:
>
> * ViewModel logic (like search & filtering) had over **85% test coverage**.
> * API error handling was tested using mocked Retrofit responses.
> * Jetpack Compose UI was verified using `composeTestRule` for accessibility and layout.
>
> Testing helped us catch bugs early and reduce release-time regressions by **50%**.

---

### ❓15. Describe your approach to integrating REST APIs using Retrofit and Coroutines.

**🧠 How to Answer:**

* Explain setting up Retrofit, data parsing with GSON/Moshi, and async calls using Coroutines.
* Mention error handling, loading states, and threading.

**✅ Ideal Answer:**

> I integrate APIs using **Retrofit** and **Kotlin Coroutines** for non-blocking network calls.
>
> In the **MELA App**:
>
> * Configured Retrofit with OkHttpClient, logging interceptor, and Moshi for JSON parsing.
> * Created a sealed class `ApiResult` to handle **Success**, **Error**, and **Loading** states cleanly.
> * Called APIs using `suspend` functions inside a **Repository**, exposing results via `LiveData`/`StateFlow` to the UI.
>
> This approach reduced boilerplate, handled errors gracefully, and improved app responsiveness.

