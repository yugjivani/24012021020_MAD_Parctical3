# 📱 MAD Practical-3 — Implicit & Explicit Intent

This repository contains the implementation of **Practical-3** for the **Mobile Application Development (MAD)** subject.

The practical demonstrates the use of **Implicit Intent** and **Explicit Intent** in Android applications. It performs common operations such as opening a website, making a phone call, viewing the call log, opening the gallery, setting an alarm, launching the camera, and navigating between Activities.

---

## 📌 Practical Information

| Information    | Details                              |
| -------------- | ------------------------------------ |
| **Subject**    | Mobile Application Development (MAD) |
| **Practical**  | Practical-3                          |
| **Language**   | Kotlin                               |
| **UI**         | XML                                  |
| **IDE**        | Android Studio                       |
| **Layout**     | ConstraintLayout / CoordinatorLayout |
| **Platform**   | Android                              |
| **Repository** | 24012021020_MAD_Parctical3           |

---

## 🎯 Aim

To create an Android application that demonstrates **Implicit Intent** and **Explicit Intent**.

The application provides different buttons to perform common Android operations such as:

* Making a phone call
* Opening a URL
* Viewing the call log
* Opening the gallery
* Setting an alarm
* Opening the camera
* Navigating to another Activity

---

## 🎯 Objectives

The objectives of this practical are:

* Understand the concept of Intent in Android.
* Demonstrate Implicit Intent.
* Demonstrate Explicit Intent.
* Use different Intent Actions.
* Use `Intent.setData()`.
* Use `Intent.setType()`.
* Open external applications using `startActivity()`.
* Navigate between Activities.
* Understand runtime permissions.
* Use `Uri.parse()` for URI-based operations.
* Understand Activity Result APIs.
* Use Android built-in content types.

---

# 🔗 What is an Intent?

An **Intent** is a messaging object used to request an action from another Android component.

Intents can be used to:

* Start another Activity
* Open another application
* Open a webpage
* Open the phone dialer
* Open the camera
* Open the gallery
* Set an alarm
* Share or access data

---

# 🔀 Types of Intent

## 1️⃣ Implicit Intent

An **Implicit Intent** does not specify a particular Activity or application.

Instead, Android finds an appropriate application that can perform the requested action.

### Example

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```

This opens a suitable browser to display the specified URL.

---

## 2️⃣ Explicit Intent

An **Explicit Intent** specifies the exact Activity or component that should be opened.

### Example

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

This opens `LoginActivity` from the current Activity.

---

# 📱 Features Demonstrated

| No. | Operation                    | Intent Type     |
| --: | ---------------------------- | --------------- |
|   1 | Make Call to Specific Number | Implicit Intent |
|   2 | Open Specific URL            | Implicit Intent |
|   3 | Open Call Log                | Implicit Intent |
|   4 | Open Gallery                 | Implicit Intent |
|   5 | Set Alarm                    | Implicit Intent |
|   6 | Open Camera                  | Implicit Intent |
|   7 | Open Login Activity          | Explicit Intent |

---

# 1️⃣ Make Call to Specific Number

The application uses `ACTION_DIAL` with the `tel:` URI scheme to open the phone dialer with a specific number.

```kotlin
val intent = Intent(Intent.ACTION_DIAL)
intent.data = Uri.parse("tel:9876543210")
startActivity(intent)
```

### Important Concept

```text
tel:
```

The `tel:` URI scheme represents a telephone number.

> `ACTION_DIAL` opens the dialer with the number filled in. It does not directly place the call.

---

# 2️⃣ Open Specific URL

The application opens a website using an Implicit Intent.

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```

### Important Components

* `Intent.ACTION_VIEW`
* `Uri.parse()`
* `setData()`
* `startActivity()`

---

# 3️⃣ Open Call Log

