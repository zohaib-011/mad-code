# Bottom Navigation with Complete CRUD - Firebase Course Management

This README shows **3-tab bottom navigation** for complete CRUD operations: View, Add, Update.

---

## 📊 App Structure

```
┌─────────────────────────────────────────────────────────────────┐
│                       MAIN ACTIVITY                              │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │              FRAGMENT CONTAINER                           │  │
│  │                                                           │  │
│  │   ┌──────────┐    ┌──────────┐    ┌──────────┐           │  │
│  │   │  VIEW    │ OR │   ADD    │ OR │  UPDATE  │           │  │
│  │   │ Fragment │    │ Fragment │    │ Fragment │           │  │
│  │   └──────────┘    └──────────┘    └──────────┘           │  │
│  │                                                           │  │
│  └───────────────────────────────────────────────────────────┘  │
│                                                                  │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │  [📋 View]        [➕ Add]        [✏️ Update]             │  │
│  │     Tab 1          Tab 2           Tab 3                  │  │
│  └───────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🎯 What Each Tab Does

| Tab | Purpose | Operations |
|-----|---------|------------|
| **View** | Display all courses | READ, DELETE |
| **Add** | Create new course | CREATE |
| **Update** | Edit existing course | READ (dropdown), UPDATE |

---

## 🔄 Update Tab - Complete Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                    UPDATE TAB USER FLOW                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  STEP 1: User clicks "Update" tab                                │
│     ↓                                                            │
│  STEP 2: UpdateCourseFragment loads                              │
│     ↓                                                            │
│  STEP 3: Firebase reads ALL courses                              │
│     ↓                                                            │
│  STEP 4: Dropdown populated with course NAMES                    │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │ Select Course: [▼]                                         │ │
│  │                                                            │ │
│  │ Options:                                                   │ │
│  │  -- Select Course --                                       │ │
│  │  Mobile App Development                                    │ │
│  │  Artificial Intelligence                                   │ │
│  │  Database Systems                                          │ │
│  └────────────────────────────────────────────────────────────┘ │
│     ↓                                                            │
│  STEP 5: User selects "Mobile App Development"                   │
│     ↓                                                            │
│  STEP 6: OnItemSelectedListener triggered                        │
│     ↓                                                            │
│  STEP 7: Get full course object from courseList                  │
│     ↓                                                            │
│  STEP 8: Form AUTO-FILLS with course data                        │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │ Name:    [Mobile App Development]  ◄── Auto-filled        │ │
│  │ Code:    [CS401]                   ◄── Auto-filled        │ │
│  │ Credits: [3]                       ◄── Auto-filled        │ │
│  └────────────────────────────────────────────────────────────┘ │
│     ↓                                                            │
│  STEP 9: User modifies values (e.g., Credits: 3 → 4)            │
│     ↓                                                            │
│  STEP 10: User clicks "Update Course" button                     │
│     ↓                                                            │
│  STEP 11: Firebase UPDATE operation                              │
│     ↓                                                            │
│  STEP 12: Success Toast shows                                    │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📁 Required Files

```
com.example.coursemanager/
├── activities/
│   └── MainActivity.java           ← NEW: Bottom Navigation setup
│
├── fragments/
│   ├── ViewCoursesFragment.java    ← Tab 1: View all courses
│   ├── AddCourseFragment.java      ← Tab 2: Add form
│   └── UpdateCourseFragment.java   ← Tab 3: NEW! Dropdown + Update
│
├── utils/
│   └── FirebaseHelper.java         ← Add updateCourse() method
│
└── res/
    ├── layout/
    │   ├── activity_main.xml       ← Bottom nav + container
    │   ├── fragment_view_courses.xml
    │   ├── fragment_add_course.xml
    │   └── fragment_update_course.xml  ← NEW! With Spinner
    │
    └── menu/
        └── bottom_nav_menu.xml     ← NEW! 3 menu items
```

---

## 1️⃣ NEW: MainActivity.java (Bottom Navigation)

```java
package com.example.coursemanager.activities;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.Fragment;
import android.os.Bundle;
import android.view.MenuItem;
import com.example.coursemanager.R;
import com.example.coursemanager.fragments.AddCourseFragment;
import com.example.coursemanager.fragments.UpdateCourseFragment;
import com.example.coursemanager.fragments.ViewCoursesFragment;
import com.google.android.material.bottomnavigation.BottomNavigationView;

public class MainActivity extends AppCompatActivity {
    private BottomNavigationView bottomNavigationView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        bottomNavigationView = findViewById(R.id.bottom_navigation);

        // Load default fragment (View tab)
        loadFragment(new ViewCoursesFragment());

