
### ❓ 6. What is Jetpack Compose and how have you used it in your apps?

**🧠 How to Answer:**

* Define Jetpack Compose and explain its benefits.
* Talk about state management (e.g., `State`, `remember`, `LaunchedEffect`).
* Mention a project where you used Compose UI and what it improved.

**✅ Ideal Answer:**

> **Jetpack Compose** is a modern declarative UI toolkit for building native Android interfaces with less boilerplate and better reusability.
>
> I used Jetpack Compose in the **MELA App** to revamp the UI for 5+ user roles.
>
> * Managed UI state using `remember` and `mutableStateOf`, ensuring reactivity.
> * Used `Scaffold`, `LazyColumn`, and `Navigation Compose` for structured layouts.
> * Integrated LiveData from ViewModel using `collectAsState()` for lifecycle-safe data observation.
>
> This led to a **30% boost in engagement** due to a smoother and more responsive UI.

---

### ❓ 7. How have you used Firebase services in your projects?

**🧠 How to Answer:**

* Mention Firebase services like **Authentication**, **Firestore**, **FCM**, and **Crashlytics**.
* Explain the use-case, integration process, and benefits seen in production.
* Include real impact (e.g., user retention, crash reduction).

**✅ Ideal Answer:**

> I’ve extensively used **Firebase services** across multiple projects:
>
> * **Authentication**: Used email/password and Google Sign-In in **MELA App**.
> * **Firestore**: For real-time content updates and user-specific data.
> * **FCM**: To send targeted notifications (e.g., assignment alerts).
> * **Crashlytics**: To monitor and resolve runtime crashes.
>
> The integration of Firebase helped me build scalable backend functionality without server overhead.
> In one case, we reduced user complaints by **40%** after implementing Firebase Crashlytics to fix stability issues.

---

### ❓ 8. What is Clean Architecture and how have you applied it?

**🧠 How to Answer:**

* Define Clean Architecture and its key layers (UI, Domain, Data).
* Mention use of **UseCases**, **Repositories**, and **Dependency Injection**.
* Explain how it helped you in code scalability or testing.

**✅ Ideal Answer:**

> **Clean Architecture** separates concerns into distinct layers:
>
> * **UI Layer**: Only interacts with ViewModels and observes states.
> * **Domain Layer**: Contains business logic and UseCases.
> * **Data Layer**: Handles repositories, API services, and local storage.
>
> In the **UPAVP-PEMS App**, I applied Clean Architecture using **Hilt** for DI and **Coroutines** for async tasks.
>
> * UseCases helped isolate logic like "Search Property by ID" or "Upload Image".
> * The Repository pattern made it easy to switch between mock and real APIs for testing.
>
> This improved maintainability and enabled unit testing of business logic independently.

---

### ❓ 9. How did you integrate Google Maps in your application?

**🧠 How to Answer:**

* Explain which Maps APIs you used (e.g., **FusedLocationProvider**, **Polyline**, **MapFragment**).
* Talk about markers, permissions, and map interactions.
* Highlight specific features like real-time tracking or geo-fencing.

**✅ Ideal Answer:**

> In the **UPAVP-PEMS App**, I integrated **Google Maps API** for real-time property tracking.
>
> * Used **FusedLocationProviderClient** to fetch real-time user location.
> * Displayed markers for properties, using data from Firestore.
> * Enabled live updates using a ViewModel and Coroutines.
>
> This helped field agents precisely locate properties, cutting search time by **35%**.

---

### ❓ 10. You've solved 200+ DSA problems. How does this help in Android development?

**🧠 How to Answer:**

* Bridge the connection between DSA and real-world dev.
* Mention scenarios like data manipulation, optimization, and algorithmic thinking.
* Give examples (e.g., sorting a dataset for a RecyclerView or caching logic).

**✅ Ideal Answer:**

> Solving **200+ DSA problems** sharpened my algorithmic thinking and helped me write optimal code in Android development.
>
> For example, while implementing the **search feature** in the UPAVP-PEMS App, I used binary search to filter property lists efficiently.
>
> * Implemented **in-memory caching** with a hashmap to avoid repeated API calls.
> * Used DSA concepts like graphs and queues for navigation and notification logic.
>
> This ensures I write clean, efficient, and scalable code in performance-critical parts of the app.
