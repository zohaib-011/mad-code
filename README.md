# Course Management System - Complete Android Project

## Syllabus Concepts Coverage Map

| Concept | Implementation | File(s) |
|---------|----------------|---------|
| **Activity Lifecycle** | All lifecycle methods with Toast/TextView | `LifecycleActivity.java` |
| **ListView with ArrayAdapter** | Menu list with item click | `MainActivity2.java` |
| **Switch Statement** | Navigation item handling | `MainActivity2.java`, `MainActivity.java` |
| **Explicit Intent** | Activity navigation with data | All Activities |
| **Notifications** | NotificationCompat + Channel | `NotificationHelper.java` |
| **Fragments** | Home, Setting, Maps, Courses, Stats, Profile | `fragments/` package |
| **DrawerLayout** | Navigation drawer with menu | `MainActivity4.java` |
| **NavigationView** | Menu-based fragment switching | `MainActivity4.java` |
| **Threads & Handler** | Background countdown + sync | `MainActivity5.java`, `DataSyncService.java` |
| **Unbound Service** | Background music service | `MusicService.java` |
| **Bound Service** | Service with LocalBinder | `MybindService.java` |
| **ServiceConnection** | Bind/unbind service | `MainActivity6.java` |
| **MediaPlayer** | Audio playback | `MusicService.java`, `MybindService.java` |
| **Firebase Database** | Full CRUD operations | `FirebaseHelper.java`, Activities |
| **ValueEventListener** | Real-time data sync | `CoursesFragment.java` |
| **Custom Adapter (BaseAdapter)** | List data display | `StudentAdapter.java` |
| **RecyclerView Adapter** | Course cards display | `CourseAdapter.java` |
| **CardView** | Material card UI | `item_course_card.xml` |
| **BottomNavigationView** | Tab navigation | `MainActivity.java` |
| **Google Maps** | SupportMapFragment + Marker | `MapsFragment.java`, `ProfileFragment.java` |
| **SharedPreferences** | Theme persistence | `SettingsActivity.java` |
| **ConstraintLayout** | Complex layouts | Multiple XML files |
| **LinearLayout** | Form layouts | Multiple XML files |
| **FrameLayout** | Fragment container | `activity_main.xml` |
| **FloatingActionButton** | Add course action | `fragment_courses.xml` |
| **TextInputLayout** | Material input fields | Form activities |
| **ProgressBar** | Loading indicators | Add/Update activities |

---

## Project Structure

```
com.example.coursemanager/
│
├── models/
│   └── Course.java                    // Data model class
│
├── adapters/
│   ├── CourseAdapter.java             // RecyclerView adapter (ViewHolder pattern)
│   └── StudentAdapter.java            // BaseAdapter example
│
├── activities/
│   ├── MainActivity.java              // Entry - BottomNavigation + Fragments
│   ├── MainActivity2.java             // ListView with switch navigation
│   ├── MainActivity4.java             // DrawerLayout + NavigationView
│   ├── MainActivity5.java             // Thread + Handler countdown
│   ├── MainActivity6.java             // Services demo (Bound + Unbound)
│   ├── AddCourseActivity.java         // Firebase CREATE
│   ├── UpdateCourseActivity.java      // Firebase UPDATE
│   ├── LifecycleActivity.java         // Activity Lifecycle demo
│   ├── SettingsActivity.java          // SharedPreferences
│   └── DatabaseActivity.java          // Firebase operations
│
├── fragments/
│   ├── HomeFragment.java              // Basic fragment
│   ├── SettingFragment.java           // Settings fragment
│   ├── MapsFragment.java              // Google Maps integration
│   ├── CoursesFragment.java           // RecyclerView + Firebase READ
│   ├── StatsFragment.java             // Statistics calculation
│   └── ProfileFragment.java           // Map + navigation buttons
│
├── services/
│   ├── MusicService.java              // Unbound Service + MediaPlayer
│   ├── MybindService.java             // Bound Service + LocalBinder
│   └── DataSyncService.java           // Background sync service
│
├── utils/
│   ├── FirebaseHelper.java            // Firebase CRUD wrapper
│   └── NotificationHelper.java        // Notification builder
│
└── res/
    ├── layout/
    │   ├── activity_main.xml          // BottomNav + FrameLayout
    │   ├── activity_main2.xml         // ListView
    │   ├── activity_main4.xml         // DrawerLayout
    │   ├── activity_main5.xml         // Thread demo
    │   ├── activity_main6.xml         // Services buttons
    │   ├── activity_add_course.xml    // Add form
    │   ├── activity_update_course.xml // Update form
    │   ├── activity_lifecycle.xml     // Lifecycle display
    │   ├── activity_settings.xml      // Settings UI
    │   ├── activity_database.xml      // Database form
    │   ├── fragment_home.xml          // Home fragment
    │   ├── fragment_setting.xml       // Setting fragment
    │   ├── fragment_maps.xml          // Map fragment
    │   ├── fragment_courses.xml       // Courses list
    │   ├── fragment_stats.xml         // Statistics
    │   ├── fragment_profile.xml       // Profile + map
    │   ├── item_course_card.xml       // RecyclerView item
    │   └── recyclerviewlayout.xml     // ListView item
    │
    ├── menu/
    │   ├── bottom_nav_menu.xml        // Bottom navigation
    │   └── drawer_menu.xml            // Drawer menu
    │
    └── values/
        ├── strings.xml
        ├── colors.xml
        └── themes.xml
```

---

## Layout Diagrams

### 1. MainActivity (Bottom Navigation)
```
┌─────────────────────────────────────┐
│                                     │
│     ┌───────────────────────┐       │
│     │                       │       │
│     │   Fragment Container  │       │
│     │   (FrameLayout)       │       │
│     │                       │       │
│     │   Shows:              │       │
│     │   - CoursesFragment   │       │
│     │   - StatsFragment     │       │
│     │   - ProfileFragment   │       │
│     │                       │       │
│     └───────────────────────┘       │
│                                     │
├─────────────────────────────────────┤
│  [📚 Courses] [📊 Stats] [👤 Profile] │  ← BottomNavigationView
└─────────────────────────────────────┘
```

### 2. MainActivity2 (ListView Navigation)
```
┌─────────────────────────────────────┐
│         ListView Menu               │
├─────────────────────────────────────┤
│  ┌─────────────────────────────┐    │
│  │ 0. Activity LifeCycle       │ → switch(0)
│  ├─────────────────────────────┤    │
│  │ 1. Change Color             │ → switch(1)
│  ├─────────────────────────────┤    │
│  │ 2. Intent                   │ → switch(2)
│  ├─────────────────────────────┤    │
│  │ 3. Send Notification        │ → switch(3)
│  ├─────────────────────────────┤    │
│  │ 4. Fragments                │ → switch(4)
│  ├─────────────────────────────┤    │
│  │ 5. Thread                   │ → switch(5)
│  ├─────────────────────────────┤    │
│  │ 6. Services                 │ → switch(6)
│  └─────────────────────────────┘    │
└─────────────────────────────────────┘
    ArrayAdapter<String> binds ArrayList to ListView
    OnItemClickListener → switch(position) → startActivity(Intent)
```

### 3. MainActivity4 (DrawerLayout)
```
┌─────────────────────────────────────┐
│ ☰ │        Fragment Content         │
├───┼─────────────────────────────────┤
│   │                                 │
│ N │   ┌─────────────────────┐       │
│ A │   │                     │       │
│ V │   │  HomeFragment       │       │
│   │   │  OR                 │       │
│ D │   │  SettingFragment    │       │
│ R │   │  OR                 │       │
│ A │   │  MapsFragment       │       │
│ W │   │                     │       │
│ E │   └─────────────────────┘       │
│ R │                                 │
└───┴─────────────────────────────────┘

DrawerLayout
├── FrameLayout (fragment_container)
└── NavigationView
    └── menu: drawer_menu.xml
        ├── HOME → HomeFragment
        ├── SETTING → SettingFragment
        └── MAP → MapsFragment
```

### 4. MainActivity5 (Thread + Handler)
```
┌─────────────────────────────────────┐
│                                     │
│     ┌───────────────────────┐       │
│     │                       │       │
│     │   TextView            │       │
│     │   "CountDown: 10"     │       │
│     │                       │       │
│     └───────────────────────┘       │
│                                     │
└─────────────────────────────────────┘

Thread Flow:
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│ new Thread() │ →  │ Handler.post │ →  │ Update UI    │
│ run() loop   │    │ (Runnable)   │    │ setText()    │
│ i = 10 to 0  │    │              │    │              │
└──────────────┘    └──────────────┘    └──────────────┘
       ↓
  Thread.sleep(1000) - 1 second delay each iteration
```

### 5. MainActivity6 (Services)
```
┌─────────────────────────────────────┐
│                                     │
│  ┌─────────────────────────────┐    │
│  │ [Unbound Service Play]      │ → startService(MusicService)
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ [Unbound Service Stop]      │ → stopService(MusicService)
│  └─────────────────────────────┘    │
│                                     │
│  ─────────────────────────────────  │
│  BOUND SERVICES BUTTONS             │
│  ─────────────────────────────────  │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ [Bound Service Play]        │ → MBS.startMusic()
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ [Bound Service Stop]        │ → MBS.stopMusic()
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘

Service Architecture:
┌─────────────────────────────────────────────────────────┐
│                    UNBOUND SERVICE                       │
│  ┌───────────────┐                  ┌──────────────┐    │
│  │ Activity      │  startService()  │ MusicService │    │
│  │               │ ───────────────→ │              │    │
│  │               │  stopService()   │ MediaPlayer  │    │
│  │               │ ───────────────→ │ .start()     │    │
│  └───────────────┘                  └──────────────┘    │
└─────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────┐
│                     BOUND SERVICE                        │
│  ┌───────────────┐  bindService()   ┌──────────────┐    │
│  │ Activity      │ ───────────────→ │ MybindService│    │
│  │               │                  │              │    │
│  │ ServiceConn   │ ←─────────────── │ LocalBinder  │    │
│  │ .onConnected  │    IBinder       │ .getservices │    │
│  │               │                  │              │    │
│  │ MBS.start()   │ ───────────────→ │ startMusic() │    │
│  │ MBS.stop()    │ ───────────────→ │ stopMusic()  │    │
│  └───────────────┘                  └──────────────┘    │
└─────────────────────────────────────────────────────────┘
```