        // Bottom navigation click listener
        bottomNavigationView.setOnNavigationItemSelectedListener(
            new BottomNavigationView.OnNavigationItemSelectedListener() {
                @Override
                public boolean onNavigationItemSelected(@NonNull MenuItem item) {
                    Fragment fragment = null;
                    
                    int id = item.getItemId();
                    
                    // Decide which fragment to show based on tab clicked
                    if (id == R.id.nav_view) {
                        fragment = new ViewCoursesFragment();
                    } else if (id == R.id.nav_add) {
                        fragment = new AddCourseFragment();
                    } else if (id == R.id.nav_update) {
                        fragment = new UpdateCourseFragment();
                    }
                    
                    if (fragment != null) {
                        loadFragment(fragment);
                        return true;
                    }
                    return false;
                }
            }
        );
    }

    // Helper method to switch fragments
    private void loadFragment(Fragment fragment) {
        getSupportFragmentManager()
                .beginTransaction()
                .replace(R.id.fragment_container, fragment)
                .commit();
    }
}
```

**What this does:**
- Sets up 3-tab bottom navigation
- Loads ViewCoursesFragment by default
- Switches fragments when user taps tabs

---

## 2️⃣ NEW: UpdateCourseFragment.java (The Important One!)

```java
package com.example.coursemanager.fragments;

import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.Button;
import android.widget.ProgressBar;
import android.widget.Spinner;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.google.android.material.textfield.TextInputEditText;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.ValueEventListener;
import java.util.ArrayList;
import java.util.List;

public class UpdateCourseFragment extends Fragment {
    // UI Components
    private Spinner spinnerCourses;
    private TextInputEditText etCourseName, etCourseCode, etCreditHours;
    private Button btnUpdateCourse;
    private ProgressBar progressBar;
    
    // Data
    private FirebaseHelper firebaseHelper;
    private List<Course> courseList;        // Full course objects
    private List<String> courseNames;       // Just names for dropdown
    private Course selectedCourse;          // Currently selected course

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container,
                             @Nullable Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_update_course, container, false);

        // Initialize views
        spinnerCourses = view.findViewById(R.id.spinnerCourses);
        etCourseName = view.findViewById(R.id.etCourseName);
        etCourseCode = view.findViewById(R.id.etCourseCode);
        etCreditHours = view.findViewById(R.id.etCreditHours);
        btnUpdateCourse = view.findViewById(R.id.btnUpdateCourse);
        progressBar = view.findViewById(R.id.progressBar);

        firebaseHelper = new FirebaseHelper();
        courseList = new ArrayList<>();
        courseNames = new ArrayList<>();

        // Load courses into dropdown
        loadCoursesIntoSpinner();

        // When user selects course from dropdown
        spinnerCourses.setOnItemSelectedListener(new AdapterView.OnItemSelectedListener() {
            @Override
            public void onItemSelected(AdapterView<?> parent, View view, int position, long id) {
                // position 0 = "-- Select Course --" (hint)
                // position 1 = first course
                if (position > 0 && courseList.size() >= position) {
                    // Get selected course (subtract 1 because of hint at position 0)
                    selectedCourse = courseList.get(position - 1);
                    
                    // Auto-fill form with course data
                    fillFormWithCourseData(selectedCourse);
                }
            }

            @Override
            public void onNothingSelected(AdapterView<?> parent) {
                // Do nothing
            }
        });

        // Update button click
        btnUpdateCourse.setOnClickListener(v -> updateCourse());

        return view;
    }

    // ═══════════════════════════════════════════════════════════
    // STEP 1: Load all courses from Firebase into dropdown
    // ═══════════════════════════════════════════════════════════
    private void loadCoursesIntoSpinner() {
        firebaseHelper.getDatabaseReference().addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot snapshot) {
                courseList.clear();
                courseNames.clear();
                
                // Add hint as first item
                courseNames.add("-- Select Course --");

                // Loop through all courses in Firebase
                for (DataSnapshot dataSnapshot : snapshot.getChildren()) {
                    Course course = dataSnapshot.getValue(Course.class);
                    if (course != null) {
                        courseList.add(course);           // Store full course object
                        courseNames.add(course.getCourseName());  // Store just name for dropdown
                    }
                }

                // Create adapter for Spinner
                ArrayAdapter<String> adapter = new ArrayAdapter<>(
                        getContext(),
                        android.R.layout.simple_spinner_item,
                        courseNames
                );
                adapter.setDropDownViewResource(android.R.layout.simple_spinner_dropdown_item);
                
                // Set adapter to Spinner
                spinnerCourses.setAdapter(adapter);
            }

            @Override
            public void onCancelled(@NonNull DatabaseError error) {
                Toast.makeText(getContext(), "Failed to load courses", Toast.LENGTH_SHORT).show();
            }
        });
    }

    // ═══════════════════════════════════════════════════════════
    // STEP 2: Fill form fields when course is selected
    // ═══════════════════════════════════════════════════════════
    private void fillFormWithCourseData(Course course) {
        etCourseName.setText(course.getCourseName());
        etCourseCode.setText(course.getCourseCode());
        etCreditHours.setText(String.valueOf(course.getCreditHours()));
    }

    // ═══════════════════════════════════════════════════════════
    // STEP 3: Update course in Firebase
    // ═══════════════════════════════════════════════════════════
    private void updateCourse() {
        // Check if course is selected
        if (selectedCourse == null) {
            Toast.makeText(getContext(), "Please select a course first", Toast.LENGTH_SHORT).show();
            return;
        }

        // Get updated values from form
        String name = etCourseName.getText().toString().trim();
        String code = etCourseCode.getText().toString().trim();
        String creditsStr = etCreditHours.getText().toString().trim();

        // Validate
        if (name.isEmpty() || code.isEmpty() || creditsStr.isEmpty()) {
            Toast.makeText(getContext(), "Please fill all fields", Toast.LENGTH_SHORT).show();
            return;
        }

        int credits = Integer.parseInt(creditsStr);

        // Show loading
        progressBar.setVisibility(View.VISIBLE);
        btnUpdateCourse.setEnabled(false);

        // Update course object with new values
        selectedCourse.setCourseName(name);
        selectedCourse.setCourseCode(code);
        selectedCourse.setCreditHours(credits);

        // Update in Firebase
        firebaseHelper.updateCourse(selectedCourse,
            unused -> {
                // Success
                progressBar.setVisibility(View.GONE);
                btnUpdateCourse.setEnabled(true);
                Toast.makeText(getContext(), "Course updated successfully!", Toast.LENGTH_SHORT).show();
            },
            e -> {
                // Failure
                progressBar.setVisibility(View.GONE);
                btnUpdateCourse.setEnabled(true);
                Toast.makeText(getContext(), "Update failed: " + e.getMessage(), 
                        Toast.LENGTH_SHORT).show();
            }
        );
    }
}
```

**Key Features:**
1. **Spinner** - Dropdown populated with course names
2. **Two Lists** - `courseList` (full objects), `courseNames` (just names)
3. **OnItemSelectedListener** - Detects when user selects course
4. **Auto-fill** - `fillFormWithCourseData()` populates form
5. **Update** - Modifies `selectedCourse` and saves to Firebase

---

## 3️⃣ CHANGE: FirebaseHelper.java (Add UPDATE method)

**Add this method to your existing FirebaseHelper.java:**

```java
/**
 * UPDATE Operation
 * Updates an existing course in Firebase
 */
