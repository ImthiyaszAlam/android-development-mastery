# Dependency Injection in Android

## What is Dependency Injection?

Dependency Injection (DI) is a design pattern used to achieve Inversion of Control (IoC) between classes and their dependencies. It allows objects to be injected into a class rather than the class creating its own dependencies. This approach enhances modularity, testability, and maintainability of code.

## Why Use Dependency Injection?

- **Modularity:** Reduces tight coupling between classes by providing a clear interface for dependencies.
- **Testability:** Makes it easier to write unit tests by allowing mock implementations to be injected.
- **Maintainability:** Simplifies code changes by centralizing dependency management.
- **Scalability:** Facilitates the management of complex dependency graphs in larger applications.

## How Does Dependency Injection Work?

Dependency Injection works by providing dependencies to a class via constructor injection, field injection, or method injection. The DI framework manages the lifecycle and instantiation of these dependencies.

## Dagger

### Overview

Dagger is a compile-time Dependency Injection framework that generates code to handle DI. It requires defining components, modules, and providing methods for dependency injection.

### Prebuilt Classes and Interfaces

#### 1. **@Component**
- **Description:** An interface that defines a bridge between the provider of dependencies and the classes requesting them.
- **Usage:** Declare a component to specify which classes will be injected with dependencies.
- **Code Example:**
  ```java
  @Component(modules = AppModule.class)
  public interface AppComponent {
      void inject(MainActivity mainActivity);
  }
  ```

#### 2. **@Module**
- **Description:** A class that provides the dependencies. It includes methods annotated with `@Provides` to supply instances of dependencies.
- **Usage:** Create modules to define how to provide dependencies.
- **Code Example:**
  ```java
  @Module
  public class AppModule {
      @Provides
      @Singleton
      public UserRepository provideUserRepository() {
          return new UserRepository();
      }
  }
  ```

#### 3. **@Provides**
- **Description:** Annotation used in a module to specify a method that provides a dependency.
- **Usage:** Annotate methods in a module to define how to create and return dependencies.
- **Code Example:** See `@Module` example above.

#### 4. **@Inject**
- **Description:** Annotation used to request dependencies. Can be used on constructors, fields, and methods.
- **Usage:** Annotate constructors or fields where dependencies should be injected.
- **Code Example:**
  ```java
  public class UserProfile {
      private UserRepository userRepository;

      @Inject
      public UserProfile(UserRepository userRepository) {
          this.userRepository = userRepository;
      }
  }
  ```

### Real-Life Example

1. **User Authentication:**
   - Inject a repository and network service into a ViewModel for user authentication.

   **Code Example:**
   ```java
   @Module
   public class AuthModule {
       @Provides
       @Singleton
       public AuthService provideAuthService() {
           return new AuthService();
       }
   }
   
   @Component(modules = AuthModule.class)
   public interface AuthComponent {
       void inject(LoginViewModel loginViewModel);
   }
   
   public class LoginViewModel {
       private AuthService authService;

       @Inject
       public LoginViewModel(AuthService authService) {
           this.authService = authService;
       }
   }
   ```

## Hilt

### Overview

Hilt is a Dependency Injection library built on top of Dagger, designed to simplify DI setup in Android apps. It offers an easier way to manage DI with minimal configuration.

### Prebuilt Classes and Interfaces

#### 1. **@HiltAndroidApp**
- **Description:** Annotation applied to the Application class to trigger Hilt’s code generation and set up the DI framework.
- **Usage:** Annotate your Application class.
- **Code Example:**
  ```java
  @HiltAndroidApp
  public class MyApp extends Application {
  }
  ```

#### 2. **@AndroidEntryPoint**
- **Description:** Annotation used on Android components (activities, fragments, services) to enable dependency injection.
- **Usage:** Annotate components where you want to inject dependencies.
- **Code Example:**
  ```java
  @AndroidEntryPoint
  public class MainActivity extends AppCompatActivity {
      @Inject
      UserRepository userRepository;
  }
  ```

#### 3. **@Inject**
- **Description:** Similar to Dagger, used to request dependencies.
- **Usage:** Annotate constructors, fields, or methods where dependencies should be injected.
- **Code Example:** See Dagger example above.

#### 4. **@Module**
- **Description:** Similar to Dagger, used to define how to provide dependencies.
- **Usage:** Annotate modules to provide and configure dependencies.
- **Code Example:**
  ```java
  @Module
  @InstallIn(SingletonComponent.class)
  public class AppModule {
      @Provides
      @Singleton
      public UserRepository provideUserRepository() {
          return new UserRepository();
      }
  }
  ```

#### 5. **@InstallIn**
- **Description:** Annotation to specify the Hilt component where the module will be installed.
- **Usage:** Annotate modules to define the scope of dependencies.
- **Code Example:** See `@Module` example above.

### Real-Life Example

1. **Dependency Injection in Fragments:**
   - Inject a ViewModel into a Fragment using Hilt.

   **Code Example:**
   ```java
   @AndroidEntryPoint
   public class MyFragment extends Fragment {
       @Inject
       MyViewModel viewModel;

       @Override
       public View onCreateView(@NonNull LayoutInflater inflater, ViewGroup container,
                                Bundle savedInstanceState) {
           // Use viewModel
           return inflater.inflate(R.layout.fragment_layout, container, false);
       }
   }
   ```

## Summary

Dependency Injection is a powerful pattern for managing dependencies in Android applications, improving modularity, testability, and maintainability. Both Dagger and Hilt provide tools to simplify and manage DI, with Hilt offering a more streamlined setup process.
