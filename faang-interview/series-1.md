

### ❓ 1. Define MVVM architecture. How have you applied it in your projects?

**🧠 How to Answer:**

* Define MVVM and its components (Model, ViewModel, View).
* Discuss usage of LiveData, ViewModel, Repository, and Data Source.
* Mention project(s) where MVVM was implemented (e.g., MELA App or UPAVP-PEMS).
* Highlight improvements in maintainability, testability, or scalability.

**✅ Ideal Answer:**

> MVVM stands for **Model-View-ViewModel**, a design pattern that helps in separating the business logic from UI code.
>
> * **Model** handles data sources like API calls or local databases.
> * **ViewModel** manages UI-related data using **LiveData** or **StateFlow**, and handles configuration changes.
> * **View** observes the ViewModel and reacts to data changes.
>
> In my **MELA App**, I implemented MVVM to ensure a scalable and maintainable architecture.
>
> * The **Repository** in the Model layer handled both Retrofit API calls and Room database.
> * **ViewModel** exposed data using LiveData, which the Jetpack Compose UI observed.
> * I used **Hilt** for dependency injection to inject repositories into the ViewModel.
>
> This structure made the app modular and easy to test. When we integrated **Paging 3**, only the Repository layer needed changes.

---

### ❓ 2. How did you implement background tasks and data sync in your apps?

**🧠 How to Answer:**

* Mention components like **WorkManager**, **AlarmManager**, or **Coroutine workers**.
* Talk about retry policies, constraints (e.g., only on Wi-Fi or charging).
* Share impact on performance or user experience (e.g., sync success rate or crash reduction).

**✅ Ideal Answer:**

> I used **WorkManager** to schedule and manage background tasks that require guaranteed execution.
>
> In the **Surveykshan App**, I developed a background sync system using WorkManager to upload field data periodically.
>
> * It used constraints like “only on Wi-Fi” and “device charging” to optimize battery and data usage.
> * The task retried automatically on failure and stored offline data until sync was successful.
>
> This improved data consistency and app reliability, reducing user-reported sync issues by 30%.

---

### ❓ 3. How did you handle API integration and network performance optimization?

**🧠 How to Answer:**

* Mention tools like **Retrofit**, **OkHttp**, **Coroutines**, and **caching**.
* Highlight how you reduced latency or improved user experience.
* Use a project like **MELA App** for context.

**✅ Ideal Answer:**

> I integrated APIs using **Retrofit** with **OkHttp Interceptors** and **Kotlin Coroutines** for asynchronous execution.
>
> In the **MELA App**, I implemented a cache mechanism using OkHttp and Retrofit to reduce redundant network calls.
>
> * Enabled response caching and added a network interceptor for offline support.
> * Combined Coroutines with proper error handling and timeouts.
>
> This reduced API response time by **40%** and improved load speed for users with slow connections.

---

### ❓ 4. How did you monitor and reduce crashes in your applications?

**🧠 How to Answer:**

* Talk about tools like **Firebase Crashlytics**, logs, and error handling.
* Share how you interpreted crash reports and fixed the root cause.
* Mention crash rate improvements or reduced ANRs.

**✅ Ideal Answer:**

> I used **Firebase Crashlytics** to monitor crashes and collect stack traces in real-time.
>
> During my internship at **Surveykshan**, I integrated Crashlytics and set up custom keys and logs to identify app states leading to crashes.
>
> * Prioritized critical crashes based on occurrence and impact.
> * Fixed issues like null pointer exceptions and misused lifecycle components.
>
> This reduced crash frequency by **40%** and helped maintain a stable user experience.

---

### ❓ 5. How have you implemented secure authentication in your apps?

**🧠 How to Answer:**

* Mention using **Firebase Authentication**, **JWT**, **OAuth 2.0**, etc.
* Explain how user roles were handled, and how tokens were stored or verified.
* Talk about security measures (e.g., encrypted SharedPreferences, token expiration).

**✅ Ideal Answer:**

> In the **MELA App**, I implemented secure authentication using **OAuth 2.0** and **JWT tokens**.
>
> * Different user roles (admin, student, teacher) were assigned via JWT claims.
> * Tokens were securely stored using encrypted SharedPreferences.
> * Token validity and expiration were verified on app startup.
>
> This ensured **99.9% secure login flows** and protected sensitive APIs from unauthorized access.