### 6. Add Course Form
```
┌─────────────────────────────────────┐
│        Add New Course               │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────────────────────────┐    │
│  │ Course Name                 │    │  ← TextInputLayout
│  │ ┌─────────────────────────┐ │    │     + TextInputEditText
│  │ │ Mobile Development      │ │    │
│  │ └─────────────────────────┘ │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ Course Code                 │    │
│  │ ┌─────────────────────────┐ │    │
│  │ │ CS401                   │ │    │
│  │ └─────────────────────────┘ │    │
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ Credit Hours                │    │
│  │ ┌─────────────────────────┐ │    │
│  │ │ 3                       │ │    │  ← inputType="number"
│  │ └─────────────────────────┘ │    │
│  └─────────────────────────────┘    │
│                                     │
│  ════════════════════════════════   │  ← ProgressBar (when saving)
│                                     │
│  ┌─────────────────────────────┐    │
│  │       ADD COURSE            │    │  ← Button
│  └─────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

### 7. Course Card (RecyclerView Item)
```
┌─────────────────────────────────────┐
│  ╔═══════════════════════════════╗  │
│  ║ Mobile App Development        ║  │  ← txtCourseName (bold, 20sp)
│  ║                               ║  │
│  ║ Code: CS401                   ║  │  ← txtCourseCode (gray, 16sp)
│  ║ Credits: 3                    ║  │  ← txtCreditHours (gray, 16sp)
│  ║                               ║  │
│  ║ ┌──────────┐  ┌──────────┐   ║  │
│  ║ │  UPDATE  │  │  DELETE  │   ║  │  ← Buttons
│  ║ └──────────┘  └──────────┘   ║  │
│  ╚═══════════════════════════════╝  │  ← CardView with elevation
└─────────────────────────────────────┘
```

### 8. Database Activity
```
┌─────────────────────────────────────┐
│  ┌─────────────────────────────┐    │
│  │ Student ID                  │    │  ← EditText (StdID)
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ Enter your Name             │    │  ← EditText (stdname)
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ Enter your Age              │    │  ← EditText (stdage)
│  └─────────────────────────────┘    │
│                                     │
│  ┌─────────────────────────────┐    │
│  │ Save to the Database        │    │  → Firebase push()
│  └─────────────────────────────┘    │
│  ┌─────────────────────────────┐    │
│  │ Read From the Database      │    │  → ValueEventListener
│  └─────────────────────────────┘    │
│                                     │
│  ┌──────────┬──────────┬────────┐   │
│  │ Name     │ Roll No  │ Marks  │   │  ← Header (LinearLayout)
│  ├──────────┴──────────┴────────┤   │
│  │ ┌────────────────────────┐   │   │
│  │ │ Student 1 data         │   │   │  ← ListView with
│  │ ├────────────────────────┤   │   │    StudentAdapter
│  │ │ Student 2 data         │   │   │
│  │ └────────────────────────┘   │   │
│  └──────────────────────────────┘   │
└─────────────────────────────────────┘
```

---

## Process Flow Diagrams

### Firebase CRUD Operations
```
┌─────────────────────────────────────────────────────────────────┐
│                      FIREBASE CRUD FLOW                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  CREATE:                                                         │
│  ┌──────────┐    ┌─────────────┐    ┌──────────────────────┐    │
│  │ Add Form │ →  │ FirebaseHelper│ → │ databaseRef.push()   │    │
│  │ onClick  │    │ .addCourse() │    │ .getKey()            │    │
│  └──────────┘    └─────────────┘    │ .setValue(course)    │    │
│                                      └──────────────────────┘    │
│                                                                  │
│  READ:                                                           │
│  ┌──────────┐    ┌─────────────────────────────────────────┐    │
│  │ Fragment │ →  │ databaseRef.addValueEventListener()      │    │
│  │ onStart  │    │   onDataChange(DataSnapshot) {           │    │
│  └──────────┘    │     for(child : snapshot.getChildren())  │    │
│                  │       course = child.getValue(Course)    │    │
│                  │       courseList.add(course)             │    │
│                  │   }                                       │    │
│                  └─────────────────────────────────────────┘    │
│                                                                  │
│  UPDATE:                                                         │
│  ┌──────────┐    ┌─────────────┐    ┌──────────────────────┐    │
│  │ Update   │ →  │ FirebaseHelper│ → │ databaseRef          │    │
│  │ Form     │    │ .updateCourse│    │ .child(id)           │    │
│  └──────────┘    └─────────────┘    │ .setValue(course)    │    │
│                                      └──────────────────────┘    │
│                                                                  │
│  DELETE:                                                         │
│  ┌──────────┐    ┌─────────────┐    ┌──────────────────────┐    │
│  │ Delete   │ →  │ FirebaseHelper│ → │ databaseRef          │    │
│  │ Button   │    │ .deleteCourse│    │ .child(id)           │    │
│  └──────────┘    └─────────────┘    │ .removeValue()       │    │
│                                      └──────────────────────┘    │
└─────────────────────────────────────────────────────────────────┘
```

### Activity Lifecycle Flow
```
┌─────────────────────────────────────────────────────────────────┐
│                    ACTIVITY LIFECYCLE                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│        ┌────────────┐                                           │
│        │ onCreate() │ ← Activity created, setContentView        │
│        └─────┬──────┘                                           │
│              ↓                                                   │
│        ┌────────────┐                                           │
│        │ onStart()  │ ← Activity becoming visible               │
│        └─────┬──────┘                                           │
│              ↓                                                   │
│        ┌────────────┐                                           │
│        │ onResume() │ ← Activity is interactive                 │
│        └─────┬──────┘                                           │
│              ↓                                                   │
│     ┌────────────────────┐                                      │
│     │   RUNNING STATE    │ ← User interacting                   │
│     └────────┬───────────┘                                      │
│              ↓                                                   │
│        ┌────────────┐                                           │
│        │ onPause()  │ ← Another activity in foreground          │
│        └─────┬──────┘                                           │
│              ↓                                                   │
│        ┌────────────┐                                           │
│        │ onStop()   │ ← Activity no longer visible              │
│        └─────┬──────┘                                           │
│              ↓                                                   │
│        ┌─────────────┐                                          │
│        │ onDestroy() │ ← Activity being destroyed               │
│        └─────────────┘                                          │
│                                                                  │
│   Special: onRestart() called when returning from stopped state │
└─────────────────────────────────────────────────────────────────┘
```

### Notification Flow
```
┌─────────────────────────────────────────────────────────────────┐
│                    NOTIFICATION FLOW                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  1. Create NotificationChannel (API 26+)                        │
│     ┌────────────────────────────────────────┐                  │
│     │ NotificationChannel("id", "name",      │                  │
│     │                     IMPORTANCE_DEFAULT)│                  │
│     └────────────────────────────────────────┘                  │
│                      ↓                                           │
│  2. Register channel with NotificationManager                   │
│     ┌────────────────────────────────────────┐                  │
│     │ manager.createNotificationChannel(ch)  │                  │
│     └────────────────────────────────────────┘                  │
│                      ↓                                           │
│  3. Create PendingIntent for click action                       │
│     ┌────────────────────────────────────────┐                  │
│     │ Intent intent = new Intent(ctx, Main)  │                  │
│     │ PendingIntent.getActivity(ctx, 0,      │                  │
│     │              intent, FLAG_IMMUTABLE)   │                  │
│     └────────────────────────────────────────┘                  │
│                      ↓                                           │
│  4. Build notification with NotificationCompat.Builder          │
│     ┌────────────────────────────────────────┐                  │
│     │ .setSmallIcon(icon)                    │                  │
│     │ .setContentTitle("Title")              │                  │
│     │ .setContentText("Message")             │                  │
│     │ .setContentIntent(pendingIntent)       │                  │
│     │ .setPriority(PRIORITY_DEFAULT)         │                  │
│     └────────────────────────────────────────┘                  │
│                      ↓                                           │
│  5. Show notification                                           │
│     ┌────────────────────────────────────────┐                  │
│     │ manager.notify(notificationId,         │                  │
│     │                builder.build())        │                  │
│     └────────────────────────────────────────┘                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## Step-by-Step Code Implementation

### Step 1: Create Project in Android Studio
1. File → New → New Project
2. Select "Empty Activity"
3. Name: `CourseManager`
4. Package: `com.example.coursemanager`
5. Language: Java
6. Minimum SDK: API 21

---

### Step 2: Add Dependencies

**Path:** `app/build.gradle`

```gradle
plugins {
    id 'com.android.application'
    id 'com.google.gms.google-services'
}

android {
    compileSdk 33

    defaultConfig {
        applicationId "com.example.coursemanager"
        minSdk 21
        targetSdk 33
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    // AndroidX Libraries
    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.9.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    implementation 'androidx.recyclerview:recyclerview:1.3.0'
    implementation 'androidx.cardview:cardview:1.0.0'

    // Firebase
    implementation platform('com.google.firebase:firebase-bom:32.2.0')
    implementation 'com.google.firebase:firebase-database'
    implementation 'com.google.firebase:firebase-analytics'

    // Google Maps
    implementation 'com.google.android.gms:play-services-maps:18.1.0'

    // Testing
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
}
```

**Path:** `build.gradle` (Project level)

```gradle
buildscript {
    dependencies {
        classpath 'com.google.gms:google-services:4.3.15'
    }
}

plugins {
    id 'com.android.application' version '8.0.0' apply false
}
```

---

### Step 3: AndroidManifest.xml

**Path:** `app/src/main/AndroidManifest.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.coursemanager">

    <!-- Permissions -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS" />

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.AppCompat.Light.DarkActionBar">

        <!-- Main Activity with Bottom Navigation -->
        <activity
            android:name=".activities.MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>

        <!-- ListView Navigation Activity -->
        <activity android:name=".activities.MainActivity2" />

        <!-- DrawerLayout Activity -->
        <activity android:name=".activities.MainActivity4" />

        <!-- Thread Demo Activity -->
        <activity android:name=".activities.MainActivity5" />

        <!-- Services Demo Activity -->
        <activity android:name=".activities.MainActivity6" />

        <!-- Add Course Activity -->
        <activity
            android:name=".activities.AddCourseActivity"
            android:parentActivityName=".activities.MainActivity" />

        <!-- Update Course Activity -->
        <activity
            android:name=".activities.UpdateCourseActivity"
            android:parentActivityName=".activities.MainActivity" />

        <!-- Lifecycle Demo Activity -->
        <activity
            android:name=".activities.LifecycleActivity"
            android:parentActivityName=".activities.MainActivity" />

        <!-- Settings Activity -->
        <activity
            android:name=".activities.SettingsActivity"
            android:parentActivityName=".activities.MainActivity" />

        <!-- Database Activity -->
        <activity android:name=".activities.DatabaseActivity" />

        <!-- Unbound Music Service -->
        <service
            android:name=".services.MusicService"
            android:enabled="true"
            android:exported="false" />

        <!-- Bound Service -->
        <service
            android:name=".services.MybindService"
            android:enabled="true"
            android:exported="false" />

        <!-- Data Sync Service -->
        <service
            android:name=".services.DataSyncService"
            android:enabled="true"
            android:exported="false" />

        <!-- Google Maps API Key -->
        <meta-data
            android:name="com.google.android.geo.API_KEY"
            android:value="YOUR_GOOGLE_MAPS_API_KEY" />

    </application>
</manifest>
```

---

### Step 4: Model Classes

**Path:** `app/src/main/java/com/example/coursemanager/models/Course.java`

```java
package com.example.coursemanager.models;

/**
 * COURSE MODEL CLASS
 * ==================
 * Data model representing a course entity
 * 
 * Concepts Covered:
 * - Java POJO (Plain Old Java Object)
 * - Getters and Setters
 * - Default constructor (required for Firebase)
 * - Parameterized constructor
 */
public class Course {
    private String id;           // Unique identifier from Firebase
    private String courseName;   // Name of the course
    private String courseCode;   // Course code (e.g., CS401)
    private int creditHours;     // Credit hours as integer

    // Default constructor - REQUIRED for Firebase deserialization
    public Course() {
    }

    // Parameterized constructor
    public Course(String id, String courseName, String courseCode, int creditHours) {
        this.id = id;
        this.courseName = courseName;
        this.courseCode = courseCode;
        this.creditHours = creditHours;
    }

    // Getters and Setters
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getCourseName() {
        return courseName;
    }

    public void setCourseName(String courseName) {
        this.courseName = courseName;
    }

    public String getCourseCode() {
        return courseCode;
    }

    public void setCourseCode(String courseCode) {
        this.courseCode = courseCode;
    }

    public int getCreditHours() {
        return creditHours;
    }

    public void setCreditHours(int creditHours) {
        this.creditHours = creditHours;
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/models/Student.java`

```java
package com.example.coursemanager.models;

/**
 * STUDENT MODEL CLASS
 * ===================
 * Data model for student entity (from syllabus)
 * 
 * Concepts Covered:
 * - Data model class
 * - Constructor with parameters
 * - Getter methods
 */
public class Student {
    String ID;
    String Name;
    int Age;

    // Default constructor for Firebase
    public Student() {
    }

    // Parameterized constructor
    public Student(String Sid, String name, int Sage) {
        this.ID = Sid;
        this.Age = Sage;
        this.Name = name;
    }

    // Getter methods
    public String getS_name() {
        return Name;
    }

    public String getS_ID() {
        return ID;
    }

    public int getS_age() {
        return Age;
    }
}
```

---

### Step 5: Utility Classes

**Path:** `app/src/main/java/com/example/coursemanager/utils/FirebaseHelper.java`

