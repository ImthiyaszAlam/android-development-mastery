# Fragment Lifecycle

## What is a Fragment?

A **Fragment** represents a reusable portion of the UI in an Android activity. It has its own lifecycle, which is closely tied to the lifecycle of its hosting Activity. A Fragment can be added or removed while the Activity is running, and it can be used in different activities, allowing for a modular and flexible user interface.

### Why Use Fragments?

- **Modularity:** You can split complex activities into reusable pieces of functionality.
- **UI Adaptability:** Fragments can be used to design responsive UIs that work well across both small (phones) and large (tablets) screens.
- **Lifecycle Management:** Fragments have their own lifecycle, separate from the Activity, giving you more control over managing the state.

### How to Use Fragments?

Fragments are used within Activities. You can add, remove, replace, and dynamically interact with them using the **FragmentManager**. A fragment's lifecycle works in tandem with the activity lifecycle, but it has its own specific lifecycle methods.

## Fragment Lifecycle Methods

The fragment lifecycle consists of several callback methods that get triggered during different stages of a fragment's existence.

### Lifecycle States

1. **onAttach(Context context):** Fragment is attached to the Activity.
2. **onCreate(Bundle savedInstanceState):** Fragment is created (initialization of data, UI components).
3. **onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState):** UI is drawn for the Fragment.
4. **onActivityCreated(Bundle savedInstanceState):** Fragment’s activity has been created.
5. **onStart():** Fragment becomes visible.
6. **onResume():** Fragment is now active and interactive.
7. **onPause():** Fragment goes into a paused state, still visible but not interactive.
8. **onStop():** Fragment is no longer visible.
9. **onDestroyView():** Fragment's view is destroyed (clean up resources tied to the view).
10. **onDestroy():** Fragment is destroyed.
11. **onDetach():** Fragment is detached from the Activity.

### Prebuilt Functions (Lifecycle Methods)

#### 1. **onAttach(Context context)**
   - **Description:** Called when the fragment has been attached to the activity.
   - **Code Example:**
     ```java
     @Override
     public void onAttach(Context context) {
         super.onAttach(context);
         // Initialize resources needed for the fragment
     }
     ```

#### 2. **onCreate(Bundle savedInstanceState)**
   - **Description:** Called when the fragment is being created. Good for initializing data.
   - **Code Example:**
     ```java
     @Override
     public void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);
         // Initialize fragment-level resources here
     }
     ```

#### 3. **onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState)**
   - **Description:** Called to create the view hierarchy associated with the fragment.
   - **Code Example:**
     ```java
     @Override
     public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
         // Inflate the fragment layout
         return inflater.inflate(R.layout.fragment_example, container, false);
     }
     ```

#### 4. **onStart()**
   - **Description:** Called when the fragment becomes visible to the user.
   - **Code Example:**
     ```java
     @Override
     public void onStart() {
         super.onStart();
         // The fragment is now visible
     }
     ```

#### 5. **onResume()**
   - **Description:** Called when the fragment is visible and active, ready for user interaction.
   - **Code Example:**
     ```java
     @Override
     public void onResume() {
         super.onResume();
         // Fragment is now interactive
     }
     ```

#### 6. **onPause()**
   - **Description:** Called when the fragment is no longer interactive but still visible.
   - **Code Example:**
     ```java
     @Override
     public void onPause() {
         super.onPause();
         // Handle fragment going to paused state
     }
     ```

#### 7. **onStop()**
   - **Description:** Called when the fragment is no longer visible to the user.
   - **Code Example:**
     ```java
     @Override
     public void onStop() {
         super.onStop();
         // Fragment is no longer visible
     }
     ```

#### 8. **onDestroyView()**
   - **Description:** Called when the fragment's UI is no longer needed and can be cleaned up.
   - **Code Example:**
     ```java
     @Override
     public void onDestroyView() {
         super.onDestroyView();
         // Clean up resources related to the view
     }
     ```

#### 9. **onDestroy()**
   - **Description:** Called to perform final cleanup when the fragment is being destroyed.
   - **Code Example:**
     ```java
     @Override
     public void onDestroy() {
         super.onDestroy();
         // Final cleanup
     }
     ```

#### 10. **onDetach()**
   - **Description:** Called when the fragment is detached from its hosting activity.
   - **Code Example:**
     ```java
     @Override
     public void onDetach() {
         super.onDetach();
         // Fragment is now detached
     }
     ```

## Prebuilt Classes and Interfaces

### **FragmentManager**
- **Description:** Manages the fragments within an activity. It allows adding, removing, or replacing fragments dynamically.
- **Usage:** Use `FragmentManager` to handle fragment transactions.
- **Code Example:**
  ```java
  FragmentManager fragmentManager = getSupportFragmentManager();
  FragmentTransaction transaction = fragmentManager.beginTransaction();
  transaction.replace(R.id.fragment_container, new ExampleFragment());
  transaction.commit();
  ```

### **FragmentTransaction**
- **Description:** Used to perform fragment operations like adding, replacing, or removing fragments.
- **Usage:** Begin a transaction, perform operations, and then commit the transaction.
- **Code Example:**
  ```java
  FragmentTransaction transaction = fragmentManager.beginTransaction();
  transaction.add(R.id.container, new MyFragment());
  transaction.commit();
  ```

### **FragmentActivity**
- **Description:** An activity that can host fragments. It provides methods to interact with fragments.
- **Usage:** Extend this class when using fragments in your activity.
- **Code Example:**
  ```java
  public class MyFragmentActivity extends FragmentActivity {
      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);
      }
  }
  ```

### **DialogFragment**
- **Description:** A fragment that displays a dialog window.
- **Usage:** Use `DialogFragment` to show dialogs inside an activity.
- **Code Example:**
  ```java
  public class MyDialogFragment extends DialogFragment {
      @NonNull
      @Override
      public Dialog onCreateDialog(Bundle savedInstanceState) {
          AlertDialog.Builder builder = new AlertDialog.Builder(getActivity());
          builder.setMessage("Example Dialog");
          return builder.create();
      }
  }
  ```

## Real-Life Example: Fragment with a List

### Code Example:

```java
public class ListFragment extends Fragment {
    @Nullable
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_list, container, false);
        
        // Set up a RecyclerView in the fragment
        RecyclerView recyclerView = view.findViewById(R.id.recycler_view);
        recyclerView.setLayoutManager(new LinearLayoutManager(getActivity()));
        recyclerView.setAdapter(new MyAdapter());
        
        return view;
    }
}
```

In this example, a fragment hosts a `RecyclerView` to display a list. You can dynamically replace this fragment with another in the parent activity using `FragmentManager`.

## Summary of Concepts

- **Fragment Lifecycle:** Handle different lifecycle states of a fragment (onCreate, onStart, onResume, onPause, onDestroy).
- **FragmentManager:** Manage and manipulate fragments dynamically.
- **FragmentTransaction:** Perform fragment transactions like adding, replacing, or removing fragments.
- **FragmentActivity:** An activity that can host fragments.
- **DialogFragment:** A specialized fragment to display dialogs.
