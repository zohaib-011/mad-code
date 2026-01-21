# Code Overview - Course Management System

This document explains **what each code file does** in simple English.

---

## 📦 Model Classes - Data Storage

### Course.java
**What it does:** This is a container that holds course information.
- Stores: Course name, course code, credit hours, and unique ID
- Used when: Saving courses to database, displaying in lists
- **Concept:** Java class with getters and setters

### Student.java
**What it does:** This is a container that holds student information.
- Stores: Student name, roll number
- Used when: Demonstrating Firebase with different data type
- **Concept:** Java class with getters and setters

---

## 🔧 Utility Classes - Helper Functions

### FirebaseHelper.java
**What it does:** Handles all communication with Firebase database.
- **addCourse()** - Saves new course to cloud database (CREATE)
- **updateCourse()** - Changes existing course data (UPDATE)
- **deleteCourse()** - Removes course from database (DELETE)
- **getDatabaseReference()** - Gets connection to database for reading (READ)
- **Concept:** Firebase Realtime Database, CRUD Operations

### NotificationHelper.java
**What it does:** Creates and shows notifications on phone.
- Creates a notification channel (required for Android 8+)
- Builds notification with title, message, and icon
- When user clicks notification, opens the app
- **Concept:** NotificationCompat, NotificationChannel, PendingIntent

---

## 🔄 Adapter Classes - Connect Data to Views

### CourseAdapter.java
**What it does:** Takes list of courses and displays them in cards.
- Creates a card view for each course
- Shows course name, code, and credits on card
- Update button → Opens edit screen with course data
- Delete button → Removes course from database
- **Concept:** RecyclerView.Adapter, ViewHolder Pattern, CardView

### StudentAdapter.java
**What it does:** Takes list of students and displays in simple list.
- Creates a row for each student
- Shows student name and roll number
- Uses older ListView approach (for learning)
- **Concept:** BaseAdapter, Custom ListView, getView() method

---

## 🎵 Service Classes - Background Tasks

### MusicService.java (Unbound Service)
**What it does:** Plays music in background even when app is closed.
- Starts playing when user clicks "Start Music"
- Keeps playing when user leaves app
- Stops only when user clicks "Stop Music"
- **Concept:** Service, startService(), stopService(), MediaPlayer

### MybindService.java (Bound Service)
**What it does:** Plays music but connected to the activity.
- Only plays while activity is connected to it
- Stops automatically when activity closes
- Returns a binder to communicate with activity
- **Concept:** Bound Service, LocalBinder, onBind(), ServiceConnection

### DataSyncService.java
**What it does:** Runs background task to sync data.
- Uses Thread to run work without freezing screen
- Uses Handler to update screen from background
- Shows how to do background processing
- **Concept:** Service, Thread, Handler, Background Processing

---

## 📱 Activity Classes - App Screens

### MainActivity.java
**What it does:** Main screen with bottom tabs.
- Shows 3 tabs at bottom: Courses, Stats, Profile
- When user taps tab, changes the fragment displayed
- Entry point of the app
- **Concept:** BottomNavigationView, Fragment Transaction, switch statement

### MainActivity2.java
**What it does:** Menu screen with list of options.
- Shows list of menu items (Lifecycle, Color, Intent, etc.)
- When user taps item, opens corresponding activity
- Uses switch statement to decide which screen to open
- **Concept:** ListView, ArrayAdapter, OnItemClickListener, switch, Intent

### MainActivity4.java
**What it does:** Screen with side drawer menu.
- Has hamburger menu (☰) at top
- Swipe from left or tap menu to open drawer
- Shows menu items: Home, Settings, Maps
- **Concept:** DrawerLayout, NavigationView, Fragment switching

### MainActivity5.java
**What it does:** Demonstrates countdown using Thread.
- Shows countdown from 10 to 0 on screen
- Thread runs in background counting down
- Handler updates the TextView on screen
- **Concept:** Thread, Handler, Runnable, Background to UI communication

### MainActivity6.java
**What it does:** Demonstrates both types of services.
- Start Service button → Starts music (unbound)
- Stop Service button → Stops music
- Bind Service button → Connects to bound service
- Unbind button → Disconnects from service
- **Concept:** startService, stopService, bindService, unbindService, ServiceConnection

### AddCourseActivity.java
**What it does:** Form to add new course.
- Text fields for: Course Name, Course Code, Credit Hours
- Add button saves course to Firebase
- Shows loading indicator while saving
- Shows notification when course is added
- Goes back to previous screen after adding
- **Concept:** TextInputLayout, Firebase CREATE, ProgressBar, Notification, finish()

### UpdateCourseActivity.java
**What it does:** Form to edit existing course.
- Receives course data from previous screen (Intent extras)
- Pre-fills the form with existing data
- Update button saves changes to Firebase
- Shows notification when updated
- **Concept:** Intent getExtras, Firebase UPDATE, Notification

### LifecycleActivity.java
**What it does:** Shows activity lifecycle states.
- Displays which lifecycle method is currently running
- onCreate → onStart → onResume → (visible)
- onPause → onStop → onDestroy → (closed)
- Shows Toast message for each state change
- **Concept:** Activity Lifecycle, onCreate, onStart, onResume, onPause, onStop, onDestroy

### SettingsActivity.java
**What it does:** Settings screen with toggle switch.
- Dark mode toggle - saves preference
- Clear data button
- Uses SharedPreferences to save settings
- Settings persist even after app closes
- **Concept:** SharedPreferences, SwitchCompat, putBoolean, getBoolean

### DatabaseActivity.java
**What it does:** Form to add students to database.
- Enter student name and roll number
- Add button saves to Firebase
- List below shows all students
- Demonstrates ValueEventListener for real-time updates
- **Concept:** Firebase, ValueEventListener, ListView, Real-time sync

