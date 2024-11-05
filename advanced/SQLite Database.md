# SQLite Database

## Overview

SQLite is a lightweight database engine that comes bundled with Android. It stores data in a structured format, making it a popular choice for local data storage in Android apps. SQLite operates in the device's internal storage and is highly efficient for apps that need to store relational data locally.

## Prebuilt Classes

### 1. **SQLiteOpenHelper**
- **Description:** A helper class to manage database creation and version management. It simplifies the process of managing database operations.
- **Usage:** You extend this class to create, update, or modify the database schema.
- **Key Methods:**
  - `onCreate(SQLiteDatabase db)`: Called when the database is created for the first time.
  - `onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion)`: Called when the database needs to be upgraded (e.g., adding new columns).
  
- **Code Example:**
  ```java
  public class MyDatabaseHelper extends SQLiteOpenHelper {
      private static final String DATABASE_NAME = "mydatabase.db";
      private static final int DATABASE_VERSION = 1;

      public MyDatabaseHelper(Context context) {
          super(context, DATABASE_NAME, null, DATABASE_VERSION);
      }

      @Override
      public void onCreate(SQLiteDatabase db) {
          String CREATE_TABLE = "CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT, age INTEGER)";
          db.execSQL(CREATE_TABLE);
      }

      @Override
      public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
          db.execSQL("DROP TABLE IF EXISTS users");
          onCreate(db);
      }
  }
  ```

### 2. **SQLiteDatabase**
- **Description:** Provides methods to perform CRUD (Create, Read, Update, Delete) operations on the database.
- **Usage:** Used to execute SQL queries and manage transactions.
- **Key Methods:**
  - `insert(String table, String nullColumnHack, ContentValues values)`: Inserts a new row into the database.
  - `update(String table, ContentValues values, String whereClause, String[] whereArgs)`: Updates existing rows in the database.
  - `delete(String table, String whereClause, String[] whereArgs)`: Deletes rows from the database.
  - `query(String table, String[] columns, String selection, String[] selectionArgs, String groupBy, String having, String orderBy)`: Performs a SELECT query to retrieve data.
  - `rawQuery(String sql, String[] selectionArgs)`: Executes raw SQL queries.

- **Code Example (Inserting Data):**
  ```java
  SQLiteDatabase db = myDatabaseHelper.getWritableDatabase();
  ContentValues values = new ContentValues();
  values.put("name", "John");
  values.put("age", 25);
  db.insert("users", null, values);
  ```

- **Code Example (Retrieving Data):**
  ```java
  SQLiteDatabase db = myDatabaseHelper.getReadableDatabase();
  Cursor cursor = db.query("users", new String[]{"id", "name", "age"}, null, null, null, null, null);

  if (cursor.moveToFirst()) {
      do {
          int id = cursor.getInt(0);
          String name = cursor.getString(1);
          int age = cursor.getInt(2);
      } while (cursor.moveToNext());
  }
  cursor.close();
  ```

### 3. **ContentValues**
- **Description:** A key/value pair collection used to pass data to SQLiteDatabase methods like `insert()` and `update()`.
- **Usage:** Stores values that will be inserted or updated in the database.

- **Code Example:**
  ```java
  ContentValues values = new ContentValues();
  values.put("name", "Jane Doe");
  values.put("age", 30);
  ```

### 4. **Cursor**
- **Description:** Provides access to the result set returned by a query. It allows you to read the rows and columns of the result set.
- **Usage:** Used for traversing the results of database queries.
  
- **Key Methods:**
  - `moveToFirst()`: Moves the cursor to the first row of the result set.
  - `moveToNext()`: Moves the cursor to the next row.
  - `getInt(int columnIndex)`, `getString(int columnIndex)`: Fetches the value of the specified column.

- **Code Example:**
  ```java
  Cursor cursor = db.query("users", null, null, null, null, null, null);
  while (cursor.moveToNext()) {
      int id = cursor.getInt(cursor.getColumnIndex("id"));
      String name = cursor.getString(cursor.getColumnIndex("name"));
  }
  cursor.close();
  ```

## Real-Life Example: Storing User Profiles

An app may store user profile data such as name, age, and email address in an SQLite database.

### Example Workflow:
1. Create a `User` table when the app is launched for the first time.
2. When a new user signs up, their details are inserted into the `User` table.
3. When the user logs in, the app queries the database to retrieve the user's details.

**Code Example:**

1. **Creating the User Table:**
   ```java
   @Override
   public void onCreate(SQLiteDatabase db) {
       String CREATE_USER_TABLE = "CREATE TABLE user (id INTEGER PRIMARY KEY, name TEXT, email TEXT)";
       db.execSQL(CREATE_USER_TABLE);
   }
   ```

2. **Inserting a New User:**
   ```java
   ContentValues values = new ContentValues();
   values.put("name", "John Doe");
   values.put("email", "john.doe@example.com");
   db.insert("user", null, values);
   ```

3. **Querying the User Data:**
   ```java
   Cursor cursor = db.query("user", new String[]{"name", "email"}, "id=?", new String[]{"1"}, null, null, null);
   if (cursor.moveToFirst()) {
       String name = cursor.getString(0);
       String email = cursor.getString(1);
   }
   cursor.close();
   ```

## Advanced Features

- **Transactions:** To ensure data consistency, you can wrap multiple database operations in a transaction.
  ```java
  db.beginTransaction();
  try {
      // Perform multiple database operations
      db.setTransactionSuccessful();
  } finally {
      db.endTransaction();
  }
  ```

- **Raw Queries:** If you need more control over the queries, you can use `rawQuery()` to execute SQL queries directly.
  ```java
  Cursor cursor = db.rawQuery("SELECT * FROM user WHERE age > ?", new String[]{"18"});
  ```

## Summary

SQLite in Android is a powerful and efficient way to store structured data locally. By utilizing classes like `SQLiteOpenHelper`, `SQLiteDatabase`, `Cursor`, and `ContentValues`, you can perform efficient database operations such as data insertion, updates, and queries.

