# RESTful APIs

## What are RESTful APIs?

**RESTful APIs** (Representational State Transfer) are a set of conventions for creating web services that allow different software applications to communicate with each other over HTTP. RESTful APIs are designed to be stateless, scalable, and use standard HTTP methods (GET, POST, PUT, DELETE).

## Why Use RESTful APIs?

1. **Interoperability:** RESTful APIs allow different applications, often built with different technologies, to communicate and share data.
2. **Scalability:** Stateless communication and separation of client and server ensure scalability.
3. **Flexibility:** REST APIs use standard HTTP methods and status codes, making them easy to use and understand.
4. **Ease of Integration:** RESTful APIs are easy to integrate with various front-end technologies, including mobile apps.

## How to Implement RESTful APIs

1. **Define Endpoints:** Define the URIs (Uniform Resource Identifiers) for accessing resources. Each endpoint corresponds to a specific resource or action.
2. **Use HTTP Methods:** Implement CRUD operations using HTTP methods:
   - **GET:** Retrieve data
   - **POST:** Create data
   - **PUT:** Update data
   - **DELETE:** Remove data
3. **Handle Requests and Responses:** Process incoming requests and return responses in a standard format (usually JSON or XML).
4. **Authentication and Authorization:** Secure your API by implementing authentication (e.g., API keys, OAuth) and authorization mechanisms.

## Prebuilt Classes and Interfaces in Android

### 1. **Retrofit**
- **Description:** A type-safe HTTP client for Android and Java, used to make API calls and handle responses.
- **Usage:** Define an interface with annotated methods to describe your API endpoints.
- **Code Example:**
  ```java
  public interface ApiService {
      @GET("users/{user}")
      Call<User> getUser(@Path("user") String userId);
      
      @POST("users")
      Call<User> createUser(@Body User user);
  }
  
  Retrofit retrofit = new Retrofit.Builder()
      .baseUrl("https://api.example.com/")
      .addConverterFactory(GsonConverterFactory.create())
      .build();
  
  ApiService apiService = retrofit.create(ApiService.class);
  ```

### 2. **OkHttp**
- **Description:** An HTTP client for Android that can be used with Retrofit or standalone to make network requests.
- **Usage:** Use OkHttp for making network requests and handling responses.
- **Code Example:**
  ```java
  OkHttpClient client = new OkHttpClient();
  
  Request request = new Request.Builder()
      .url("https://api.example.com/users")
      .build();
  
  client.newCall(request).enqueue(new Callback() {
      @Override
      public void onFailure(Call call, IOException e) {
          // Handle failure
      }
      
      @Override
      public void onResponse(Call call, Response response) throws IOException {
          if (response.isSuccessful()) {
              String responseData = response.body().string();
              // Process response data
          }
      }
  });
  ```

### 3. **Gson**
- **Description:** A library for converting Java objects to JSON and vice versa.
- **Usage:** Use Gson for parsing JSON responses from RESTful APIs into Java objects.
- **Code Example:**
  ```java
  Gson gson = new Gson();
  String json = "{\"name\":\"John\",\"age\":30}";
  User user = gson.fromJson(json, User.class);
  ```

### 4. **LiveData**
- **Description:** A lifecycle-aware data holder that can be used to observe changes in data.
- **Usage:** Use LiveData to observe data from API calls and update the UI accordingly.
- **Code Example:**
  ```java
  public class UserRepository {
      private ApiService apiService;
      private MutableLiveData<User> userLiveData = new MutableLiveData<>();
      
      public UserRepository(ApiService apiService) {
          this.apiService = apiService;
      }
      
      public LiveData<User> getUser(String userId) {
          apiService.getUser(userId).enqueue(new Callback<User>() {
              @Override
              public void onResponse(Call<User> call, Response<User> response) {
                  if (response.isSuccessful()) {
                      userLiveData.setValue(response.body());
                  }
              }
              
              @Override
              public void onFailure(Call<User> call, Throwable t) {
                  // Handle failure
              }
          });
          return userLiveData;
      }
  }
  ```

### 5. **ViewModel**
- **Description:** A component that stores and manages UI-related data in a lifecycle-conscious way.
- **Usage:** Use ViewModel to manage data for your UI components and handle configuration changes.
- **Code Example:**
  ```java
  public class UserViewModel extends ViewModel {
      private UserRepository userRepository;
      private LiveData<User> userLiveData;
      
      public UserViewModel(UserRepository userRepository) {
          this.userRepository = userRepository;
      }
      
      public LiveData<User> getUser(String userId) {
          if (userLiveData == null) {
              userLiveData = userRepository.getUser(userId);
          }
          return userLiveData;
      }
  }
  ```

## Real-Life Examples

1. **Fetching User Profile:**
   - Retrieve user profile information from a remote server using Retrofit and display it in the app.

   **Code Example:**
   ```java
   @GET("users/{userId}")
   Call<User> getUserProfile(@Path("userId") String userId);
   ```

2. **Posting Data to Server:**
   - Submit form data or user-generated content to a server.

   **Code Example:**
   ```java
   @POST("users")
   Call<User> createUser(@Body User user);
   ```

3. **Handling Authentication:**
   - Implement login functionality and handle authentication tokens.

   **Code Example:**
   ```java
   @POST("auth/login")
   Call<AuthResponse> login(@Body LoginRequest loginRequest);
   ```

4. **Updating User Information:**
   - Update existing user details on the server.

   **Code Example:**
   ```java
   @PUT("users/{userId}")
   Call<User> updateUser(@Path("userId") String userId, @Body User user);
   ```

## Summary

RESTful APIs provide a standardized way to interact with backend services and retrieve or manipulate data. They are integral to modern mobile applications for accessing and managing remote resources.

---

### Category
RESTful APIs should be categorized as **Advanced** due to the complexity involved in setting up and managing network requests, data parsing, and integration with various components.