---

## 🧩 Fragment Classes - Reusable Screen Parts

### CoursesFragment.java
**What it does:** Shows list of all courses.
- Displays courses in RecyclerView with cards
- Floating button to add new course
- Listens to Firebase for real-time updates
- When course added/deleted, list updates automatically
- **Concept:** Fragment, RecyclerView, FloatingActionButton, ValueEventListener

### StatsFragment.java
**What it does:** Shows course statistics.
- Calculates total number of courses
- Calculates total credit hours
- Displays in nice card layouts
- Updates when data changes
- **Concept:** Fragment, Data Aggregation, CardView

### ProfileFragment.java
**What it does:** Shows map and navigation options.
- Displays Google Map with location marker
- Buttons to navigate to other screens
- Map shows university/campus location
- **Concept:** Fragment, SupportMapFragment, OnMapReadyCallback, Google Maps

### HomeFragment.java
**What it does:** Simple home screen for drawer navigation.
- Just shows "Home" text
- Used as default screen in DrawerLayout
- **Concept:** Basic Fragment

### SettingFragment.java
**What it does:** Settings screen for drawer navigation.
- Shows settings options
- Used in DrawerLayout navigation
- **Concept:** Basic Fragment

### MapsFragment.java
**What it does:** Standalone map fragment.
- Shows full-screen Google Map
- Adds marker at specific location
- Used to demonstrate map integration
- **Concept:** SupportMapFragment, OnMapReadyCallback, MarkerOptions

---

## 📐 Layout XML Files - Screen Designs

| Layout File | What It Creates |
|-------------|-----------------|
| **activity_main.xml** | Screen with fragment container + bottom navigation bar |
| **activity_main2.xml** | Screen with scrollable list of menu items |
| **activity_main4.xml** | Screen with slide-out drawer menu |
| **activity_main5.xml** | Screen with countdown text display |
| **activity_main6.xml** | Screen with 4 buttons for service controls |
| **activity_add_course.xml** | Form with 3 input fields + add button |
| **activity_update_course.xml** | Form with 3 input fields + update button |
| **activity_lifecycle.xml** | Screen showing lifecycle state text |
| **activity_settings.xml** | Screen with toggle switch + clear button |
| **activity_database.xml** | Form with 2 input fields + student list |
| **fragment_courses.xml** | Course list + floating add button |
| **fragment_stats.xml** | Statistics cards display |
| **fragment_profile.xml** | Map view + navigation buttons |
| **fragment_home.xml** | Simple text display |
| **fragment_setting.xml** | Settings text display |
| **fragment_maps.xml** | Full-screen map view |
| **item_course_card.xml** | Single course card with buttons |
| **recyclerviewlayout.xml** | Single student row in list |

---

## 📋 Menu Files

| Menu File | What It Creates |
|-----------|-----------------|
| **bottom_nav_menu.xml** | 3 tabs: Courses, Stats, Profile with icons |
| **drawer_menu.xml** | 3 items: Home, Settings, Maps in side drawer |

---

## 🎨 Values Files

| Values File | What It Contains |
|-------------|------------------|
| **strings.xml** | All text used in app (app name, button labels, etc.) |
| **colors.xml** | Color codes for app theme (primary, secondary colors) |
| **themes.xml** | App theme settings (Material Design theme) |

---

## 🔗 Concept to Code Mapping Summary

| Concept | Where It's Used |
|---------|-----------------|
| **Activity Lifecycle** | LifecycleActivity.java shows all 6 lifecycle methods |
| **ListView + ArrayAdapter** | MainActivity2.java creates menu list |
| **Switch Statement** | MainActivity2.java decides which screen to open |
| **Explicit Intent** | All activities use Intent to navigate |
| **Intent putExtra** | UpdateCourseActivity receives course data |
| **Notifications** | NotificationHelper.java creates notifications |
| **NotificationChannel** | Required for Android 8+, created in NotificationHelper |
| **Fragments** | 6 fragments used for reusable UI sections |
| **Fragment Transaction** | MainActivity.java switches between fragments |
| **DrawerLayout** | MainActivity4.java has slide-out menu |
| **NavigationView** | MainActivity4.java menu items |
| **Thread** | MainActivity5.java runs countdown in background |
| **Handler** | MainActivity5.java updates UI from thread |
| **Unbound Service** | MusicService.java runs independently |
| **Bound Service** | MybindService.java connects to activity |
| **ServiceConnection** | MainActivity6.java connects to bound service |
| **MediaPlayer** | Both services play audio files |
| **Firebase CREATE** | FirebaseHelper.addCourse() |
| **Firebase READ** | CoursesFragment uses ValueEventListener |
| **Firebase UPDATE** | FirebaseHelper.updateCourse() |
| **Firebase DELETE** | FirebaseHelper.deleteCourse() |
| **ValueEventListener** | CoursesFragment listens for data changes |
| **RecyclerView Adapter** | CourseAdapter.java with ViewHolder |
| **BaseAdapter** | StudentAdapter.java for ListView |
| **CardView** | item_course_card.xml for course cards |
| **BottomNavigationView** | MainActivity.java bottom tabs |
| **FloatingActionButton** | fragment_courses.xml add button |
| **Google Maps** | MapsFragment and ProfileFragment |
| **SharedPreferences** | SettingsActivity.java saves settings |
| **TextInputLayout** | Add/Update course forms |
| **ProgressBar** | Loading indicator in forms |
| **LinearLayout** | Most form layouts |
| **FrameLayout** | Fragment container |
| **ConstraintLayout** | Complex layouts |
| **RelativeLayout** | Positioning elements |