```java
package com.example.coursemanager.utils;

import androidx.annotation.NonNull;
import com.example.coursemanager.models.Course;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

/**
 * FIREBASE HELPER CLASS
 * =====================
 * Centralizes all Firebase CRUD operations
 * 
 * Concepts Covered:
 * - Firebase Realtime Database
 * - DatabaseReference
 * - push() for generating unique keys
 * - setValue() for CREATE/UPDATE
 * - removeValue() for DELETE
 * - OnSuccessListener / OnFailureListener callbacks
 * 
 * Firebase Structure:
 * root/
 * └── Courses/
 *     ├── -NxYz123abc/
 *     │   ├── id: "-NxYz123abc"
 *     │   ├── courseName: "Mobile Dev"
 *     │   ├── courseCode: "CS401"
 *     │   └── creditHours: 3
 *     └── -NxYz456def/
 *         └── ...
 */
public class FirebaseHelper {
    private DatabaseReference databaseReference;

    public FirebaseHelper() {
        // Get reference to "Courses" node in Firebase
        databaseReference = FirebaseDatabase.getInstance().getReference("Courses");
    }

    /**
     * CREATE Operation
     * Adds a new course to Firebase database
     * Uses push() to generate unique key
     */
    public void addCourse(Course course, OnSuccessListener<Void> successListener,
                          OnFailureListener failureListener) {
        // Generate unique key
        String key = databaseReference.push().getKey();
        if (key != null) {
            course.setId(key);
            // Save course with generated key
            databaseReference.child(key).setValue(course)
                    .addOnSuccessListener(successListener)
                    .addOnFailureListener(failureListener);
        }
    }

    /**
     * UPDATE Operation
     * Updates existing course in Firebase
     * Uses course's existing ID
     */
    public void updateCourse(Course course, OnSuccessListener<Void> successListener,
                             OnFailureListener failureListener) {
        databaseReference.child(course.getId()).setValue(course)
                .addOnSuccessListener(successListener)
                .addOnFailureListener(failureListener);
    }

    /**
     * DELETE Operation
     * Removes course from Firebase by ID
     */
    public void deleteCourse(String courseId, OnSuccessListener<Void> successListener,
                             OnFailureListener failureListener) {
        databaseReference.child(courseId).removeValue()
                .addOnSuccessListener(successListener)
                .addOnFailureListener(failureListener);
    }

    /**
     * Returns DatabaseReference for direct queries
     * Used with ValueEventListener for READ operations
     */
    public DatabaseReference getDatabaseReference() {
        return databaseReference;
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/utils/NotificationHelper.java`

```java
package com.example.coursemanager.utils;

import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Context;
import android.content.Intent;
import android.os.Build;
import androidx.core.app.NotificationCompat;
import com.example.coursemanager.R;
import com.example.coursemanager.activities.MainActivity;

/**
 * NOTIFICATION HELPER CLASS
 * =========================
 * Creates and displays system notifications
 * 
 * Concepts Covered:
 * - NotificationChannel (API 26+)
 * - NotificationManager
 * - NotificationCompat.Builder
 * - PendingIntent for click action
 * - Build version check for compatibility
 * 
 * Notification Flow:
 * 1. Create channel (once)
 * 2. Build notification with Builder
 * 3. Set icon, title, text, intent
 * 4. Show via NotificationManager.notify()
 */
public class NotificationHelper {
    private static final String CHANNEL_ID = "course_channel";
    private static final String CHANNEL_NAME = "Course Notifications";
    private Context context;
    private NotificationManager notificationManager;

    public NotificationHelper(Context context) {
        this.context = context;
        notificationManager = (NotificationManager)
                context.getSystemService(Context.NOTIFICATION_SERVICE);
        createNotificationChannel();
    }

    /**
     * Creates NotificationChannel for Android O (API 26) and above
     * Required before showing any notification on newer devices
     */
    private void createNotificationChannel() {
        // Check if running on Android O or higher
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(
                    CHANNEL_ID,
                    CHANNEL_NAME,
                    NotificationManager.IMPORTANCE_DEFAULT
            );
            channel.setDescription("Notifications for course operations");
            notificationManager.createNotificationChannel(channel);
        }
    }

    /**
     * Shows notification with title and message
     * Clicking opens MainActivity
     */
    public void showNotification(String title, String message) {
        // Create intent to open when notification clicked
        Intent intent = new Intent(context, MainActivity.class);
        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TASK);

        // Create PendingIntent with FLAG_IMMUTABLE (required for API 31+)
        PendingIntent pendingIntent = PendingIntent.getActivity(
                context,
                0,
                intent,
                PendingIntent.FLAG_IMMUTABLE
        );

        // Build notification using NotificationCompat for backward compatibility
        NotificationCompat.Builder builder = new NotificationCompat.Builder(context, CHANNEL_ID)
                .setSmallIcon(R.drawable.ic_notification)
                .setContentTitle(title)
                .setContentText(message)
                .setContentIntent(pendingIntent)
                .setPriority(NotificationCompat.PRIORITY_DEFAULT)
                .setAutoCancel(true);  // Dismiss when clicked

        // Show notification with unique ID
        notificationManager.notify((int) System.currentTimeMillis(), builder.build());
    }
}
```

---

### Step 6: Adapter Classes

**Path:** `app/src/main/java/com/example/coursemanager/adapters/CourseAdapter.java`

```java
package com.example.coursemanager.adapters;

import android.content.Context;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;
import com.example.coursemanager.R;
import com.example.coursemanager.activities.UpdateCourseActivity;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.example.coursemanager.utils.NotificationHelper;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import java.util.List;

/**
 * COURSE ADAPTER CLASS
 * ====================
 * RecyclerView Adapter with ViewHolder pattern
 * 
 * Concepts Covered:
 * - RecyclerView.Adapter<VH>
 * - ViewHolder pattern for efficient view recycling
 * - onCreateViewHolder - inflate item layout
 * - onBindViewHolder - bind data to views
 * - getItemCount - return list size
 * - Intent with extras for data passing
 * - CardView for Material Design cards
 * 
 * Adapter Flow:
 * 1. RecyclerView calls onCreateViewHolder to create view
 * 2. RecyclerView calls onBindViewHolder to populate data
 * 3. ViewHolder caches view references
 * 4. Views are recycled as user scrolls
 */
public class CourseAdapter extends RecyclerView.Adapter<CourseAdapter.CourseViewHolder> {
    private List<Course> courseList;
    private Context context;
    private FirebaseHelper firebaseHelper;
    private NotificationHelper notificationHelper;

    public CourseAdapter(List<Course> courseList, Context context) {
        this.courseList = courseList;
        this.context = context;
        this.firebaseHelper = new FirebaseHelper();
        this.notificationHelper = new NotificationHelper(context);
    }

    @NonNull
    @Override
    public CourseViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        // Inflate item layout
        View view = LayoutInflater.from(context)
                .inflate(R.layout.item_course_card, parent, false);
        return new CourseViewHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull CourseViewHolder holder, int position) {
        // Get course at position
        Course course = courseList.get(position);

        // Bind data to views
        holder.txtCourseName.setText(course.getCourseName());
        holder.txtCourseCode.setText("Code: " + course.getCourseCode());
        holder.txtCreditHours.setText("Credits: " + course.getCreditHours());

        // Update button - navigate to UpdateCourseActivity with Intent extras
        holder.btnUpdate.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(context, UpdateCourseActivity.class);
                // Pass course data via Intent extras
                intent.putExtra("courseId", course.getId());
                intent.putExtra("courseName", course.getCourseName());
                intent.putExtra("courseCode", course.getCourseCode());
                intent.putExtra("creditHours", course.getCreditHours());
                context.startActivity(intent);
            }
        });

        // Delete button - Firebase DELETE operation
        holder.btnDelete.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                firebaseHelper.deleteCourse(
                        course.getId(),
                        new OnSuccessListener<Void>() {
                            @Override
                            public void onSuccess(Void unused) {
                                // Remove from list and notify adapter
                                courseList.remove(holder.getAdapterPosition());
                                notifyItemRemoved(holder.getAdapterPosition());
                                Toast.makeText(context, "Course deleted",
                                        Toast.LENGTH_SHORT).show();
                                // Show notification
                                notificationHelper.showNotification(
                                        "Course Deleted",
                                        course.getCourseName() + " removed"
                                );
                            }
                        },
                        new OnFailureListener() {
                            @Override
                            public void onFailure(@NonNull Exception e) {
                                Toast.makeText(context, "Delete failed: " + e.getMessage(),
                                        Toast.LENGTH_SHORT).show();
                            }
                        }
                );
            }
        });
    }

    @Override
    public int getItemCount() {
        return courseList.size();
    }

    /**
     * ViewHolder inner class
     * Caches view references for efficient recycling
     */
    public static class CourseViewHolder extends RecyclerView.ViewHolder {
        TextView txtCourseName, txtCourseCode, txtCreditHours;
        Button btnUpdate, btnDelete;
        CardView cardView;

        public CourseViewHolder(@NonNull View itemView) {
            super(itemView);
            cardView = itemView.findViewById(R.id.cardView);
            txtCourseName = itemView.findViewById(R.id.txtCourseName);
            txtCourseCode = itemView.findViewById(R.id.txtCourseCode);
            txtCreditHours = itemView.findViewById(R.id.txtCreditHours);
            btnUpdate = itemView.findViewById(R.id.btnUpdate);
            btnDelete = itemView.findViewById(R.id.btnDelete);
        }
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/adapters/StudentAdapter.java`

```java
package com.example.coursemanager.adapters;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Student;
import java.util.List;

/**
 * STUDENT ADAPTER CLASS
 * =====================
 * BaseAdapter for ListView (from syllabus code)
 * 
 * Concepts Covered:
 * - BaseAdapter (extends for ListView)
 * - getCount() - number of items
 * - getItem(position) - item at position
 * - getItemId(position) - item ID
 * - getView() - create/recycle view for item
 * - LayoutInflater for inflating XML layouts
 * - View recycling pattern (if view == null)
 */
public class StudentAdapter extends BaseAdapter {
    List<Student> stdlist;
    Context context;

    public StudentAdapter(List<Student> stdlist, Context context) {
        this.context = context;
        this.stdlist = stdlist;
    }

    @Override
    public int getCount() {
        return stdlist.size();
    }

    @Override
    public Object getItem(int i) {
        return stdlist.get(i);
    }

    @Override
    public long getItemId(int i) {
        return i;
    }

    @Override
    public View getView(int i, View view, ViewGroup viewGroup) {
        // Recycle view if possible, otherwise inflate new
        if (view == null) {
            view = LayoutInflater.from(context)
                    .inflate(R.layout.recyclerviewlayout, viewGroup, false);
        }

        // Get student at position
        Student std = stdlist.get(i);

        // Find views and set data
        TextView rollno = view.findViewById(R.id.textrollno);
        TextView name = view.findViewById(R.id.textName);
        TextView age = view.findViewById(R.id.textAge);

        rollno.setText("Roll No: " + std.getS_ID());
        name.setText("Name: " + std.getS_name());
        age.setText("Age: " + std.getS_age());

        return view;
    }
}
```

---

### Step 7: Service Classes

**Path:** `app/src/main/java/com/example/coursemanager/services/MusicService.java`

```java
package com.example.coursemanager.services;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.IBinder;
import android.provider.Settings;

/**
 * MUSIC SERVICE CLASS (UNBOUND SERVICE)
 * ======================================
 * Background service that plays audio
 * 
 * Concepts Covered:
 * - Service class (extends Service)
 * - Unbound service lifecycle
 * - onStartCommand() - called when startService() is invoked
 * - onDestroy() - cleanup when service stops
 * - MediaPlayer for audio playback
 * - START_STICKY - service restarts if killed
 * 
 * Unbound Service Lifecycle:
 * startService() → onCreate() → onStartCommand() → Running → stopService() → onDestroy()
 * 
 * Key: onBind() returns null for unbound service
 */
public class MusicService extends Service {
    MediaPlayer mp;

    public MusicService() {
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // Create MediaPlayer with default alarm sound
        mp = MediaPlayer.create(this, Settings.System.DEFAULT_ALARM_ALERT_URI);
        mp.setLooping(true);  // Loop the audio

        if (mp != null) {
            mp.start();  // Start playback
        }

        return START_STICKY;  // Restart if killed by system
    }

    @Override
    public void onDestroy() {
        // Cleanup MediaPlayer
        if (mp != null && mp.isPlaying()) {
            mp.stop();
            mp.release();
        }
        super.onDestroy();
    }

    @Override
    public IBinder onBind(Intent intent) {
        // Return null - this is an unbound service
        return null;
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/services/MybindService.java`