public void updateCourse(Course course, OnSuccessListener<Void> successListener, 
                        OnFailureListener failureListener) {
    // Update course at its ID location
    databaseReference.child(course.getId()).setValue(course)
            .addOnSuccessListener(successListener)
            .addOnFailureListener(failureListener);
}
```

---

## 4️⃣ NEW: Layout Files

### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- Fragment Container -->
    <FrameLayout
        android:id="@+id/fragment_container"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_above="@id/bottom_navigation" />

    <!-- Bottom Navigation -->
    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottom_navigation"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_alignParentBottom="true"
        android:background="?android:attr/windowBackground"
        app:menu="@menu/bottom_nav_menu" />

</RelativeLayout>
```

### menu/bottom_nav_menu.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    
    <item
        android:id="@+id/nav_view"
        android:icon="@android:drawable/ic_menu_view"
        android:title="View" />

    <item
        android:id="@+id/nav_add"
        android:icon="@android:drawable/ic_input_add"
        android:title="Add" />

    <item
        android:id="@+id/nav_update"
        android:icon="@android:drawable/ic_menu_edit"
        android:title="Update" />

</menu>
```

### fragment_update_course.xml (NEW!)
```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:fillViewport="true">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="24dp">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Update Course"
            android:textSize="24sp"
            android:textStyle="bold"
            android:layout_marginBottom="24dp" />

        <!-- Dropdown to select course -->
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Select Course:"
            android:textSize="16sp"
            android:layout_marginBottom="8dp" />

        <Spinner
            android:id="@+id/spinnerCourses"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:minHeight="48dp"
            android:padding="12dp"
            android:background="@android:drawable/edit_text"
            android:layout_marginBottom="24dp" />

        <!-- Course Name -->
        <com.google.android.material.textfield.TextInputLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Course Name">
            <com.google.android.material.textfield.TextInputEditText
                android:id="@+id/etCourseName"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />
        </com.google.android.material.textfield.TextInputLayout>

        <!-- Course Code -->
        <com.google.android.material.textfield.TextInputLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Course Code"
            android:layout_marginTop="16dp">
            <com.google.android.material.textfield.TextInputEditText
                android:id="@+id/etCourseCode"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />
        </com.google.android.material.textfield.TextInputLayout>

        <!-- Credit Hours -->
        <com.google.android.material.textfield.TextInputLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Credit Hours"
            android:layout_marginTop="16dp">
            <com.google.android.material.textfield.TextInputEditText
                android:id="@+id/etCreditHours"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:inputType="number" />
        </com.google.android.material.textfield.TextInputLayout>

        <!-- Loading Indicator -->
        <ProgressBar
            android:id="@+id/progressBar"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_gravity="center"
            android:layout_marginTop="16dp"
            android:visibility="gone" />

        <!-- Update Button -->
        <Button
            android:id="@+id/btnUpdateCourse"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="24dp"
            android:text="Update Course"
            android:padding="16dp" />

    </LinearLayout>