The application opens the device's call log using an Intent.

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.type = CallLog.Calls.CONTENT_TYPE
startActivity(intent)
```

### Important Resource

```kotlin
CallLog.Calls.CONTENT_TYPE
```

This represents the content type associated with the device's call log.

---

# 4️⃣ Open Gallery

The application opens the device gallery and allows the user to select an image.

```kotlin
val intent = Intent(Intent.ACTION_GET_CONTENT)
intent.type = "image/*"
startActivity(intent)
```

### Important Concept

```text
image/*
```

The MIME type `image/*` indicates that the Intent is intended to work with image files.

---

# 5️⃣ Set Alarm

The application uses the Android Clock/Alarm Intent to open the alarm interface.

```kotlin
val intent = Intent(AlarmClock.ACTION_SET_ALARM)
intent.putExtra(AlarmClock.EXTRA_HOUR, 7)
intent.putExtra(AlarmClock.EXTRA_MINUTES, 0)
startActivity(intent)
```

### Important Classes

```kotlin
AlarmClock.ACTION_SET_ALARM
AlarmClock.EXTRA_HOUR
AlarmClock.EXTRA_MINUTES
```

These constants are used to specify the alarm action and its time.

---

# 6️⃣ Open Camera

The application launches the device camera using an Implicit Intent.

```kotlin
val intent = Intent(MediaStore.ACTION_IMAGE_CAPTURE)
startActivity(intent)
```

Depending on the Android version and implementation, camera permissions or the Activity Result API may be required.

---

# 7️⃣ Open Login Activity

The application demonstrates **Explicit Intent** by opening a specific Activity within the same application.

```kotlin
val intent = Intent(this, LoginActivity::class.java)
startActivity(intent)
```

Here:

* `this` refers to the current Activity.
* `LoginActivity::class.java` identifies the target Activity.
* `startActivity()` starts the Activity.

---

# 🔐 Permissions

Some Android operations may require permissions.

Permissions can be declared in `AndroidManifest.xml`.

Example:

```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_CALL_LOG" />
```

For permissions that require runtime approval, the application can check permissions using:

```kotlin
ContextCompat.checkSelfPermission()
```

and request them using:

```kotlin
ActivityCompat.requestPermissions()
```

> The permissions required depend on the Android version and the specific operation being performed.

---

# 📦 Activity Result API

Modern Android applications can use the **Activity Result API** instead of the older `startActivityForResult()` approach.

Example:

```kotlin
val launcher = registerForActivityResult(
    ActivityResultContracts.StartActivityForResult()
) {
    // Handle result
}
```

The launcher can be used to start an Activity and receive its result.

---

# 🔧 Important Intent Methods

## `setData()`

Used to set the data URI associated with an Intent.

```kotlin
intent.setData(
    Uri.parse("https://www.google.com")
)
```

---

## `setType()`

Used to specify the MIME type of the data.

```kotlin
intent.setType("image/*")
```

---

## `startActivity()`

Used to launch an Activity.

```kotlin
startActivity(intent)
```

---

## `Uri.parse()`

Converts a string into a `Uri`.

```kotlin
Uri.parse("tel:9876543210")
```

---

# 🧩 UI Components Used

## Button

Buttons are provided for each Intent operation.

Example:

```xml
<Button
    android:id="@+id/btnGallery"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:text="Open Gallery" />
```

---

## ConstraintLayout

`ConstraintLayout` is used to position UI elements using constraints.

It provides flexible positioning without requiring deeply nested layouts.

---

## CoordinatorLayout

`CoordinatorLayout` can be used as the root layout when coordinating interactions between UI components such as:

* Snackbar
* AppBar
* Buttons
* Other interactive views

---

# 📚 Important Study Topics

This practical covers:

* Intent
* Implicit Intent
* Explicit Intent
* Intent Actions
* `Intent.ACTION_VIEW`
* `Intent.ACTION_DIAL`
* `Intent.ACTION_GET_CONTENT`
* `Intent.setData()`
* `Intent.setType()`
* `Uri.parse()`
* `startActivity()`
* Activity Result API
* `ActivityResultContracts`
* Runtime Permissions
* `ContextCompat.checkSelfPermission()`
* `ActivityCompat.requestPermissions()`
* `CallLog.Calls.CONTENT_TYPE`
* `ContactsContract.Contacts.CONTENT_TYPE`
* `"image/*"`
* `"tel:"`
* Buttons
* ConstraintLayout
* CoordinatorLayout
* Drawable Resources
* Adding Activities

---

# 📂 Project Structure

```text
24012021020_MAD_Parctical3/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── ...
│           │
│           ├── res/
│           │   ├── drawable/
│           │   ├── layout/
│           │   │   ├── activity_main.xml
│           │   │   └── activity_login.xml
│           │   │
│           │   └── values/
│           │
│           └── AndroidManifest.xml
│
├── gradle/
│
├── build.gradle.kts
├── settings.gradle.kts
└── README.md
```

---

# ▶️ How to Run

### Step 1 — Clone the Repository

```bash
git clone https://github.com/Sakariya-Krish/24012021020_MAD_Parctical3.git
```

### Step 2 — Open the Project

Open the cloned project in **Android Studio**.

### Step 3 — Gradle Synchronization

Allow Android Studio to complete the Gradle synchronization.

### Step 4 — Connect a Device

Connect an Android device with USB Debugging enabled or start an Android Emulator.

### Step 5 — Run the Application

Click:

```text
Run ▶
```

### Step 6 — Test the Features

The application displays buttons for different Intent operations.

Click each button to test the corresponding functionality.

### Step 7 — Grant Permissions

Grant any permissions requested by Android when required.

---

# 🧪 Expected Output

The application provides buttons similar to:

```text
┌─────────────────────────┐
│     Make Phone Call     │
├─────────────────────────┤
│        Open URL         │
├─────────────────────────┤
│      Open Call Log      │
├─────────────────────────┤
│      Open Gallery       │
├─────────────────────────┤
│        Set Alarm        │
├─────────────────────────┤
│       Open Camera       │
├─────────────────────────┤
│    Open Login Activity  │
└─────────────────────────┘
```

Each button performs the corresponding operation using either an **Implicit Intent** or **Explicit Intent**.

---

# 🎓 Learning Outcomes

After completing this practical, the following concepts are understood:

* Intent and its purpose
* Implicit Intent
* Explicit Intent
* Intent Actions
* URI-based Intent operations
* MIME types
* `startActivity()`
* Activity Result API
* Runtime Permissions
* Opening external applications
* Navigating between Activities
* ConstraintLayout
* CoordinatorLayout
* Android UI components
* Kotlin Intent programming

---

# 📌 Conclusion

MAD Practical-3 provides practical knowledge of **Implicit and Explicit Intents** in Android.

The application demonstrates how Android applications can communicate with other applications and components to perform operations such as opening websites, accessing the phone dialer, viewing call logs, selecting images, setting alarms, opening the camera, and navigating between Activities.

---

## 👨‍💻 Author

**Yug Jivani**

**Course:** B.Tech Information Technology
**Subject:** Mobile Application Development (MAD)
