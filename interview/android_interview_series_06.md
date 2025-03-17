

## **1. Can you walk me through your experience with migrating Java code to Kotlin? What challenges did you face, and how did you overcome them?**

### **Answer:**
At **Surveykshan**, I led the migration of the **Research Data Collection App** from Java to Kotlin to improve maintainability and performance. 

**Challenges Faced & Solutions:**
1. **Null Safety Issues:**  
   - Java allows `null`, but Kotlin has null safety. I resolved this using **nullable types (`?`)** and **safe calls (`?.`)**.
   
2. **SAM (Single Abstract Method) Conversions:**  
   - Java requires anonymous classes for functional interfaces, but Kotlin simplifies this with **lambda expressions**.
   
3. **Coroutines Integration:**  
   - I replaced Java's Threading (Executors) with Kotlin **Coroutines + Retrofit** for better async handling.

**Impact:**  
- Reduced **boilerplate code by 40%**, improved **app performance**, and enhanced **readability**.  

---

## **2. How did you improve app efficiency by 30% at Surveykshan?**

### **Answer:**
I optimized the **background data sync process** and **API handling** using:
1. **WorkManager for Background Sync**  
   - Ensured efficient **periodic updates** without draining the battery.  

2. **Retrofit + Coroutines for API Calls**  
   - Replaced traditional AsyncTask with Coroutines, reducing API response time.  

3. **AWS for File Handling**  
   - Moved **large file storage** to AWS S3, reducing local storage overhead.

**Result:**  
- Improved app performance by **30%**, reduced API response time by **40%**, and enhanced user experience.

---

## **3. Can you explain how you integrated Firebase Crashlytics and how it helped reduce crashes by 40%?**

### **Answer:**
At **Surveykshan**, I implemented **Firebase Crashlytics** for real-time error tracking.

**Steps Taken:**
1. **Integrated Crashlytics SDK**  
   - Added dependencies and enabled **automatic crash reports**.

2. **Identified & Fixed Crashes**  
   - Analyzed Crashlytics logs and identified a **memory leak** in image handling.
   - Fixed it using **WeakReference** and optimized image loading with **Glide**.

3. **Proactive Monitoring & Fixing**  
   - Implemented **custom logs** to track API failures.
   - Fixed **UI thread blocking issues** using Coroutines.

**Impact:**  
- Reduced crashes by **40%**, improved app stability, and ensured a seamless user experience.

---

## **4. What architecture did you use in your projects, and why?**

### **Answer:**
I used **MVVM + Clean Architecture** in my projects.

1. **MVVM Benefits:**
   - **Separation of concerns**: UI (ViewModel), Data (Repository), Business Logic (UseCases).
   - **Lifecycle-aware ViewModel** prevents memory leaks.

2. **Clean Architecture Benefits:**
   - **Domain Layer**: UseCases for business logic.
   - **Data Layer**: Repository pattern for API calls.
   - **Presentation Layer**: ViewModels for UI.

**Example:**  
In the **Mela App**, I used **MVVM + Repository Pattern** to separate concerns, improving code maintainability.

---

## **5. How did you optimize API calls in your projects?**

### **Answer:**
I used multiple techniques to **optimize API calls**:

1. **Retrofit with OkHttp Caching**  
   - Cached GET requests to **reduce redundant API calls**.  

2. **Coroutines for Asynchronous Calls**  
   - Handled API calls efficiently **without blocking the main thread**.

3. **Pagination with Paging 3**  
   - Implemented **lazy loading**, reducing API load by **50%**.

4. **Efficient API Response Handling**  
   - Used **sealed classes** for handling success & error responses gracefully.

**Result:**  
- **Reduced API response time by 40%**, improving app efficiency.

---

## **6. How did you implement Secure Authentication in the Mela App?**

### **Answer:**
I implemented **OAuth 2.0 & JWT-based authentication**.

1. **OAuth 2.0 for Third-Party Logins**
   - Used **Google Sign-In & Firebase Auth**.

2. **JWT Token-Based Authentication**
   - Implemented secure login with **token-based access control**.

3. **Best Security Practices**
   - Used **encrypted shared preferences** for storing tokens.
   - Implemented **refresh tokens** for maintaining session security.

**Impact:**  
- Achieved **99.9% secure logins** across multiple user roles.

---

## **7. Can you explain how you integrated Google Maps API in your projects?**

### **Answer:**
At **UPAVP-PEMS**, I integrated **Google Maps API** for real-time location tracking.

1. **Map Integration**  
   - Implemented **Marker & Polyline features** for visual representation.

2. **Geocoding & Reverse Geocoding**  
   - Converted latitude/longitude to addresses for user-friendly UI.

3. **Optimized Location Fetching**  
   - Used **FusedLocationProvider** for **battery-efficient location updates**.

**Impact:**  
- Improved **tracking accuracy** and reduced **data retrieval time by 35%**.

---

## **8. How do you handle memory leaks in Android?**

### **Answer:**
I use multiple techniques to **prevent memory leaks**:

1. **Avoid Static Context References**  
   - Used **WeakReference** for background tasks.

2. **Lifecycle-Aware Components**  
   - Used **ViewModels** to avoid unnecessary UI object retention.

3. **LeakCanary for Detection**  
   - Used **LeakCanary** to identify **memory leaks** and fixed them proactively.

4. **Proper Resource Cleanup**  
   - Released unused listeners & observers.

---

## **9. Can you discuss a challenging bug you encountered and how you solved it?**

### **Answer:**
At **CloudSect**, I faced a **UI freezing issue** when loading large JSON data.

### **Issue:**  
- The app UI was **lagging** when parsing **large JSON responses**.

### **Solution:**  
1. **Used Coroutines (Dispatchers.IO)**  
   - Moved **JSON parsing to a background thread**.

2. **Optimized JSON Parsing**  
   - Used **Gson & Moshi** instead of manual parsing.

3. **Implemented Pagination (Paging 3)**  
   - Loaded data in chunks instead of a **single large response**.

**Impact:**  
- Reduced UI lag, making app **60% more responsive**.

---

## **10. Why should we hire you for this role?**

### **Answer:**
I bring **strong Android development expertise**, **problem-solving skills**, and **hands-on experience** in building scalable apps.

1. **Proven Technical Skills:**  
   - Worked on **MVVM, Firebase, Jetpack Components, Google Maps API, AWS**.
   - Solved **200+ DSA problems**, ensuring algorithmic expertise.

2. **Real-World Impact:**  
   - Optimized APIs (**40% faster**), reduced crashes (**40% less**), improved user engagement (**30% increase**).

3. **Growth Mindset & Adaptability:**  
   - Passionate about **writing efficient, scalable code** and keeping up with **latest Android trends**.

I am confident that my **technical acumen, real-world project experience, and problem-solving mindset** align perfectly with your team’s goals.

---

### **Final Tips for Cracking FAANG/MAANG Interviews**
✅ **Practice DSA Daily** (Focus on Trees, Graphs, DP, Arrays).  
✅ **Master System Design Concepts** (Scalability, Caching, Load Balancing).  
✅ **Mock Interviews** (HLD, LLD, Android Scenarios).  
✅ **Stay Updated** with **latest Android trends** (Jetpack Compose, Modularization).  
