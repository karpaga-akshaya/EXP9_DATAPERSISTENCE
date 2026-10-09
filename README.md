# EXP9_DATAPERSISTENCE

# Data Persistence Using SharedPreferences and SQLite

## 1. Experiment Title
Demonstrate data persistence using SharedPreferences and SQLite in an Android application.

## 2. Aim
To develop an Android application that stores and retrieves simple key-value data using SharedPreferences and structured student records using an SQLite database.

## 3. Software Requirements
- Android Studio
- Kotlin programming language
- XML for the user interface
- Android SDK and an emulator or Android device

## 4. Overview
This application demonstrates two Android data-persistence techniques:

- **SharedPreferences:** Stores a student's name as a key-value pair and restores it when the application is reopened.
- **SQLite:** Stores student records containing an ID, name, and course. The application inserts records and displays the saved records.

Both methods store data locally on the device. No external database server or additional library is required.

## 5. Application Features
1. Enter and save a name using SharedPreferences.
2. Display the saved name when the app starts.
3. Enter a student's name and course.
4. Insert student details into SQLite.
5. Display all stored student records.
6. Verify persistence by closing and reopening the app.

## 6. Project Structure
```text
DataPersistenceDemo/
├── app/
│   └── src/main/
│       ├── java/com/example/datapersistencedemo/
│       │   ├── MainActivity.kt
│       │   └── DatabaseHelper.kt
│       └── res/layout/
│           └── activity_main.xml
└── README.md
```

## 7. Implementation Summary

### SharedPreferences
The application opens a preferences file named `MyPreferences`. It saves the name with the key `student_name` using `putString()` and `apply()`. On startup, `getString()` retrieves the previously saved name.

Example:
```kotlin
val preferences = getSharedPreferences(
    "MyPreferences",
    MODE_PRIVATE
)
preferences.edit()
    .putString("student_name", name)
    .apply()
```

### SQLite
`DatabaseHelper.kt` extends `SQLiteOpenHelper` and manages a database named `StudentDB`. It creates a `students` table with the columns `id`, `name`, and `course`.

- `onCreate()` creates the table.
- `insertStudent()` inserts a student record using `ContentValues`.
- `getStudents()` reads records using a `Cursor`.
- `onUpgrade()` handles a database-version change. In this simple demonstration it drops and recreates the table, so existing records would be lost if the database version is increased.

## 8. Steps to Run
1. Open the project in Android Studio.
2. Confirm the package name is `com.example.datapersistencedemo`, or make the package declarations match your own project.
3. In `app/build.gradle.kts`, set `compileSdk` to an SDK platform installed on your computer (for example, `compileSdk = 35` if API 35 is installed). Set `targetSdk` to a suitable installed/available target, such as `35`.
4. Click **Sync Now** and wait for Gradle sync to finish.
5. Start an Android emulator or connect an Android phone with USB debugging enabled.
6. Click **Run**.
7. In the SharedPreferences section, enter a name and tap **SAVE NAME**.
8. In the SQLite section, enter a student name and course, then tap **ADD STUDENT**.
9. Close and reopen the app. Check that the saved name and student records still appear.

> Use SDK versions available in your Android SDK Manager. SharedPreferences and SQLite do not require a specific recent API level for this experiment.

## 9. Expected Output
Example:

```text
SharedPreferences
Saved Name: Akshay

SQLite Database
Students:
1. Akshay - MCA
2. Rahul - MBA
```

The displayed records depend on the values entered during testing.

## 10. Testing
- **Test 1:** Save a name and verify that it appears under “Saved Name”.
- **Test 2:** Restart the application and verify that the saved name is restored.
- **Test 3:** Add a student name and course and verify that the record appears in the list.
- **Test 4:** Restart the application and verify that the SQLite record remains available.

## 11. Result
The application demonstrates successful local data persistence using SharedPreferences for simple key-value data and SQLite for structured student records.

## 12. Conclusion
SharedPreferences is suitable for small settings or values, while SQLite is suitable for data organized into tables. Both allow the application to retain data after it is closed and reopened.
