

### **1️⃣ Clean Architecture & MVVM**
#### **Q1: Why did you choose Clean Architecture over MVC or MVP?**  
✅ **Expected Answer:**  
- MVC and MVP tightly couple UI and business logic, making testing difficult.  
- Clean Architecture **separates concerns**, **improves scalability**, and allows **independent testing of each layer**.  
- Reduces **code duplication**, making refactoring easier.  

---
#### **Q2: How would you modify your Clean Architecture approach if your app had to support offline mode?**  
✅ **Expected Answer:**  
- Introduce a **Repository pattern** to manage offline data sync.  
- Implement **Room Database** for local storage.  
- Use **WorkManager** for background sync.  
- Use **NetworkBoundResource** to decide between local and remote data.  

---

### **2️⃣ API Optimization & Performance**
#### **Q3: You mentioned optimizing API calls with caching. What challenges did you face?**  
✅ **Expected Answer:**  
- Handling **stale cache** (used Cache-Control headers).  
- **Edge cases with pagination** (stored separate cache keys for each page).  
- Ensuring cache doesn’t increase **memory footprint** (used LRUCache).  

---
#### **Q4: If your API takes too long to respond, how would you handle that?**  
✅ **Expected Answer:**  
- Set **timeouts** in Retrofit/OkHttp.  
- Implement **retry mechanism** with **exponential backoff**.  
- Use **WebSockets for real-time updates** instead of polling.  

---

### **3️⃣ Memory Management & Performance**
#### **Q5: How would you debug and fix a memory leak in a production Android app?**  
✅ **Expected Answer:**  
1. **Use LeakCanary** to detect leaks.  
2. Check for **static references** holding Activity contexts.  
3. Avoid memory leaks in **ViewModels** by clearing LiveData.  
4. Ensure **onDestroy()** releases listeners, observers, and handlers.  

---
#### **Q6: How would you improve an Android app's frame rate and rendering performance?**  
✅ **Expected Answer:**  
- Use **ViewBinding** instead of `findViewById()`.  
- Avoid **deep view hierarchies** (use ConstraintLayout).  
- **Offload heavy computations** to coroutines (Dispatchers.IO).  
- Use **GPU Profiler** to optimize rendering bottlenecks.  

---

### **4️⃣ Security & Authentication**
#### **Q7: How do you securely store sensitive user data in an Android app?**  
✅ **Expected Answer:**  
- Use **EncryptedSharedPreferences** for local storage.  
- Store tokens in **Android Keystore** (not SharedPreferences).  
- Use **OAuth 2.0 & JWT** instead of storing passwords locally.  

---
#### **Q8: How would you handle API rate limiting and prevent abuse in a mobile app?**  
✅ **Expected Answer:**  
- Implement **API Throttling** (limit API calls per second).  
- Use **CAPTCHA verification** for suspicious behavior.  
- Implement **JWT-based authentication** and refresh tokens securely.  

---

### **5️⃣ Crash Handling & Debugging**
#### **Q9: How would you handle a crash that happens only on specific Android devices?**  
✅ **Expected Answer:**  
- Use **Firebase Crashlytics** to check stack traces & device logs.  
- Identify **device-specific issues** (low RAM, custom OEM modifications).  
- Implement **fallback mechanisms** for edge cases (e.g., `try-catch` around device-specific APIs).  

---
#### **Q10: How would you ensure an app doesn't crash due to bad network conditions?**  
✅ **Expected Answer:**  
- Implement **offline-first** behavior (cache results, retry failed requests).  
- Show a **graceful fallback UI** instead of a crash screen.  
- Use **ConnectivityManager** to check network status before API calls.  

---

 
Interviewers often follow up with:  
- **"What trade-offs did you consider?"**  
- **"Can you improve your solution?"**  
- **"How does this compare to another approach?"**  