</ScrollView>
```

---

## 🎨 Visual: How Dropdown Works

```
BEFORE SELECTION:
┌────────────────────────────────────┐
│ Select Course: [▼]                 │
│                                    │
│ Dropdown shows:                    │
│  -- Select Course --    ← position 0
│  Mobile App Development ← position 1 (courseList[0])
│  Artificial Intelligence← position 2 (courseList[1])
│  Database Systems       ← position 3 (courseList[2])
│                                    │
│ Name:    [           ]  ← Empty    │
│ Code:    [           ]  ← Empty    │
│ Credits: [           ]  ← Empty    │
└────────────────────────────────────┘

AFTER SELECTING "Mobile App Development":
┌────────────────────────────────────┐
│ Select Course: [Mobile App Dev ▼]  │
│                                    │
│ OnItemSelectedListener triggered   │
│   position = 1                     │
│   selectedCourse = courseList[0]   │
│   fillFormWithCourseData()         │
│                                    │
│ Name:    [Mobile App Development]  │
│ Code:    [CS401]                   │
│ Credits: [3]                       │
│          ↑ AUTO-FILLED!            │
└────────────────────────────────────┘
```

---

## 🔍 Code Explanation: Why position - 1?

```java
onItemSelected(AdapterView<?> parent, View view, int position, long id) {
    if (position > 0 && courseList.size() >= position) {
        selectedCourse = courseList.get(position - 1);  // Why subtract 1?
    }
}
```

**Reason:**
```
Spinner (courseNames):          courseList:
Position 0: "-- Select Course --"   (no course)
Position 1: "Mobile App Dev"         courseList[0]
Position 2: "AI"                     courseList[1]
Position 3: "Database"               courseList[2]

When position = 1, we want courseList[0]
When position = 2, we want courseList[1]

Therefore: courseList[position - 1]
```

---

## ✅ Summary: What's NEW vs OLD

### NEW Files/Code:
1. ✅ **MainActivity.java** - Bottom navigation logic
2. ✅ **UpdateCourseFragment.java** - Dropdown + auto-fill + update
3. ✅ **FirebaseHelper.updateCourse()** - UPDATE method
4. ✅ **activity_main.xml** - Bottom nav layout
5. ✅ **bottom_nav_menu.xml** - 3 menu items
6. ✅ **fragment_update_course.xml** - Update form with Spinner

### UNCHANGED (Already Exist):
- ❌ ViewCoursesFragment.java (same as before)
- ❌ AddCourseFragment.java (same as before)
- ❌ CourseAdapter.java (same as before)
- ❌ Course.java (same as before)
- ❌ FirebaseHelper.addCourse() and deleteCourse() (already exist)

---

## 🎯 Key Concepts Used

| Concept | Where Used | What It Does |
|---------|------------|--------------|
| **BottomNavigationView** | MainActivity | 3-tab navigation |
| **Fragment switching** | MainActivity.loadFragment() | Change displayed fragment |
| **Spinner (Dropdown)** | UpdateCourseFragment | Select course |
| **ArrayAdapter** | Spinner | Populate dropdown with names |
| **OnItemSelectedListener** | Spinner | Detect selection |
| **Two Lists** | courseList + courseNames | Full objects + names only |
| **Auto-fill form** | fillFormWithCourseData() | Populate TextFields |
| **Firebase UPDATE** | updateCourse() | Save changes to database |
| **ValueEventListener** | Load courses | Real-time data sync |

---

## 🚀 How to Test

1. **View Tab**: Open app → Should show all courses
2. **Add Tab**: Click Add → Fill form → Click Add → Course added
3. **Update Tab**: 
   - Click Update
   - Dropdown should show course names
   - Select a course
   - Form should AUTO-FILL
   - Change values
   - Click Update
   - Go to View tab → Changes visible

Done! Complete CRUD with Bottom Navigation! 🎉