```java
package com.example.coursemanager.services;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.Binder;
import android.os.IBinder;
import android.provider.Settings;

/**
 * MY BIND SERVICE CLASS (BOUND SERVICE)
 * ======================================
 * Service that clients can bind to for direct method calls
 * 
 * Concepts Covered:
 * - Bound Service pattern
 * - LocalBinder inner class
 * - IBinder interface
 * - onBind() returns binder
 * - Service methods callable from Activity
 * - MediaPlayer control
 * 
 * Bound Service Flow:
 * 1. Activity calls bindService(intent, connection, flags)
 * 2. Service's onBind() returns IBinder (LocalBinder)
 * 3. ServiceConnection.onServiceConnected receives IBinder
 * 4. Cast IBinder to LocalBinder
 * 5. Call binder.getservices() to get service instance
 * 6. Call service methods directly (startMusic, stopMusic)
 * 7. unbindService() when done
 */
public class MybindService extends Service {
    MediaPlayer mp;
    private final IBinder binder = new LocalBinder();

    /**
     * LocalBinder class
     * Provides getservices() method to return service instance
     */
    public class LocalBinder extends Binder {
        public MybindService getservices() {
            return MybindService.this;
        }
    }

    @Override
    public void onCreate() {
        super.onCreate();
        // Initialize MediaPlayer with default ringtone
        mp = MediaPlayer.create(this, Settings.System.DEFAULT_RINGTONE_URI);
        mp.setLooping(true);
    }

    /**
     * Public method - callable from bound Activity
     */
    public void startMusic() {
        if (!mp.isPlaying()) {
            mp.start();
        }
    }

    /**
     * Public method - callable from bound Activity
     */
    public void stopMusic() {
        if (mp.isPlaying()) {
            mp.stop();
            mp.prepareAsync();  // Prepare for next play
        }
    }

    @Override
    public void onDestroy() {
        if (mp != null) {
            mp.release();
        }
        super.onDestroy();
    }

    @Override
    public IBinder onBind(Intent intent) {
        // Return binder for bound service
        return binder;
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/services/DataSyncService.java`

```java
package com.example.coursemanager.services;

import android.app.Service;
import android.content.Intent;
import android.os.Handler;
import android.os.IBinder;
import android.os.Looper;
import android.widget.Toast;

/**
 * DATA SYNC SERVICE CLASS
 * =======================
 * Background service for periodic data synchronization
 * 
 * Concepts Covered:
 * - Unbound service
 * - Handler with Looper
 * - Runnable for repeated tasks
 * - postDelayed for scheduling
 * - Service lifecycle management
 * 
 * Handler/Runnable Pattern:
 * Handler runs on main thread (Looper.getMainLooper())
 * Runnable contains task to execute
 * postDelayed schedules execution after delay
 * Runnable can schedule itself for periodic execution
 */
public class DataSyncService extends Service {
    private Handler handler;
    private Runnable syncRunnable;
    private static final int SYNC_INTERVAL = 30000; // 30 seconds

    @Override
    public void onCreate() {
        super.onCreate();
        // Create Handler on main thread
        handler = new Handler(Looper.getMainLooper());
        Toast.makeText(this, "Data Sync Service Started", Toast.LENGTH_SHORT).show();
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // Define sync task
        syncRunnable = new Runnable() {
            @Override
            public void run() {
                // Simulate sync operation
                Toast.makeText(DataSyncService.this,
                        "Syncing data with server...", Toast.LENGTH_SHORT).show();

                // Schedule next sync
                handler.postDelayed(this, SYNC_INTERVAL);
            }
        };

        // Start first sync immediately
        handler.post(syncRunnable);

        return START_STICKY;
    }

    @Override
    public void onDestroy() {
        super.onDestroy();
        // Remove callbacks to prevent memory leaks
        if (handler != null && syncRunnable != null) {
            handler.removeCallbacks(syncRunnable);
        }
        Toast.makeText(this, "Data Sync Service Stopped", Toast.LENGTH_SHORT).show();
    }

    @Override
    public IBinder onBind(Intent intent) {
        return null;  // Unbound service
    }
}
```

---

### Step 8: Activity Classes

**Path:** `app/src/main/java/com/example/coursemanager/activities/MainActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.MenuItem;
import com.example.coursemanager.R;
import com.example.coursemanager.fragments.CoursesFragment;
import com.example.coursemanager.fragments.ProfileFragment;
import com.example.coursemanager.fragments.StatsFragment;
import com.google.android.material.bottomnavigation.BottomNavigationView;

/**
 * MAIN ACTIVITY - Entry Point
 * ===========================
 * Uses BottomNavigationView with Fragments
 * 
 * Concepts Covered:
 * - AppCompatActivity
 * - BottomNavigationView
 * - Fragment transactions
 * - OnNavigationItemSelectedListener
 * - If-else for menu selection (replaces switch on resource IDs)
 * - getSupportFragmentManager().beginTransaction()
 * 
 * Navigation Pattern:
 * User taps bottom nav item → Listener fires → 
 * Fragment created → Transaction replaces container
 */
public class MainActivity extends AppCompatActivity {
    private BottomNavigationView bottomNavigationView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottomNavigationView = findViewById(R.id.bottomNavigation);

        // Load default fragment on first launch
        if (savedInstanceState == null) {
            loadFragment(new CoursesFragment());
        }

        // Bottom navigation listener
        bottomNavigationView.setOnNavigationItemSelectedListener(
                new BottomNavigationView.OnNavigationItemSelectedListener() {
                    @Override
                    public boolean onNavigationItemSelected(@NonNull MenuItem item) {
                        Fragment selectedFragment = null;

                        // Menu item selection (if-else replaces switch for resource IDs)
                        int itemId = item.getItemId();
                        if (itemId == R.id.nav_courses) {
                            selectedFragment = new CoursesFragment();
                        } else if (itemId == R.id.nav_stats) {
                            selectedFragment = new StatsFragment();
                        } else if (itemId == R.id.nav_profile) {
                            selectedFragment = new ProfileFragment();
                        }

                        if (selectedFragment != null) {
                            loadFragment(selectedFragment);
                        }
                        return true;
                    }
                }
        );
    }

    /**
     * Loads fragment into container using FragmentTransaction
     */
    private void loadFragment(Fragment fragment) {
        getSupportFragmentManager()
                .beginTransaction()
                .replace(R.id.fragmentContainer, fragment)
                .commit();
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/MainActivity2.java`

```java
package com.example.coursemanager.activities;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import java.util.ArrayList;

/**
 * MAIN ACTIVITY 2 - ListView with Switch Navigation
 * ==================================================
 * Demonstrates ListView, ArrayAdapter, and switch statement
 * 
 * Concepts Covered:
 * - ListView widget
 * - ArrayAdapter<String> - adapts ArrayList to ListView
 * - OnItemClickListener
 * - switch(position) for navigation
 * - Explicit Intent with startActivity()
 * 
 * ListView Pattern:
 * ArrayList<String> → ArrayAdapter → ListView → OnItemClick → switch → Intent
 */
public class MainActivity2 extends AppCompatActivity {
    ListView lv;
    ArrayList<String> al = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main2);

        lv = findViewById(R.id.listmenu);

        // Populate menu items
        al.add("Activity LifeCycle");
        al.add("Change Color");
        al.add("Intent");
        al.add("Send Notification");
        al.add("Fragments");
        al.add("Thread");
        al.add("Services");
        al.add("Database");

        // Create ArrayAdapter - binds ArrayList to ListView
        ArrayAdapter<String> adapter = new ArrayAdapter<>(
                this,
                android.R.layout.simple_list_item_1,  // Built-in layout
                al
        );

        // Set adapter to ListView
        lv.setAdapter(adapter);

        // Item click listener with switch statement
        lv.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> adapterView, View view, int position, long id) {
                // Switch statement for navigation based on position
                switch (position) {
                    case 0:
                        // Activity Lifecycle
                        Intent i0 = new Intent(MainActivity2.this, LifecycleActivity.class);
                        startActivity(i0);
                        break;

                    case 1:
                        // Change Color - could navigate to color picker
                        break;

                    case 2:
                        // Intent demo
                        Intent i2 = new Intent(MainActivity2.this, AddCourseActivity.class);
                        startActivity(i2);
                        break;

                    case 3:
                        // Send Notification
                        Intent i3 = new Intent(MainActivity2.this, MainActivity.class);
                        startActivity(i3);
                        break;

                    case 4:
                        // Fragments - DrawerLayout activity
                        Intent i4 = new Intent(MainActivity2.this, MainActivity4.class);
                        startActivity(i4);
                        break;

                    case 5:
                        // Thread demo
                        Intent i5 = new Intent(MainActivity2.this, MainActivity5.class);
                        startActivity(i5);
                        break;

                    case 6:
                        // Services demo
                        Intent i6 = new Intent(MainActivity2.this, MainActivity6.class);
                        startActivity(i6);
                        break;

                    case 7:
                        // Database
                        Intent i7 = new Intent(MainActivity2.this, DatabaseActivity.class);
                        startActivity(i7);
                        break;
                }
            }
        });
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/MainActivity4.java`

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.ActionBarDrawerToggle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.core.view.GravityCompat;
import androidx.drawerlayout.widget.DrawerLayout;
import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.MenuItem;
import com.example.coursemanager.R;
import com.example.coursemanager.fragments.HomeFragment;
import com.example.coursemanager.fragments.MapsFragment;
import com.example.coursemanager.fragments.SettingFragment;
import com.google.android.material.navigation.NavigationView;

/**
 * MAIN ACTIVITY 4 - DrawerLayout with NavigationView
 * ===================================================
 * Navigation Drawer pattern with fragments
 * 
 * Concepts Covered:
 * - DrawerLayout as root layout
 * - NavigationView with menu
 * - ActionBarDrawerToggle (hamburger icon)
 * - OnNavigationItemSelectedListener
 * - Fragment transactions
 * - GravityCompat for drawer direction
 * 
 * DrawerLayout Structure:
 * DrawerLayout
 * ├── Main Content (FrameLayout for fragments)
 * └── NavigationView (slides from start/left)
 *     └── Menu items
 */
