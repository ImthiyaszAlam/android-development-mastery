# Room Database

## Overview

Room is a persistence library that provides an abstraction layer over SQLite to allow for more robust database access while harnessing the full power of SQLite. It simplifies database interactions and helps you to avoid boilerplate code and potential errors.

## Prebuilt Classes and Interfaces

### 1. **RoomDatabase**
- **Description:** The base class for the Room database. It serves as the main access point for the underlying SQLite database.
- **Usage:** Extend this class to create a database instance.
- **Code Example:**
  ```java
  @Database(entities = {User.class}, version = 1)
  public abstract class AppDatabase extends RoomDatabase {
      public abstract UserDao userDao();
  }
  ```

### 2. **Entity**
- **Description:** Annotation to define a table within the database. Each class marked with `@Entity` represents a table.
- **Usage:** Annotate your data model classes with `@Entity` to represent a table in the database.
- **Code Example:**
  ```java
  @Entity
  public class User {
      @PrimaryKey
      public int uid;
      @ColumnInfo(name = "first_name")
      public String firstName;
      @ColumnInfo(name = "last_name")
      public String lastName;
  }
  ```

### 3. **Dao (Data Access Object)**
- **Description:** Interface or abstract class containing methods that access the database. These methods must be annotated with Room annotations to define the SQL queries.
- **Usage:** Define database operations (CRUD operations) in DAO interfaces.
- **Code Example:**
  ```java
  @Dao
  public interface UserDao {
      @Insert
      void insert(User user);
      
      @Query("SELECT * FROM user")
      List<User> getAllUsers();
      
      @Delete
      void delete(User user);
  }
  ```

### 4. **RoomDatabase.Builder**
- **Description:** Builder class to create an instance of the Room database.
- **Usage:** Use this class to build and obtain an instance of the Room database.
- **Code Example:**
  ```java
  AppDatabase db = Room.databaseBuilder(getApplicationContext(),
          AppDatabase.class, "database-name").build();
  ```

### 5. **Migration**
- **Description:** Handles database schema changes and migrations from one version to another.
- **Usage:** Define migration strategies to update the database schema.
- **Code Example:**
  ```java
  Migration MIGRATION_1_2 = new Migration(1, 2) {
      @Override
      public void migrate(@NonNull SupportSQLiteDatabase database) {
          database.execSQL("ALTER TABLE user ADD COLUMN age INTEGER");
      }
  };
  
  AppDatabase db = Room.databaseBuilder(getApplicationContext(),
          AppDatabase.class, "database-name")
          .addMigrations(MIGRATION_1_2)
          .build();
  ```

## Key Methods

### **insert()**
- **Description:** Inserts one or more entities into the database.
- **Usage:** Use this method to add data to the database.
- **Code Example:** See `UserDao` interface example above.

### **update()**
- **Description:** Updates an existing entity in the database.
- **Usage:** Use this method to modify existing records.
- **Code Example:**
  ```java
  @Dao
  public interface UserDao {
      @Update
      void update(User user);
  }
  ```

### **delete()**
- **Description:** Deletes an entity from the database.
- **Usage:** Use this method to remove data from the database.
- **Code Example:** See `UserDao` interface example above.

### **getAll()**
- **Description:** Retrieves all entities of a specific type from the database.
- **Usage:** Use this method to fetch data from the database.
- **Code Example:** See `UserDao` interface example above.

## Real-Life Examples

1. **User Management System:**
   - Store user information such as name, email, and age in a local database.

   **Code Example:**
   ```java
   @Entity
   public class User {
       @PrimaryKey(autoGenerate = true)
       public int uid;
       @ColumnInfo(name = "first_name")
       public String firstName;
       @ColumnInfo(name = "last_name")
       public String lastName;
   }
   
   @Dao
   public interface UserDao {
       @Insert
       void insert(User user);
       
       @Query("SELECT * FROM user WHERE uid = :userId")
       User getUserById(int userId);
   }
   ```

2. **Notes Application:**
   - Save and retrieve notes or to-do items, with fields like title, description, and date.

   **Code Example:**
   ```java
   @Entity
   public class Note {
       @PrimaryKey(autoGenerate = true)
       public int id;
       public String title;
       public String description;
       public Date date;
   }
   
   @Dao
   public interface NoteDao {
       @Insert
       void insert(Note note);
       
       @Query("SELECT * FROM note")
       List<Note> getAllNotes();
   }
   ```

3. **Task Tracking:**
   - Track tasks with due dates, statuses, and priorities.

   **Code Example:**
   ```java
   @Entity
   public class Task {
       @PrimaryKey(autoGenerate = true)
       public int taskId;
       public String taskName;
       public Date dueDate;
       public boolean isCompleted;
   }
   
   @Dao
   public interface TaskDao {
       @Insert
       void insert(Task task);
       
       @Query("SELECT * FROM task WHERE isCompleted = 0")
       List<Task> getPendingTasks();
   }
   ```

## Summary

Room Database simplifies database interactions and management in Android by providing a high-level API over SQLite. It helps to ensure type safety, reduce boilerplate code, and manage database migrations smoothly.

---

### Category
Room Database is categorized as **Advanced** due to its detailed setup, schema management, and the complexity involved in handling database migrations and interactions.
