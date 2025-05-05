
### ❓16. Why did you choose Clean Architecture, and how did you implement it?

**🧠 How to Answer:**

* Explain the 3-layer structure: **Domain**, **Data**, **Presentation**.
* Discuss decoupling, testability, and long-term maintainability.
* Refer to a specific project like MELA or UPAVP-PEMS.

**✅ Ideal Answer:**

> I adopted **Clean Architecture** to ensure modularity, testability, and a clear separation of concerns.
>
> In the **UPAVP-PEMS App**, I structured the code into:
>
> * **Domain Layer**: Business logic, use cases.
> * **Data Layer**: API services and Room database using repositories.
> * **Presentation Layer**: ViewModels using LiveData/StateFlow to expose data.
>
> This separation made it easier to test use cases independently, onboard new developers quickly, and reduce feature update time by **40%**.

---

### ❓17. What is Hilt and how do you use it for Dependency Injection in your projects?

**🧠 How to Answer:**

* Define Hilt as a DI framework built on top of Dagger.
* Explain how it simplifies component and module creation.
* Show real usage with ViewModel, Repository, and Retrofit.

**✅ Ideal Answer:**

> **Hilt** simplifies Dependency Injection in Android by providing a standard way to declare dependencies and scopes.
>
> In both **MELA** and **Surveykshan Apps**:
>
> * I injected the `Repository` into `ViewModel` using `@HiltViewModel` and `@Inject`.
> * Defined network dependencies (Retrofit, OkHttp) inside `@Module` with `@Provides`.
> * Used `@Singleton` scope for Retrofit and `@ActivityRetainedScoped` for ViewModels.
>
> This eliminated boilerplate Dagger setup, improved testability, and reduced setup time by **60%**.

---

### ❓18. How did you implement Paging 3 and what benefits did it provide?

**🧠 How to Answer:**

* Talk about use-case (e.g., large datasets from API or DB).
* Explain PagingSource, Pager, and UI integration.
* Highlight smoothness, memory management, and user experience.

**✅ Ideal Answer:**

> I used **Paging 3** to efficiently load large lists of properties in the **UPAVP-PEMS App**.
>
> * Implemented `PagingSource` to fetch paginated data from the REST API.
> * Used `Pager` to control flow and cache data via Room.
> * Integrated it with `PagingDataAdapter` and `LazyColumn` in Jetpack Compose.
>
> This significantly reduced memory usage and provided smooth, infinite scrolling. API response size dropped by **70%** per request.

---

### ❓19. How have you used Firebase in your Android apps?

**🧠 How to Answer:**

* Mention specific Firebase services: Auth, Firestore, FCM, Crashlytics.
* Explain how each solved real-world problems.

**✅ Ideal Answer:**

> In multiple projects, I’ve used Firebase services to improve reliability and feature richness:
>
> * **Authentication**: Google Sign-In & OTP in **MELA App**, managing user roles securely.
> * **Cloud Firestore**: Real-time sync for data like live content updates.
> * **FCM**: Delivered push notifications with targeting based on user activity.
> * **Crashlytics**: Tracked crash reports in **Surveykshan App**, reducing crash rate by **40%**.
>
> Firebase allowed me to ship production-ready features quickly without building a backend from scratch.

---

### ❓20. How did you implement Jetpack Compose in your projects, and what advantages did you observe?

**🧠 How to Answer:**

* Talk about why you used Compose over XML.
* Mention features like `State`, `LazyColumn`, theming, reusability.
* Explain improvements in UI dev speed, testing, and maintainability.

**✅ Ideal Answer:**

> I used **Jetpack Compose** for modern UI development in the **MELA App**.
>
> * Used `State` and `remember` for reactive UI.
> * Built reusable components like buttons, cards, input fields using `MaterialTheme`.
> * Implemented complex lists using `LazyColumn` and conditionally rendered layouts.
>
> Compared to XML, Compose reduced UI boilerplate, improved development speed by **40%**, and made screen testing more straightforward with `composeTestRule`.