public class MainActivity4 extends AppCompatActivity
        implements NavigationView.OnNavigationItemSelectedListener {

    DrawerLayout drawer;
    NavigationView navView;
    Toolbar toolbar;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main4);

        // Setup toolbar
        toolbar = findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);

        // Setup drawer
        drawer = findViewById(R.id.drawer_layout);
        navView = findViewById(R.id.nav_view);

        // ActionBarDrawerToggle - creates hamburger icon
        ActionBarDrawerToggle toggle = new ActionBarDrawerToggle(
                this, drawer, toolbar,
                R.string.navigation_drawer_open,
                R.string.navigation_drawer_close
        );
        drawer.addDrawerListener(toggle);
        toggle.syncState();

        // Set navigation listener
        navView.setNavigationItemSelectedListener(this);

        // Load default fragment
        if (savedInstanceState == null) {
            getSupportFragmentManager().beginTransaction()
                    .replace(R.id.fragment_container, new HomeFragment())
                    .commit();
            navView.setCheckedItem(R.id.nav_home);
        }
    }

    @Override
    public boolean onNavigationItemSelected(@NonNull MenuItem item) {
        Fragment selectedFragment = null;

        // Handle navigation item selection
        int itemId = item.getItemId();
        if (itemId == R.id.nav_home) {
            selectedFragment = new HomeFragment();
        } else if (itemId == R.id.nav_setting) {
            selectedFragment = new SettingFragment();
        } else if (itemId == R.id.nav_map) {
            selectedFragment = new MapsFragment();
        }

        if (selectedFragment != null) {
            getSupportFragmentManager().beginTransaction()
                    .replace(R.id.fragment_container, selectedFragment)
                    .commit();
        }

        // Close drawer after selection
        drawer.closeDrawer(GravityCompat.START);
        return true;
    }

    @Override
    public void onBackPressed() {
        // Close drawer on back press if open
        if (drawer.isDrawerOpen(GravityCompat.START)) {
            drawer.closeDrawer(GravityCompat.START);
        } else {
            super.onBackPressed();
        }
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/MainActivity5.java`

```java
package com.example.coursemanager.activities;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.os.Handler;
import android.os.Looper;
import android.widget.TextView;
import com.example.coursemanager.R;

/**
 * MAIN ACTIVITY 5 - Thread with Handler Demo
 * ===========================================
 * Demonstrates background thread with UI updates
 * 
 * Concepts Covered:
 * - new Thread() for background work
 * - Runnable interface
 * - Handler for main thread communication
 * - handler.post() to run on UI thread
 * - Thread.sleep() for delays
 * - UI updates from background thread (via Handler)
 * 
 * Thread Communication Pattern:
 * ┌──────────────────┐         ┌──────────────────┐
 * │ Background Thread│ ──────→ │ Handler          │
 * │ (cannot update   │  post() │ (runs on main    │
 * │  UI directly)    │         │  UI thread)      │
 * └──────────────────┘         └──────────────────┘
 *                                      │
 *                                      ↓
 *                              ┌──────────────────┐
 *                              │ Update TextView  │
 *                              └──────────────────┘
 */
public class MainActivity5 extends AppCompatActivity {
    TextView tv;
    Handler handler;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main5);

        tv = findViewById(R.id.textView);

        // Create Handler on main (UI) thread
        handler = new Handler(Looper.getMainLooper());

        // Start background thread
        new Thread(new Runnable() {
            @Override
            public void run() {
                // Countdown from 10 to 0
                for (int i = 10; i >= 0; i--) {
                    final int count = i;  // Final for inner class access

                    // Post to UI thread via Handler
                    handler.post(new Runnable() {
                        @Override
                        public void run() {
                            // This runs on UI thread - safe to update TextView
                            tv.setText("CountDown: " + count);
                        }
                    });

                    try {
                        Thread.sleep(1000);  // Wait 1 second
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            }
        }).start();  // Don't forget to start the thread!
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/MainActivity6.java`

```java
package com.example.coursemanager.activities;

import androidx.appcompat.app.AppCompatActivity;
import android.content.ComponentName;
import android.content.Context;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.view.View;
import android.widget.Button;
import com.example.coursemanager.R;
import com.example.coursemanager.services.MusicService;
import com.example.coursemanager.services.MybindService;

/**
 * MAIN ACTIVITY 6 - Services Demo
 * ================================
 * Demonstrates both Unbound and Bound services
 * 
 * Concepts Covered:
 * - startService() / stopService() for unbound services
 * - bindService() / unbindService() for bound services
 * - ServiceConnection interface
 * - onServiceConnected callback
 * - Accessing service methods via binder
 * - BIND_AUTO_CREATE flag
 * 
 * Service Types Comparison:
 * ┌────────────────────────────────────────────────────────────┐
 * │ UNBOUND SERVICE                                            │
 * │ - Started with startService()                              │
 * │ - Runs independently of activity                           │
 * │ - Must explicitly stop with stopService()                  │
 * │ - No direct method calls                                   │
 * ├────────────────────────────────────────────────────────────┤
 * │ BOUND SERVICE                                              │
 * │ - Started with bindService()                               │
 * │ - Bound to activity lifecycle                              │
 * │ - Can call service methods directly                        │
 * │ - Stops when all clients unbind                            │
 * └────────────────────────────────────────────────────────────┘
 */
public class MainActivity6 extends AppCompatActivity {
    Button unboundPlay, unboundStop, boundPlay, boundStop;

    // Bound service reference
    MybindService MBS;
    boolean isBound = false;

    // ServiceConnection - receives binder when connected
    ServiceConnection myconn = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            // Cast IBinder to LocalBinder
            MybindService.LocalBinder binder = (MybindService.LocalBinder) iBinder;
            // Get service instance
            MBS = binder.getservices();
            isBound = true;
        }

        @Override
        public void onServiceDisconnected(ComponentName componentName) {
            isBound = false;
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main6);

        unboundPlay = findViewById(R.id.unboundPlay);
        unboundStop = findViewById(R.id.unboundStop);
        boundPlay = findViewById(R.id.boundPlay);
        boundStop = findViewById(R.id.boundStop);

        // ========== UNBOUND SERVICE ==========

        // Start unbound service
        unboundPlay.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent i = new Intent(MainActivity6.this, MusicService.class);
                startService(i);  // Starts MusicService
            }
        });

        // Stop unbound service
        unboundStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent i = new Intent(MainActivity6.this, MusicService.class);
                stopService(i);  // Stops MusicService
            }
        });

        // ========== BOUND SERVICE ==========

        // Bind service on activity start
        Intent bindIntent = new Intent(this, MybindService.class);
        bindService(bindIntent, myconn, Context.BIND_AUTO_CREATE);

        // Play via bound service
        boundPlay.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (isBound) {
                    MBS.startMusic();  // Direct method call
                }
            }
        });

        // Stop via bound service
        boundStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (isBound) {
                    MBS.stopMusic();  // Direct method call
                }
            }
        });
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        // Unbind when activity destroyed
        if (isBound) {
            unbindService(myconn);
            isBound = false;
        }
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/AddCourseActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;
import android.widget.Toast;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.example.coursemanager.utils.NotificationHelper;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.android.material.textfield.TextInputEditText;

/**
 * ADD COURSE ACTIVITY
 * ===================
 * Firebase CREATE operation
 * 
 * Concepts Covered:
 * - TextInputLayout + TextInputEditText
 * - ProgressBar for loading state
 * - Firebase push() + setValue()
 * - OnSuccessListener / OnFailureListener
 * - Input validation
 * - Toast messages
 * - Notification on success
 * 
 * Firebase CREATE Flow:
 * User Input → Validation → Course Object → 
 * FirebaseHelper.addCourse() → push().setValue() → 
 * Success Callback → Notification + finish()
 */
