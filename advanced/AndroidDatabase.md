# Databases in Android: SQLite, Room, SharedPreferences

## 1. **SQLite**

### What:
SQLite is a lightweight relational database embedded within Android. It provides standard SQL syntax and is useful for local data storage in applications where structured data needs to be persisted.

### Why:
SQLite allows you to handle complex queries, joins, and transactions with ease. It is used when your application requires a relational database to manage structured data with rows and columns.

### How:
SQLite operates through the `SQLiteOpenHelper` class in Android, which helps manage database creation and version management. You define the schema using SQL statements, and you can perform CRUD operations (Create, Read, Update, Delete) with SQL queries.

### Prebuilt Classes and Functions:
- **SQLiteOpenHelper**: Manages database creation and version management.
  - Methods:
    - `onCreate(SQLiteDatabase db)`: Called when the database is first created.
    - `onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion)`: Handles upgrades to the database schema.
  - Code Example:
    ```java
    public class MyDatabaseHelper extends SQLiteOpenHelper {
        private static final String DATABASE_NAME = "mydb.db";
        private static final int DATABASE_VERSION = 1;

        public MyDatabaseHelper(Context context) {
            super(context, DATABASE_NAME, null, DATABASE_VERSION);
        }

        @Override
        public void onCreate(SQLiteDatabase db) {
            db.execSQL("CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER);");
        }

        @Override
        public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
            db.execSQL("DROP TABLE IF EXISTS users");
            onCreate(db);
        }
    }
    ```
- **SQLiteDatabase**: Provides methods to perform SQL operations.
  - `execSQL()`: Executes SQL commands (e.g., create table, insert data).
  - `query()`: Runs select queries.
  - `insert(), update(), delete()`: Performs basic CRUD operations.

### Real-Life Example:
- **Use Case**: Storing a user’s profile information in a local database.
  ```java
  SQLiteDatabase db = myDatabaseHelper.getWritableDatabase();
  ContentValues values = new ContentValues();
  values.put("name", "John");
  values.put("age", 30);
  db.insert("users", null, values);
  ```

### Category:
- **Basic**: SQLite falls under the basics of Android development as it forms the foundation of local database handling.

---

## 2. **Room**

### What:
Room is an abstraction layer over SQLite that provides a more manageable way of working with SQLite databases by reducing boilerplate code. It also provides compile-time checking for SQL queries, making it more type-safe and easier to debug.

### Why:
Room eliminates the need to write complex and repetitive SQLite code. It also integrates with LiveData, ViewModel, and RxJava, making it ideal for modern Android development.

### How:
Room is based on annotations to define the database schema and DAO (Data Access Object) patterns for database operations. It simplifies migrations, queries, and data handling.

### Prebuilt Classes and Functions:
- **RoomDatabase**: Abstract class to define the database and get DAOs.
  - `@Database(entities = {YourEntity.class}, version = 1)`
  - `public abstract YourDao yourDao();`
  - Code Example:
    ```java
    @Database(entities = {User.class}, version = 1)
    public abstract class AppDatabase extends RoomDatabase {
        public abstract UserDao userDao();
    }
    ```

- **Dao**: An interface that defines database operations.
  - `@Insert`: For inserting records.
  - `@Query`: For custom SQL queries.
  - `@Delete`: For deleting records.
  - Code Example:
    ```java
    @Dao
    public interface UserDao {
        @Insert
        void insert(User user);

        @Query("SELECT * FROM user WHERE userId = :id")
        User getUserById(int id);
    }
    ```

- **Entity**: Annotates the class to represent a table in the database.
  - Code Example:
    ```java
    @Entity
    public class User {
        @PrimaryKey
        public int id;
        public String name;
        public int age;
    }
    ```

- **RoomDatabase.Builder**: To create and get the RoomDatabase instance.
  - Code Example:
    ```java
    AppDatabase db = Room.databaseBuilder(getApplicationContext(),
            AppDatabase.class, "my-database").build();
    ```

### Real-Life Example:
- **Use Case**: An app that stores user login data.
  ```java
  User user = new User();
  user.id = 1;
  user.name = "John Doe";
  user.age = 28;

  db.userDao().insert(user);
  ```

### Category:
- **Advanced**: Room provides a robust and scalable solution for database management in Android apps, making it an advanced concept.

---

## 3. **SharedPreferences**

### What:
SharedPreferences is a lightweight key-value pair storage solution used for storing small amounts of primitive data such as integers, booleans, and strings.

### Why:
It’s efficient for storing small bits of data such as user settings, app preferences, or state information that doesn’t require a relational database or complex schema.

### How:
SharedPreferences stores data in XML format. You can retrieve and modify the data using `SharedPreferences` and `Editor` objects.

### Prebuilt Classes and Functions:
- **SharedPreferences**: Interface for accessing and modifying preference data.
  - `getString()`, `getInt()`, `getBoolean()`: Retrieve data from SharedPreferences.
  - `edit()`: Edit data in SharedPreferences.

- **Editor**: Interface used to make changes to SharedPreferences.
  - `putString()`, `putInt()`, `putBoolean()`: Save data to SharedPreferences.
  - `apply()`: Commit changes asynchronously.
  - `commit()`: Commit changes synchronously.

### Real-Life Example:
- **Use Case**: Saving user login status.
  ```java
  // Storing data
  SharedPreferences sharedPreferences = getSharedPreferences("MyPrefs", Context.MODE_PRIVATE);
  SharedPreferences.Editor editor = sharedPreferences.edit();
  editor.putBoolean("isLoggedIn", true);
  editor.apply();

  // Retrieving data
  boolean isLoggedIn = sharedPreferences.getBoolean("isLoggedIn", false);
  ```

### Category:
- **Basic**: SharedPreferences is categorized as a basic concept because it deals with simple, small-scale data storage without involving complex databases.

---

## Conclusion:

- **SQLite**: Basic – foundation of database handling with SQL queries.
- **Room**: Advanced – modern, abstracted, and scalable database management system.
- **SharedPreferences**: Basic – simple storage for key-value pairs.

These database options offer different levels of complexity and flexibility, allowing developers to choose the appropriate one based on
