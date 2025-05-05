### ❓21. How did you handle background tasks in your apps?

**🧠 How to Answer:**

* Discuss the use of **WorkManager**, **Coroutines**, or **AlarmManager**.
* Highlight reliability across OS versions and conditions like battery constraints.
* Mention how this improved UX or performance.

**✅ Ideal Answer:**

> I used **WorkManager** in the **Surveykshan App** for background data synchronization to ensure reliability even when the app was closed or device rebooted.
>
> * Configured it with network and battery constraints.
> * Integrated it with **Coroutines** for asynchronous operations.
> * Scheduled retries for failed syncs, using exponential backoff.
>
> This reduced manual user sync actions by **90%** and improved data consistency in poor network areas.

---

### ❓22. How do you handle error states and exceptions in your app?

**🧠 How to Answer:**

* Talk about using `try-catch`, `sealed classes`, `Result`, and proper UI feedback.
* Mention Crashlytics and user-friendly error messaging.

**✅ Ideal Answer:**

> I follow a layered error handling strategy:
>
> * In the Repository, I use `try-catch` with a **sealed class** `ApiResult<Success, Error>`.
> * The ViewModel observes these and emits UI states using `LiveData` or `StateFlow`.
> * UI layers show proper toasts, dialogs, or retry buttons based on error type.
>
> In addition, **Crashlytics** logs uncaught exceptions, which helped me proactively fix bugs — improving crash-free users by **40%**.

---

### ❓23. How did you optimize app performance or memory usage?

**🧠 How to Answer:**

* Mention tools like **Android Profiler**, **StrictMode**, and performance patterns.
* Highlight before/after results and bottlenecks solved.

**✅ Ideal Answer:**

> I optimized **MELA App’s** performance by profiling it with **Android Profiler** and fixing memory leaks.
>
> * Replaced Glide with Coil in Compose UI to reduce memory consumption.
> * Used `ViewModelScope` for long-running tasks instead of `GlobalScope`.
> * Cached API responses using OkHttp and Room to reduce unnecessary calls.
>
> These changes improved app load time by **30%** and cut memory usage by **25%**.

---

### ❓24. How do you ensure security in Android apps?

**🧠 How to Answer:**

* Mention techniques like **JWT**, **OAuth2**, secure storage, and HTTPS.
* Avoid storing sensitive data in SharedPreferences without encryption.

**✅ Ideal Answer:**

> I follow security best practices:
>
> * Used **JWT + OAuth2** in **MELA App** to protect APIs and manage sessions securely.
> * Enabled **HTTPS-only** network calls via Retrofit with certificate pinning.
> * Encrypted sensitive local data using **EncryptedSharedPreferences** and **SQLCipher** (when needed).
>
> Also, I follow Play Store security guidelines and test with tools like **MobSF** to minimize risks.

---

### ❓25. How do you collaborate with backend or cross-functional teams?

**🧠 How to Answer:**

* Focus on tools (Postman, Swagger, Git), communication, ticketing (JIRA), and iteration.
* Show that you understand backend constraints and API design.

**✅ Ideal Answer:**

> At **CloudSect**, I closely worked with backend developers during the REST API integration phase.
>
> * Used **Postman** and **Swagger Docs** for API testing and schema understanding.
> * Attended daily stand-ups, tracked progress via **JIRA**, and shared test cases.
> * Proactively suggested changes in API response formats for better Android integration.
>
> This saved rework time by **20%** and ensured faster and smoother integration cycles.
