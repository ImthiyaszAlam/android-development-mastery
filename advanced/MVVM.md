# MVVM (Model-View-ViewModel)

## What is MVVM?

MVVM (Model-View-ViewModel) is a design pattern used in Android development to separate concerns in the application architecture. It divides the application into three main components:

- **Model:** Represents the data and business logic of the application. It is responsible for retrieving data, processing it, and providing it to the ViewModel.
- **View:** Displays the data and handles user interactions. It observes changes in the ViewModel and updates the UI accordingly.
- **ViewModel:** Acts as a bridge between the Model and the View. It retrieves data from the Model and prepares it for display in the View. It also handles user interactions and updates the Model as needed.

## Why Use MVVM?

- **Separation of Concerns:** MVVM separates the UI (View) from the business logic (ViewModel) and data (Model), making the codebase easier to manage and test.
- **Testability:** ViewModels can be tested independently from the View, facilitating unit testing of business logic.
- **Reusability:** The ViewModel can be reused across different Views or activities.
- **Maintainability:** Changes to the UI or business logic can be made independently without affecting the other parts of the application.

## How MVVM Works

1. **View:** Displays data to the user and sends user actions (like button clicks) to the ViewModel.
2. **ViewModel:** Processes user actions, interacts with the Model to fetch or update data, and prepares the data for the View. It also exposes LiveData or Observable fields that the View can observe.
3. **Model:** Contains the data and business logic. It retrieves data from sources like databases or network and provides it to the ViewModel.

## Prebuilt Classes and Interfaces

### 1. **ViewModel**
- **Description:** A class designed to store and manage UI-related data in a lifecycle-conscious way. It survives configuration changes such as screen rotations.
- **Usage:** Extend this class to create your ViewModel.
- **Code Example:**
  ```java
  public class MyViewModel extends ViewModel {
      private MutableLiveData<String> data;
      
      public LiveData<String> getData() {
          if (data == null) {
              data = new MutableLiveData<>();
              loadData();
          }
          return data;
      }
      
      private void loadData() {
          // Load data from repository
      }
  }
  ```

### 2. **LiveData**
- **Description:** A lifecycle-aware data holder class that allows data to be observed. It ensures that the UI only updates when it is in an active lifecycle state.
- **Usage:** Use LiveData to observe changes in data and update the UI accordingly.
- **Code Example:**
  ```java
  LiveData<String> liveData = viewModel.getData();
  liveData.observe(this, new Observer<String>() {
      @Override
      public void onChanged(@Nullable String data) {
          // Update UI with new data
      }
  });
  ```

### 3. **DataBinding**
- **Description:** A library that allows you to bind UI components in your layouts to data sources in your app using a declarative format.
- **Usage:** Use DataBinding to automatically update the UI when data changes.
- **Code Example:**
  ```xml
  <layout xmlns:android="http://schemas.android.com/apk/res/android">
      <data>
          <variable
              name="viewModel"
              type="com.example.MyViewModel" />
      </data>
      <TextView
          android:text="@{viewModel.data}" />
  </layout>
  ```

### 4. **Repository**
- **Description:** A class that manages data operations and provides a clean API for data access to the ViewModel.
- **Usage:** Use this class to abstract data sources (e.g., network, database) and provide data to the ViewModel.
- **Code Example:**
  ```java
  public class UserRepository {
      private UserDao userDao;
      
      public UserRepository(Application application) {
          AppDatabase db = AppDatabase.getDatabase(application);
          userDao = db.userDao();
      }
      
      public LiveData<User> getUser(int userId) {
          return userDao.getUser(userId);
      }
  }
  ```

## Key Concepts

### **Data Binding**
- **Description:** Allows you to bind UI components to data sources in XML layouts, reducing boilerplate code.
- **Usage:** Use data binding to bind UI elements directly to ViewModel properties.
- **Code Example:** See `DataBinding` class example above.

### **LiveData and Observers**
- **Description:** LiveData objects notify observers about data changes, ensuring that the UI components react accordingly.
- **Usage:** Use LiveData in your ViewModel to expose data and observe changes in your View.
- **Code Example:** See `LiveData` class example above.

### **Repository Pattern**
- **Description:** A design pattern that abstracts data access logic and provides a unified API for accessing data.
- **Usage:** Use repositories to fetch and manage data from different sources (network, database).
- **Code Example:** See `Repository` class example above.

## Real-Life Examples

1. **Fetching User Data:**
   - Fetch user data from a network or database and display it in the UI.

   **Code Example:**
   ```java
   // ViewModel
   public class UserViewModel extends ViewModel {
       private UserRepository repository;
       private LiveData<User> user;

       public UserViewModel() {
           repository = new UserRepository();
           user = repository.getUser(1);
       }
       
       public LiveData<User> getUser() {
           return user;
       }
   }
   
   // Activity
   userViewModel.getUser().observe(this, new Observer<User>() {
       @Override
       public void onChanged(@Nullable User user) {
           // Update UI with user data
       }
   });
   ```

2. **User Authentication:**
   - Manage user authentication logic and update the UI based on authentication state.

   **Code Example:**
   ```java
   // ViewModel
   public class AuthViewModel extends ViewModel {
       private MutableLiveData<Boolean> isAuthenticated;
       
       public LiveData<Boolean> getIsAuthenticated() {
           if (isAuthenticated == null) {
               isAuthenticated = new MutableLiveData<>();
               checkAuthStatus();
           }
           return isAuthenticated;
       }
       
       private void checkAuthStatus() {
           // Check if user is authenticated
           isAuthenticated.setValue(true); // or false
       }
   }
   
   // Activity
   authViewModel.getIsAuthenticated().observe(this, new Observer<Boolean>() {
       @Override
       public void onChanged(@Nullable Boolean isAuthenticated) {
           if (isAuthenticated) {
               // Navigate to main activity
           } else {
               // Show login screen
           }
       }
   });
   ```

## Summary

MVVM is a powerful architecture pattern for Android development that separates concerns into distinct components, making your codebase more maintainable, testable, and reusable. By using ViewModels, LiveData, and DataBinding, you can build responsive and robust applications.

---

### Category
MVVM is categorized as **Advanced** due to its complexity in managing data flow and the integration of multiple components.