public class AddCourseActivity extends AppCompatActivity {
    private TextInputEditText edtCourseName, edtCourseCode, edtCreditHours;
    private Button btnAddCourse;
    private ProgressBar progressBar;
    private FirebaseHelper firebaseHelper;
    private NotificationHelper notificationHelper;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_add_course);

        // Initialize views
        edtCourseName = findViewById(R.id.edtCourseName);
        edtCourseCode = findViewById(R.id.edtCourseCode);
        edtCreditHours = findViewById(R.id.edtCreditHours);
        btnAddCourse = findViewById(R.id.btnAddCourse);
        progressBar = findViewById(R.id.progressBar);

        // Initialize helpers
        firebaseHelper = new FirebaseHelper();
        notificationHelper = new NotificationHelper(this);

        // Add course button click
        btnAddCourse.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                addCourse();
            }
        });
    }

    private void addCourse() {
        // Get input values
        String name = edtCourseName.getText().toString().trim();
        String code = edtCourseCode.getText().toString().trim();
        String creditsStr = edtCreditHours.getText().toString().trim();

        // Validate inputs
        if (name.isEmpty()) {
            edtCourseName.setError("Required");
            return;
        }
        if (code.isEmpty()) {
            edtCourseCode.setError("Required");
            return;
        }
        if (creditsStr.isEmpty()) {
            edtCreditHours.setError("Required");
            return;
        }

        int credits = Integer.parseInt(creditsStr);

        // Show progress
        progressBar.setVisibility(View.VISIBLE);
        btnAddCourse.setEnabled(false);

        // Create course object (id will be set by FirebaseHelper)
        Course course = new Course(null, name, code, credits);

        // Add to Firebase
        firebaseHelper.addCourse(course,
                new OnSuccessListener<Void>() {
                    @Override
                    public void onSuccess(Void unused) {
                        progressBar.setVisibility(View.GONE);
                        Toast.makeText(AddCourseActivity.this,
                                "Course added successfully", Toast.LENGTH_SHORT).show();

                        // Show notification
                        notificationHelper.showNotification(
                                "Course Added",
                                name + " has been added successfully"
                        );

                        finish();  // Close activity
                    }
                },
                new OnFailureListener() {
                    @Override
                    public void onFailure(@NonNull Exception e) {
                        progressBar.setVisibility(View.GONE);
                        btnAddCourse.setEnabled(true);
                        Toast.makeText(AddCourseActivity.this,
                                "Error: " + e.getMessage(), Toast.LENGTH_SHORT).show();
                    }
                }
        );
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/UpdateCourseActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;
import android.widget.Toast;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.example.coursemanager.utils.NotificationHelper;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.android.material.textfield.TextInputEditText;

/**
 * UPDATE COURSE ACTIVITY
 * ======================
 * Firebase UPDATE operation
 * 
 * Concepts Covered:
 * - Receiving Intent extras
 * - Pre-populating form with existing data
 * - Firebase setValue() for update
 * - Explicit Intent data passing
 * 
 * Intent Data Flow:
 * CourseAdapter (click) → Intent.putExtra() → 
 * UpdateCourseActivity → getIntent().getStringExtra() → 
 * Pre-fill form → User edits → Firebase UPDATE
 */
public class UpdateCourseActivity extends AppCompatActivity {
    private TextInputEditText edtCourseName, edtCourseCode, edtCreditHours;
    private Button btnUpdateCourse;
    private ProgressBar progressBar;
    private FirebaseHelper firebaseHelper;
    private NotificationHelper notificationHelper;

    private String courseId;  // Received from Intent

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_update_course);

        // Initialize views
        edtCourseName = findViewById(R.id.edtCourseName);
        edtCourseCode = findViewById(R.id.edtCourseCode);
        edtCreditHours = findViewById(R.id.edtCreditHours);
        btnUpdateCourse = findViewById(R.id.btnUpdateCourse);
        progressBar = findViewById(R.id.progressBar);

        // Initialize helpers
        firebaseHelper = new FirebaseHelper();
        notificationHelper = new NotificationHelper(this);

        // Get data from Intent extras
        courseId = getIntent().getStringExtra("courseId");
        String courseName = getIntent().getStringExtra("courseName");
        String courseCode = getIntent().getStringExtra("courseCode");
        int creditHours = getIntent().getIntExtra("creditHours", 0);

        // Pre-populate form with existing data
        edtCourseName.setText(courseName);
        edtCourseCode.setText(courseCode);
        edtCreditHours.setText(String.valueOf(creditHours));

        // Update button click
        btnUpdateCourse.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                updateCourse();
            }
        });
    }

    private void updateCourse() {
        // Get updated values
        String name = edtCourseName.getText().toString().trim();
        String code = edtCourseCode.getText().toString().trim();
        String creditsStr = edtCreditHours.getText().toString().trim();

        // Validate
        if (name.isEmpty() || code.isEmpty() || creditsStr.isEmpty()) {
            Toast.makeText(this, "Please fill all fields", Toast.LENGTH_SHORT).show();
            return;
        }

        int credits = Integer.parseInt(creditsStr);

        // Show progress
        progressBar.setVisibility(View.VISIBLE);
        btnUpdateCourse.setEnabled(false);

        // Create updated course object with existing ID
        Course course = new Course(courseId, name, code, credits);

        // Update in Firebase
        firebaseHelper.updateCourse(course,
                new OnSuccessListener<Void>() {
                    @Override
                    public void onSuccess(Void unused) {
                        progressBar.setVisibility(View.GONE);
                        Toast.makeText(UpdateCourseActivity.this,
                                "Course updated successfully", Toast.LENGTH_SHORT).show();

                        notificationHelper.showNotification(
                                "Course Updated",
                                name + " has been updated"
                        );

                        finish();
                    }
                },
                new OnFailureListener() {
                    @Override
                    public void onFailure(@NonNull Exception e) {
                        progressBar.setVisibility(View.GONE);
                        btnUpdateCourse.setEnabled(true);
                        Toast.makeText(UpdateCourseActivity.this,
                                "Error: " + e.getMessage(), Toast.LENGTH_SHORT).show();
                    }
                }
        );
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/LifecycleActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;
import android.widget.Toast;
import com.example.coursemanager.R;

/**
 * LIFECYCLE ACTIVITY
 * ==================
 * Demonstrates all Activity lifecycle methods
 * 
 * Concepts Covered:
 * - onCreate() - Activity created
 * - onStart() - Activity becoming visible
 * - onResume() - Activity interactive (foreground)
 * - onPause() - Activity losing focus
 * - onStop() - Activity no longer visible
 * - onDestroy() - Activity being destroyed
 * - onRestart() - Activity restarting from stopped state
 * 
 * Lifecycle Flow Visualization:
 * 
 * Launch:    onCreate → onStart → onResume → [RUNNING]
 * 
 * Home btn:  onPause → onStop → [STOPPED]
 * 
 * Return:    onRestart → onStart → onResume → [RUNNING]
 * 
 * Back btn:  onPause → onStop → onDestroy → [DESTROYED]
 */
public class LifecycleActivity extends AppCompatActivity {
    private TextView txtCurrentState;
    private TextView txtLifecycleLog;
    private StringBuilder lifecycleLog = new StringBuilder();
    private int stepCounter = 0;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_lifecycle);

        txtCurrentState = findViewById(R.id.txtCurrentState);
        txtLifecycleLog = findViewById(R.id.txtLifecycleLog);

        logLifecycleEvent("onCreate()");
        Toast.makeText(this, "onCreate() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onStart() {
        super.onStart();
        logLifecycleEvent("onStart()");
        Toast.makeText(this, "onStart() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onResume() {
        super.onResume();
        logLifecycleEvent("onResume()");
        Toast.makeText(this, "onResume() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onPause() {
        super.onPause();
        logLifecycleEvent("onPause()");
        Toast.makeText(this, "onPause() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onStop() {
        super.onStop();
        logLifecycleEvent("onStop()");
        Toast.makeText(this, "onStop() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        logLifecycleEvent("onDestroy()");
        Toast.makeText(this, "onDestroy() called", Toast.LENGTH_SHORT).show();
    }

    @Override
    protected void onRestart() {
        super.onRestart();
        logLifecycleEvent("onRestart()");
        Toast.makeText(this, "onRestart() called", Toast.LENGTH_SHORT).show();
    }

    /**
     * Logs lifecycle event to TextView
     */
    private void logLifecycleEvent(String event) {
        stepCounter++;
        lifecycleLog.append(stepCounter).append(". ").append(event).append("\n");
        txtCurrentState.setText("Current State: " + event);
        txtLifecycleLog.setText(lifecycleLog.toString());
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/SettingsActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.app.AppCompatDelegate;
import androidx.appcompat.widget.SwitchCompat;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CompoundButton;
import android.widget.Toast;
import com.example.coursemanager.R;

/**
 * SETTINGS ACTIVITY
 * =================
 * SharedPreferences for persistent settings
 * 
 * Concepts Covered:
 * - SharedPreferences for data persistence
 * - getSharedPreferences(name, mode)
 * - SharedPreferences.Editor for writing
 * - editor.putBoolean() / putString() / putInt()
 * - editor.apply() / commit()
 * - prefs.getBoolean() for reading
 * - AppCompatDelegate for dark theme
 * 
 * SharedPreferences Pattern:
 * ┌─────────────────────────────────────────────────────────┐
 * │ WRITE:                                                  │
 * │ SharedPreferences prefs = getSharedPreferences(...)     │
 * │ SharedPreferences.Editor editor = prefs.edit()          │
 * │ editor.putBoolean("key", value)                         │
 * │ editor.apply()  // async                                │
 * ├─────────────────────────────────────────────────────────┤
 * │ READ:                                                   │
 * │ boolean value = prefs.getBoolean("key", defaultValue)   │
 * └─────────────────────────────────────────────────────────┘
 */
public class SettingsActivity extends AppCompatActivity {
    private SwitchCompat switchDarkMode;
    private Button btnClearData;
    private SharedPreferences sharedPreferences;
    private static final String PREFS_NAME = "AppSettings";
    private static final String KEY_DARK_MODE = "dark_mode";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_settings);

        switchDarkMode = findViewById(R.id.switchDarkMode);
        btnClearData = findViewById(R.id.btnClearData);

        // Get SharedPreferences
        sharedPreferences = getSharedPreferences(PREFS_NAME, MODE_PRIVATE);

        // Load saved preference
        boolean isDarkMode = sharedPreferences.getBoolean(KEY_DARK_MODE, false);
        switchDarkMode.setChecked(isDarkMode);

        // Dark mode toggle listener
        switchDarkMode.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                // Save preference
                SharedPreferences.Editor editor = sharedPreferences.edit();
                editor.putBoolean(KEY_DARK_MODE, isChecked);
                editor.apply();  // Async save

                // Apply theme
                if (isChecked) {
                    AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_YES);
                } else {
                    AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_NO);
                }

                Toast.makeText(SettingsActivity.this,
                        "Dark mode " + (isChecked ? "enabled" : "disabled"),
                        Toast.LENGTH_SHORT).show();
            }
        });

        // Clear data button
        btnClearData.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                // Clear all SharedPreferences
                SharedPreferences.Editor editor = sharedPreferences.edit();
                editor.clear();
                editor.apply();

                switchDarkMode.setChecked(false);
                Toast.makeText(SettingsActivity.this,
                        "All data cleared", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/activities/DatabaseActivity.java`

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.ListView;
import android.widget.Toast;
import com.example.coursemanager.R;
import com.example.coursemanager.adapters.StudentAdapter;
import com.example.coursemanager.models.Student;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;
import java.util.ArrayList;
import java.util.List;

/**
 * DATABASE ACTIVITY
 * =================
 * Firebase Database with ValueEventListener
 * 
 * Concepts Covered:
 * - FirebaseDatabase.getInstance()
 * - DatabaseReference
 * - setValue() for writing data
 * - addValueEventListener for reading
 * - DataSnapshot iteration
 * - getValue(Class) for deserialization
 * - BaseAdapter with ListView
 * 
 * Firebase Read Pattern:
 * databaseRef.addValueEventListener(new ValueEventListener() {
 *     onDataChange(DataSnapshot snapshot) {
 *         for (DataSnapshot child : snapshot.getChildren()) {
 *             Object obj = child.getValue(Model.class);
 *             list.add(obj);
 *         }
 *         adapter.notifyDataSetChanged();
 *     }
 * })
 */
public class DatabaseActivity extends AppCompatActivity {
    EditText stdID, stdname, stdage;
    Button btnsave, btnload;
    ListView lv;

    DatabaseReference databaseReference;
    List<Student> studentList = new ArrayList<>();
    StudentAdapter adapter;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_database);

        // Initialize views
        stdID = findViewById(R.id.StdID);
        stdname = findViewById(R.id.stdname);
        stdage = findViewById(R.id.stdage);
        btnsave = findViewById(R.id.btnsave);
        btnload = findViewById(R.id.btnload);
        lv = findViewById(R.id.listviewstd);

        // Initialize Firebase reference
        databaseReference = FirebaseDatabase.getInstance().getReference("Students");

        // Initialize adapter
        adapter = new StudentAdapter(studentList, this);
        lv.setAdapter(adapter);

        // Save button - Firebase CREATE
        btnsave.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                String id = stdID.getText().toString().trim();
                String name = stdname.getText().toString().trim();
                String ageStr = stdage.getText().toString().trim();

                if (id.isEmpty() || name.isEmpty() || ageStr.isEmpty()) {
                    Toast.makeText(DatabaseActivity.this,
                            "Please fill all fields", Toast.LENGTH_SHORT).show();
                    return;
                }

                int age = Integer.parseInt(ageStr);

                // Create student object
                Student student = new Student(id, name, age);

                // Save to Firebase using ID as key
                databaseReference.child(id).setValue(student)
                        .addOnSuccessListener(unused -> {
                            Toast.makeText(DatabaseActivity.this,
                                    "Student saved", Toast.LENGTH_SHORT).show();
                            // Clear fields
                            stdID.setText("");
                            stdname.setText("");
                            stdage.setText("");
                        })
                        .addOnFailureListener(e -> {
                            Toast.makeText(DatabaseActivity.this,
                                    "Error: " + e.getMessage(), Toast.LENGTH_SHORT).show();
                        });
            }
        });

        // Load button - Firebase READ with ValueEventListener
        btnload.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                databaseReference.addValueEventListener(new ValueEventListener() {
                    @Override
                    public void onDataChange(@NonNull DataSnapshot snapshot) {
                        // Clear existing list
                        studentList.clear();

                        // Iterate through all children
                        for (DataSnapshot dataSnapshot : snapshot.getChildren()) {
                            // Deserialize to Student object
                            Student student = dataSnapshot.getValue(Student.class);
                            if (student != null) {
                                studentList.add(student);
                            }
                        }

                        // Notify adapter of data change
                        adapter.notifyDataSetChanged();

                        Toast.makeText(DatabaseActivity.this,
                                "Loaded " + studentList.size() + " students",
                                Toast.LENGTH_SHORT).show();
                    }

                    @Override
                    public void onCancelled(@NonNull DatabaseError error) {
                        Toast.makeText(DatabaseActivity.this,
                                "Error: " + error.getMessage(),
                                Toast.LENGTH_SHORT).show();
                    }
                });
            }
        });
    }
}
```

---

### Step 9: Fragment Classes

**Path:** `app/src/main/java/com/example/coursemanager/fragments/CoursesFragment.java`

```java
package com.example.coursemanager.fragments;

import android.content.Intent;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ProgressBar;
import android.widget.TextView;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;
import com.example.coursemanager.R;
import com.example.coursemanager.activities.AddCourseActivity;
import com.example.coursemanager.adapters.CourseAdapter;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.google.android.material.floatingactionbutton.FloatingActionButton;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.ValueEventListener;
import java.util.ArrayList;
import java.util.List;

/**
 * COURSES FRAGMENT
 * ================
 * Displays courses in RecyclerView with Firebase READ
 * 
 * Concepts Covered:
 * - Fragment lifecycle (onCreateView, onStart)
 * - RecyclerView with LinearLayoutManager
 * - FloatingActionButton
 * - Firebase ValueEventListener for real-time updates
 * - Empty state handling
 * 
 * Fragment Lifecycle:
 * onAttach → onCreate → onCreateView → onViewCreated → 
 * onStart → onResume → [ACTIVE] → onPause → onStop → 
 * onDestroyView → onDestroy → onDetach
 */
public class CoursesFragment extends Fragment {
    private RecyclerView recyclerView;
    private CourseAdapter adapter;
    private List<Course> courseList = new ArrayList<>();
    private ProgressBar progressBar;
    private TextView txtEmptyState;
    private FloatingActionButton fabAddCourse;
    private FirebaseHelper firebaseHelper;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        // Inflate fragment layout
        return inflater.inflate(R.layout.fragment_courses, container, false);
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        // Initialize views
        recyclerView = view.findViewById(R.id.recyclerViewCourses);
        progressBar = view.findViewById(R.id.progressBar);
        txtEmptyState = view.findViewById(R.id.txtEmptyState);
        fabAddCourse = view.findViewById(R.id.fabAddCourse);

        firebaseHelper = new FirebaseHelper();

        // Setup RecyclerView
        recyclerView.setLayoutManager(new LinearLayoutManager(getContext()));
        adapter = new CourseAdapter(courseList, getContext());
        recyclerView.setAdapter(adapter);

        // FAB click - navigate to AddCourseActivity
        fabAddCourse.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(getActivity(), AddCourseActivity.class);
                startActivity(intent);
            }
        });
    }

    @Override
    public void onStart() {
        super.onStart();
        loadCourses();  // Refresh data when fragment becomes visible
    }

    /**
     * Loads courses from Firebase with real-time listener
     */
    private void loadCourses() {
        progressBar.setVisibility(View.VISIBLE);
        txtEmptyState.setVisibility(View.GONE);

        // Firebase READ with ValueEventListener
        firebaseHelper.getDatabaseReference().addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot snapshot) {
                courseList.clear();

                // Iterate and deserialize
                for (DataSnapshot dataSnapshot : snapshot.getChildren()) {
                    Course course = dataSnapshot.getValue(Course.class);
                    if (course != null) {
                        courseList.add(course);
                    }
                }

                adapter.notifyDataSetChanged();
                progressBar.setVisibility(View.GONE);

                // Show empty state if no courses
                if (courseList.isEmpty()) {
                    txtEmptyState.setVisibility(View.VISIBLE);
                } else {
                    txtEmptyState.setVisibility(View.GONE);
                }
            }

            @Override
            public void onCancelled(@NonNull DatabaseError error) {
                progressBar.setVisibility(View.GONE);
                txtEmptyState.setText("Error loading courses");
                txtEmptyState.setVisibility(View.VISIBLE);
            }
        });
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/fragments/StatsFragment.java`

```java
package com.example.coursemanager.fragments;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.ValueEventListener;

/**
 * STATS FRAGMENT
 * ==============
 * Shows course statistics calculated from Firebase data
 * 
 * Concepts Covered:
 * - Fragment with data calculations
 * - CardView for statistics display
 * - Firebase data aggregation
 */
public class StatsFragment extends Fragment {
    private TextView txtTotalCourses, txtTotalCredits, txtAverageCredits;
    private FirebaseHelper firebaseHelper;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_stats, container, false);
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        txtTotalCourses = view.findViewById(R.id.txtTotalCourses);
        txtTotalCredits = view.findViewById(R.id.txtTotalCredits);
        txtAverageCredits = view.findViewById(R.id.txtAverageCredits);

        firebaseHelper = new FirebaseHelper();
    }

    @Override
    public void onStart() {
        super.onStart();
        loadStats();
    }

    private void loadStats() {
        firebaseHelper.getDatabaseReference().addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot snapshot) {
                int totalCourses = 0;
                int totalCredits = 0;

                for (DataSnapshot dataSnapshot : snapshot.getChildren()) {
                    Course course = dataSnapshot.getValue(Course.class);
                    if (course != null) {
                        totalCourses++;
                        totalCredits += course.getCreditHours();
                    }
                }

                double average = totalCourses > 0 ? (double) totalCredits / totalCourses : 0;

                // Update UI
                txtTotalCourses.setText("Total Courses: " + totalCourses);
                txtTotalCredits.setText("Total Credits: " + totalCredits);
                txtAverageCredits.setText(String.format("Average Credits: %.1f", average));
            }

            @Override
            public void onCancelled(@NonNull DatabaseError error) {
                // Handle error
            }
        });
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/fragments/ProfileFragment.java`

```java
package com.example.coursemanager.fragments;

import android.content.Intent;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;
import com.example.coursemanager.activities.LifecycleActivity;
import com.example.coursemanager.activities.SettingsActivity;
import com.example.coursemanager.services.DataSyncService;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

/**
 * PROFILE FRAGMENT
 * ================
 * Google Maps integration with navigation buttons
 * 
 * Concepts Covered:
 * - SupportMapFragment (nested fragment)
 * - OnMapReadyCallback interface
 * - GoogleMap object
 * - LatLng for coordinates
 * - MarkerOptions for map markers
 * - CameraUpdateFactory for map camera
 * - Starting services from fragment
 * 
 * Google Maps Setup:
 * 1. Get SupportMapFragment from childFragmentManager
 * 2. Call getMapAsync(callback)
 * 3. Implement onMapReady(GoogleMap)
 * 4. Add markers, move camera
 */
public class ProfileFragment extends Fragment implements OnMapReadyCallback {
    private GoogleMap mMap;
    private Button btnSettings, btnLifecycle, btnStartService;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_profile, container, false);
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        btnSettings = view.findViewById(R.id.btnSettings);
        btnLifecycle = view.findViewById(R.id.btnLifecycle);
        btnStartService = view.findViewById(R.id.btnStartService);

        // Get map fragment and request async callback
        SupportMapFragment mapFragment = (SupportMapFragment)
                getChildFragmentManager().findFragmentById(R.id.map);
        if (mapFragment != null) {
            mapFragment.getMapAsync(this);
        }

        // Settings button
        btnSettings.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(getActivity(), SettingsActivity.class);
                startActivity(intent);
            }
        });

        // Lifecycle demo button
        btnLifecycle.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(getActivity(), LifecycleActivity.class);
                startActivity(intent);
            }
        });

        // Start sync service button
        btnStartService.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent serviceIntent = new Intent(getActivity(), DataSyncService.class);
                getActivity().startService(serviceIntent);
                Toast.makeText(getContext(), "Data Sync Service Started",
                        Toast.LENGTH_SHORT).show();
            }
        });
    }

    /**
     * Called when GoogleMap is ready
     * Implements OnMapReadyCallback
     */
    @Override
    public void onMapReady(@NonNull GoogleMap googleMap) {
        mMap = googleMap;

        // Add marker at sample location
        LatLng location = new LatLng(33.6844, 73.0479);  // Islamabad coordinates
        mMap.addMarker(new MarkerOptions()
                .position(location)
                .title("My Location"));

        // Move camera to location with zoom
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(location, 12f));
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/fragments/HomeFragment.java`

```java
package com.example.coursemanager.fragments;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;

/**
 * HOME FRAGMENT
 * =============
 * Simple fragment for DrawerLayout navigation
 * 
 * Concepts Covered:
 * - Basic Fragment structure
 * - onCreateView for layout inflation
 */
public class HomeFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_home, container, false);
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/fragments/SettingFragment.java`

```java
package com.example.coursemanager.fragments;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;

/**
 * SETTING FRAGMENT
 * ================
 * Settings fragment for DrawerLayout navigation
 */
public class SettingFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_setting, container, false);
    }
}
```

**Path:** `app/src/main/java/com/example/coursemanager/fragments/MapsFragment.java`

```java
package com.example.coursemanager.fragments;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;
import com.google.android.gms.maps.CameraUpdateFactory;
import com.google.android.gms.maps.GoogleMap;
import com.google.android.gms.maps.OnMapReadyCallback;
import com.google.android.gms.maps.SupportMapFragment;
import com.google.android.gms.maps.model.LatLng;
import com.google.android.gms.maps.model.MarkerOptions;

/**
 * MAPS FRAGMENT
 * =============
 * Standalone Google Maps fragment
 * 
 * Concepts Covered:
 * - SupportMapFragment integration
 * - OnMapReadyCallback
 * - GoogleMap, LatLng, MarkerOptions
 * - CameraUpdateFactory
 */
public class MapsFragment extends Fragment implements OnMapReadyCallback {
    private GoogleMap mMap;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater,
                             @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_maps, container, false);
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);

        // Get nested map fragment
        SupportMapFragment mapFragment = (SupportMapFragment)
                getChildFragmentManager().findFragmentById(R.id.mapfragment);
        if (mapFragment != null) {
            mapFragment.getMapAsync(this);
        }
    }

    @Override
    public void onMapReady(@NonNull GoogleMap googleMap) {
        mMap = googleMap;

        // Add marker
        LatLng islamabad = new LatLng(33.6844, 73.0479);
        mMap.addMarker(new MarkerOptions()
                .position(islamabad)
                .title("Islamabad"));
        mMap.moveCamera(CameraUpdateFactory.newLatLngZoom(islamabad, 10f));
    }
}
```

---

### Step 10: Layout XML Files

**Path:** `app/src/main/res/layout/activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
MAIN ACTIVITY LAYOUT
BottomNavigationView with Fragment container
┌─────────────────────────────────────┐
│                                     │
│     ┌───────────────────────┐       │
│     │   FrameLayout         │       │
│     │   (Fragment Container)│       │
│     │                       │       │
│     └───────────────────────┘       │
│                                     │
├─────────────────────────────────────┤
│  [Courses] [Stats] [Profile]        │ ← BottomNavigationView
└─────────────────────────────────────┘
-->
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Fragment Container -->
    <FrameLayout
        android:id="@+id/fragmentContainer"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@id/bottomNavigation" />

    <!-- Bottom Navigation -->
    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomNavigation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:background="?android:attr/windowBackground"
        app:menu="@menu/bottom_nav_menu" />

</RelativeLayout>
```

**Path:** `app/src/main/res/layout/activity_main2.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
MAIN ACTIVITY 2 LAYOUT
ListView for menu navigation
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Select Feature"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="16dp" />

    <ListView
        android:id="@+id/listmenu"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_main4.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
MAIN ACTIVITY 4 LAYOUT
DrawerLayout with NavigationView
-->
<androidx.drawerlayout.widget.DrawerLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Main Content -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <androidx.appcompat.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            android:background="@color/colorPrimary"
            app:titleTextColor="@android:color/white" />

        <FrameLayout
            android:id="@+id/fragment_container"
            android:layout_width="match_parent"
            android:layout_height="match_parent" />

    </LinearLayout>

    <!-- Navigation Drawer -->
    <com.google.android.material.navigation.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        app:menu="@menu/drawer_menu" />

</androidx.drawerlayout.widget.DrawerLayout>
```

**Path:** `app/src/main/res/layout/activity_main5.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
MAIN ACTIVITY 5 LAYOUT
Thread countdown display
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="CountDown: 10"
        android:textSize="48sp"
        android:textStyle="bold" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_main6.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
MAIN ACTIVITY 6 LAYOUT
Services demo with buttons
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="UNBOUND SERVICE"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginBottom="16dp" />

    <Button
        android:id="@+id/unboundPlay"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Unbound Service Play"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/unboundStop"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Unbound Service Stop"
        android:layout_marginBottom="32dp" />

    <View
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="#CCCCCC"
        android:layout_marginBottom="32dp" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="BOUND SERVICE"
        android:textSize="20sp"
        android:textStyle="bold"
        android:layout_marginBottom="16dp" />

    <Button
        android:id="@+id/boundPlay"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Bound Service Play"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/boundStop"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Bound Service Stop" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_add_course.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
ADD COURSE ACTIVITY LAYOUT
Form with TextInputLayout fields
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Add New Course"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="32dp" />

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Course Name"
        android:layout_marginBottom="16dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCourseName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Course Code"
        android:layout_marginBottom="16dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCourseCode"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Credit Hours"
        android:layout_marginBottom="24dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCreditHours"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="number" />
    </com.google.android.material.textfield.TextInputLayout>

    <ProgressBar
        android:id="@+id/progressBar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        style="?android:attr/progressBarStyleHorizontal"
        android:indeterminate="true"
        android:visibility="gone" />

    <Button
        android:id="@+id/btnAddCourse"
        android:layout_width="match_parent"
        android:layout_height="60dp"
        android:text="Add Course"
        android:textSize="18sp"
        android:backgroundTint="@color/colorPrimary" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_update_course.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
UPDATE COURSE ACTIVITY LAYOUT
Pre-filled form for editing
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Update Course"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="32dp" />

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Course Name"
        android:layout_marginBottom="16dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCourseName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Course Code"
        android:layout_marginBottom="16dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCourseCode"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="text" />
    </com.google.android.material.textfield.TextInputLayout>

    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Credit Hours"
        android:layout_marginBottom="24dp">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/edtCreditHours"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:inputType="number" />
    </com.google.android.material.textfield.TextInputLayout>

    <ProgressBar
        android:id="@+id/progressBar"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        style="?android:attr/progressBarStyleHorizontal"
        android:indeterminate="true"
        android:visibility="gone" />

    <Button
        android:id="@+id/btnUpdateCourse"
        android:layout_width="match_parent"
        android:layout_height="60dp"
        android:text="Update Course"
        android:textSize="18sp"
        android:backgroundTint="@color/colorPrimary" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_lifecycle.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
LIFECYCLE ACTIVITY LAYOUT
Shows lifecycle states in real-time
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Activity Lifecycle Tracker"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="24dp" />

    <!-- Current State Display -->
    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        app:cardElevation="4dp"
        app:cardCornerRadius="8dp">

        <TextView
            android:id="@+id/txtCurrentState"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Current State: onCreate()"
            android:textSize="20sp"
            android:textStyle="bold"
            android:padding="16dp"
            android:gravity="center"
            android:textColor="@color/colorPrimary" />
    </androidx.cardview.widget.CardView>

    <!-- Lifecycle Log Title -->
    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Lifecycle History:"
        android:textSize="18sp"
        android:textStyle="bold"
        android:layout_marginBottom="8dp" />

    <!-- Lifecycle Log Scroll View -->
    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:id="@+id/txtLifecycleLog"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text=""
            android:textSize="16sp"
            android:padding="16dp"
            android:background="#F5F5F5"
            android:fontFamily="monospace" />
    </ScrollView>

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_settings.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
SETTINGS ACTIVITY LAYOUT
Dark mode toggle and clear data
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Settings"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="24dp" />

    <!-- Dark Mode Setting -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="16dp"
        android:background="?attr/selectableItemBackground">

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Dark Theme"
            android:textSize="18sp" />

        <androidx.appcompat.widget.SwitchCompat
            android:id="@+id/switchDarkMode"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content" />
    </LinearLayout>

    <View
        android:layout_width="match_parent"
        android:layout_height="1dp"
        android:background="#E0E0E0" />

    <!-- Clear Data Button -->
    <Button
        android:id="@+id/btnClearData"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Clear All Data"
        android:layout_marginTop="24dp"
        style="?attr/borderlessButtonStyle"
        android:textColor="@android:color/holo_red_dark" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/activity_database.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
DATABASE ACTIVITY LAYOUT
Student form with ListView
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/StdID"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Student ID"
        android:layout_marginBottom="8dp" />

    <EditText
        android:id="@+id/stdname"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your Name"
        android:layout_marginBottom="8dp" />

    <EditText
        android:id="@+id/stdage"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your Age"
        android:inputType="number"
        android:layout_marginBottom="16dp" />

    <Button
        android:id="@+id/btnsave"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Save to the Database"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnload"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Read From the Database"
        android:layout_marginBottom="16dp" />

    <!-- Header Row -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:padding="8dp"
        android:background="#E0E0E0">

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Name"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Roll No"
            android:textStyle="bold" />

        <TextView
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:text="Age"
            android:textStyle="bold" />
    </LinearLayout>

    <ListView
        android:id="@+id/listviewstd"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/fragment_courses.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
COURSES FRAGMENT LAYOUT
RecyclerView with FAB
-->
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="8dp">

    <!-- Progress Bar -->
    <ProgressBar
        android:id="@+id/progressBar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:visibility="gone" />

    <!-- Empty State Text -->
    <TextView
        android:id="@+id/txtEmptyState"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="No courses yet"
        android:textSize="18sp"
        android:visibility="gone" />

    <!-- Courses RecyclerView -->
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerViewCourses"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:clipToPadding="false"
        android:paddingBottom="80dp" />

    <!-- Floating Action Button -->
    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fabAddCourse"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"
        android:layout_alignParentBottom="true"
        android:layout_margin="16dp"
        android:src="@android:drawable/ic_input_add"
        app:tint="@android:color/white"
        app:backgroundTint="@color/colorPrimary" />

</RelativeLayout>
```

**Path:** `app/src/main/res/layout/fragment_stats.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
STATS FRAGMENT LAYOUT
Statistics cards
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <TextView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Course Statistics"
        android:textSize="24sp"
        android:textStyle="bold"
        android:gravity="center"
        android:layout_marginBottom="24dp" />

    <!-- Total Courses Card -->
    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        app:cardElevation="4dp"
        app:cardCornerRadius="8dp">

        <TextView
            android:id="@+id/txtTotalCourses"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Total Courses: 0"
            android:textSize="20sp"
            android:padding="20dp"
            android:gravity="center" />
    </androidx.cardview.widget.CardView>

    <!-- Total Credits Card -->
    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp"
        app:cardElevation="4dp"
        app:cardCornerRadius="8dp">

        <TextView
            android:id="@+id/txtTotalCredits"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Total Credits: 0"
            android:textSize="20sp"
            android:padding="20dp"
            android:gravity="center" />
    </androidx.cardview.widget.CardView>

    <!-- Average Credits Card -->
    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:cardElevation="4dp"
        app:cardCornerRadius="8dp">

        <TextView
            android:id="@+id/txtAverageCredits"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Average Credits: 0.0"
            android:textSize="20sp"
            android:padding="20dp"
            android:gravity="center" />
    </androidx.cardview.widget.CardView>

</LinearLayout>
```

**Path:** `app/src/main/res/layout/fragment_profile.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
PROFILE FRAGMENT LAYOUT
Map with action buttons
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <!-- Google Map Fragment -->
    <fragment
        android:id="@+id/map"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <!-- Button Container -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="16dp">

        <Button
            android:id="@+id/btnSettings"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Settings"
            android:layout_marginBottom="8dp" />

        <Button
            android:id="@+id/btnLifecycle"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Lifecycle Demo"
            android:layout_marginBottom="8dp" />

        <Button
            android:id="@+id/btnStartService"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Start Sync Service" />

    </LinearLayout>

</LinearLayout>
```

**Path:** `app/src/main/res/layout/fragment_home.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Home Fragment"
        android:textSize="24sp"
        android:textStyle="bold" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/fragment_setting.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Setting Fragment"
        android:textSize="24sp"
        android:textStyle="bold" />

</LinearLayout>
```

**Path:** `app/src/main/res/layout/fragment_maps.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <fragment
        android:id="@+id/mapfragment"
        android:name="com.google.android.gms.maps.SupportMapFragment"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</FrameLayout>
```

**Path:** `app/src/main/res/layout/item_course_card.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
COURSE CARD ITEM LAYOUT
RecyclerView item with CardView
-->
<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/cardView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_margin="8dp"
    app:cardElevation="4dp"
    app:cardCornerRadius="8dp">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="16dp">

        <!-- Course Name -->
        <TextView
            android:id="@+id/txtCourseName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Course Name"
            android:textSize="20sp"
            android:textStyle="bold"
            android:textColor="@android:color/black"
            android:layout_marginBottom="8dp" />

        <!-- Course Code -->
        <TextView
            android:id="@+id/txtCourseCode"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Code: CS101"
            android:textSize="16sp"
            android:textColor="@android:color/darker_gray"
            android:layout_marginBottom="4dp" />

        <!-- Credit Hours -->
        <TextView
            android:id="@+id/txtCreditHours"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Credits: 3"
            android:textSize="16sp"
            android:textColor="@android:color/darker_gray"
            android:layout_marginBottom="12dp" />

        <!-- Buttons Container -->
        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:orientation="horizontal">

            <Button
                android:id="@+id/btnUpdate"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Update"
                android:layout_marginEnd="8dp"
                style="?attr/materialButtonOutlinedStyle" />

            <Button
                android:id="@+id/btnDelete"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_weight="1"
                android:text="Delete"
                android:backgroundTint="@android:color/holo_red_light" />

        </LinearLayout>

    </LinearLayout>

</androidx.cardview.widget.CardView>
```

**Path:** `app/src/main/res/layout/recyclerviewlayout.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
STUDENT LIST ITEM LAYOUT
For BaseAdapter ListView
-->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="horizontal"
    android:padding="12dp">

    <TextView
        android:id="@+id/textName"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="Name"
        android:textSize="16sp" />

    <TextView
        android:id="@+id/textrollno"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="Roll No"
        android:textSize="16sp" />

    <TextView
        android:id="@+id/textAge"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_weight="1"
        android:text="Age"
        android:textSize="16sp" />

</LinearLayout>
```

---

### Step 11: Menu Files

**Path:** `app/src/main/res/menu/bottom_nav_menu.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
BOTTOM NAVIGATION MENU
Three navigation items
-->
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/nav_courses"
        android:icon="@android:drawable/ic_menu_view"
        android:title="Courses" />

    <item
        android:id="@+id/nav_stats"
        android:icon="@android:drawable/ic_menu_sort_by_size"
        android:title="Stats" />

    <item
        android:id="@+id/nav_profile"
        android:icon="@android:drawable/ic_menu_myplaces"
        android:title="Profile" />
</menu>
```

**Path:** `app/src/main/res/menu/drawer_menu.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<!--
DRAWER NAVIGATION MENU
Navigation drawer menu items
-->
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/nav_home"
        android:icon="@android:drawable/ic_menu_compass"
        android:title="HOME" />

    <item
        android:id="@+id/nav_setting"
        android:icon="@android:drawable/ic_menu_preferences"
        android:title="SETTING" />

    <item
        android:id="@+id/nav_map"
        android:icon="@android:drawable/ic_menu_mapmode"
        android:title="MAP" />
</menu>
```

---

### Step 12: Values Files

**Path:** `app/src/main/res/values/strings.xml`

```xml
<resources>
    <string name="app_name">Course Manager</string>
    <string name="add_course">Add Course</string>
    <string name="update_course">Update Course</string>
    <string name="delete_course">Delete Course</string>
    <string name="course_name">Course Name</string>
    <string name="course_code">Course Code</string>
    <string name="credit_hours">Credit Hours</string>
    <string name="settings">Settings</string>
    <string name="lifecycle">Lifecycle Demo</string>
    <string name="dark_mode">Dark Mode</string>
    <string name="navigation_drawer_open">Open navigation drawer</string>
    <string name="navigation_drawer_close">Close navigation drawer</string>
</resources>
```

**Path:** `app/src/main/res/values/colors.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <color name="colorPrimary">#6200EE</color>
    <color name="colorPrimaryDark">#3700B3</color>
    <color name="colorAccent">#03DAC5</color>
    <color name="white">#FFFFFF</color>
    <color name="black">#000000</color>
</resources>
```

**Path:** `app/src/main/res/values/themes.xml`

```xml
<resources>
    <!-- Base application theme -->
    <style name="Theme.CourseManager" parent="Theme.AppCompat.Light.DarkActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>
</resources>
```

---

## Firebase Setup Instructions

### Step 1: Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project"
3. Enter project name: "CourseManager"
4. Enable Google Analytics (optional)
5. Click "Create project"

### Step 2: Add Android App
1. In Firebase Console, click Android icon
2. Enter package name: `com.example.coursemanager`
3. Download `google-services.json`
4. Place in `app/` directory

### Step 3: Enable Realtime Database
1. Go to Realtime Database section
2. Click "Create Database"
3. Choose region
4. Select "Start in test mode" (for development)
5. Set rules:
```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

### Firebase Database Structure
```
root/
├── Courses/
│   ├── -NxYz123abc/
│   │   ├── id: "-NxYz123abc"
│   │   ├── courseName: "Mobile Development"
│   │   ├── courseCode: "CS401"
│   │   └── creditHours: 3
│   └── -NxYz456def/
│       └── ...
└── Students/
    ├── STD001/
    │   ├── ID: "STD001"
    │   ├── Name: "John Doe"
    │   └── Age: 20
    └── ...
```

---

## Google Maps Setup

### Step 1: Get API Key
1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create new project or select existing
3. Enable Maps SDK for Android
4. Create API Key credentials
5. Restrict key to Android apps

### Step 2: Add API Key
In `AndroidManifest.xml`:
```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_API_KEY_HERE" />
```

---

## Quick Reference - Key Code Patterns

### Firebase CRUD Summary
```java
// CREATE
databaseRef.push().getKey();
databaseRef.child(key).setValue(object);

// READ
databaseRef.addValueEventListener(new ValueEventListener() {
    onDataChange(DataSnapshot snapshot) {
        for (DataSnapshot child : snapshot.getChildren()) {
            Model obj = child.getValue(Model.class);
        }
    }
});

// UPDATE
databaseRef.child(id).setValue(updatedObject);

// DELETE
databaseRef.child(id).removeValue();
```

### Intent Data Passing
```java
// Send data
Intent intent = new Intent(this, TargetActivity.class);
intent.putExtra("key", value);
startActivity(intent);

// Receive data
String value = getIntent().getStringExtra("key");
int intValue = getIntent().getIntExtra("key", defaultValue);
```

### Fragment Transaction
```java
getSupportFragmentManager()
    .beginTransaction()
    .replace(R.id.container, new MyFragment())
    .commit();
```

### Service Patterns
```java
// Unbound Service
startService(new Intent(this, MyService.class));
stopService(new Intent(this, MyService.class));

// Bound Service
bindService(intent, serviceConnection, BIND_AUTO_CREATE);
unbindService(serviceConnection);
```

### SharedPreferences
```java
// Write
SharedPreferences.Editor editor = prefs.edit();
editor.putBoolean("key", value);
editor.apply();

// Read
boolean value = prefs.getBoolean("key", defaultValue);
```

### Handler + Thread
```java
Handler handler = new Handler(Looper.getMainLooper());
new Thread(() -> {
    // Background work
    handler.post(() -> {
        // UI update
    });
}).start();
```

---

## Complete Concept Coverage Checklist

| # | Concept | Status |
|---|---------|--------|
| 1 | Activity Lifecycle | ✅ |
| 2 | ListView + ArrayAdapter | ✅ |
| 3 | RecyclerView + Adapter | ✅ |
| 4 | BaseAdapter (Custom) | ✅ |
| 5 | Switch Statement | ✅ |
| 6 | Explicit Intent | ✅ |
| 7 | Intent Extras | ✅ |
| 8 | Fragments | ✅ |
| 9 | Fragment Transactions | ✅ |
| 10 | BottomNavigationView | ✅ |
| 11 | DrawerLayout | ✅ |
| 12 | NavigationView | ✅ |
| 13 | Notifications (NotificationCompat) | ✅ |
| 14 | NotificationChannel | ✅ |
| 15 | PendingIntent | ✅ |
| 16 | Thread | ✅ |
| 17 | Handler | ✅ |
| 18 | Runnable | ✅ |
| 19 | Unbound Service | ✅ |
| 20 | Bound Service | ✅ |
| 21 | LocalBinder | ✅ |
| 22 | ServiceConnection | ✅ |
| 23 | MediaPlayer | ✅ |
| 24 | Firebase Database | ✅ |
| 25 | DatabaseReference | ✅ |
| 26 | ValueEventListener | ✅ |
| 27 | DataSnapshot | ✅ |
| 28 | SharedPreferences | ✅ |
| 29 | Google Maps | ✅ |
| 30 | SupportMapFragment | ✅ |
| 31 | OnMapReadyCallback | ✅ |
| 32 | LatLng + MarkerOptions | ✅ |
| 33 | CardView | ✅ |
| 34 | FloatingActionButton | ✅ |
| 35 | TextInputLayout | ✅ |
| 36 | ProgressBar | ✅ |
| 37 | Toast | ✅ |

---

## Running the Project

1. **Clone/Create Project** in Android Studio
2. **Add Firebase** - Place `google-services.json` in `app/`
3. **Add Google Maps API Key** in `AndroidManifest.xml`
4. **Sync Gradle** - Click "Sync Now"
5. **Build & Run** on emulator or device

---

*This README covers all syllabus concepts for the Android Mobile Application Development course with complete, runnable code examples.*
"# mad-code" 
