# Firebase Course Management - Complete Guide

This README covers **Firebase CRUD operations** with RecyclerView to Add, View, and Delete courses.

---

## 📋 What This Guide Covers

| Feature | What It Does | Concepts Used |
|---------|--------------|---------------|
| **Add Course** | User fills form → Data saves to Firebase | Firebase CREATE, TextInputLayout |
| **View Courses** | All courses display in card list | Firebase READ, RecyclerView, CardView |
| **Delete Course** | User clicks delete → Course removed | Firebase DELETE, Notification |

---

## 🔄 User Flow Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                        COURSE MANAGEMENT FLOW                           │
└─────────────────────────────────────────────────────────────────────────┘

    ┌──────────────┐                              
    │  App Opens   │                              
    └──────┬───────┘                              
           │                                       
           ▼                                       
    ┌──────────────────────────────────────────┐  
    │         COURSES FRAGMENT                  │  
    │  ┌────────────────────────────────────┐  │  
    │  │  Course Card 1  [Update] [Delete]  │  │  
    │  │  Course Card 2  [Update] [Delete]  │  │  
    │  │  Course Card 3  [Update] [Delete]  │  │  
    │  └────────────────────────────────────┘  │  
    │                                    [+]   │ ← Floating Action Button
    └─────────────────┬────────────────────────┘  
                      │                            
         ┌────────────┼────────────┐              
         │            │            │              
         ▼            ▼            ▼              
    ┌─────────┐  ┌─────────┐  ┌─────────┐        
    │  ADD    │  │ UPDATE  │  │ DELETE  │        
    │ COURSE  │  │ COURSE  │  │ COURSE  │        
    └────┬────┘  └────┬────┘  └────┬────┘        
         │            │            │              
         ▼            ▼            ▼              
    ┌─────────────────────────────────────────┐  
    │           FIREBASE DATABASE              │  
    │  ┌─────────────────────────────────┐    │  
    │  │  Courses/                        │    │  
    │  │    ├── -ABC123/                  │    │  
    │  │    │     ├── courseName: "MAD"   │    │  
    │  │    │     ├── courseCode: "CS401" │    │  
    │  │    │     └── creditHours: 3      │    │  
    │  │    └── -XYZ789/                  │    │  
    │  │          └── ...                 │    │  
    │  └─────────────────────────────────┘    │  
    └─────────────────────────────────────────┘  
```

---

## 📁 Required Files

```
com.example.coursemanager/
│
├── models/
│   └── Course.java              ← Data model
│
├── utils/
│   └── FirebaseHelper.java      ← CRUD operations
│
├── adapters/
│   └── CourseAdapter.java       ← RecyclerView adapter
│
├── fragments/
│   └── CoursesFragment.java     ← Display courses list
│
├── activities/
│   └── AddCourseActivity.java   ← Add course form
│
└── res/layout/
    ├── fragment_courses.xml     ← RecyclerView + FAB
    ├── activity_add_course.xml  ← Form layout
    └── item_course_card.xml     ← Single course card
```

---

## 1️⃣ Model Class - Course.java

**Purpose:** Container to hold course data. Firebase needs this structure to save/read data.

```java
package com.example.coursemanager.models;

public class Course {
    private String id;           // Unique Firebase key
    private String courseName;   // Example: "Mobile App Development"
    private String courseCode;   // Example: "CS401"
    private int creditHours;     // Example: 3

    // Empty constructor - REQUIRED for Firebase
    public Course() {
    }

    // Constructor with all fields
    public Course(String id, String courseName, String courseCode, int creditHours) {
        this.id = id;
        this.courseName = courseName;
        this.courseCode = courseCode;
        this.creditHours = creditHours;
    }

    // Getters
    public String getId() { return id; }
    public String getCourseName() { return courseName; }
    public String getCourseCode() { return courseCode; }
    public int getCreditHours() { return creditHours; }

    // Setters
    public void setId(String id) { this.id = id; }
    public void setCourseName(String courseName) { this.courseName = courseName; }
    public void setCourseCode(String courseCode) { this.courseCode = courseCode; }
    public void setCreditHours(int creditHours) { this.creditHours = creditHours; }
}
```

**What each field does:**
- `id` → Firebase generates unique key like "-NxYz123abc"
- `courseName` → Name user enters in form
- `courseCode` → Code user enters in form  
- `creditHours` → Number user enters in form

---

## 2️⃣ Firebase Helper - FirebaseHelper.java

**Purpose:** Handles all database operations (Create, Read, Update, Delete).

```java
package com.example.coursemanager.utils;

import com.example.coursemanager.models.Course;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;

public class FirebaseHelper {
    private DatabaseReference databaseReference;

    public FirebaseHelper() {
        // Connect to "Courses" node in Firebase
        databaseReference = FirebaseDatabase.getInstance().getReference("Courses");
    }

    // ═══════════════════════════════════════════════════════════
    // CREATE - Add new course to database
    // ═══════════════════════════════════════════════════════════
    public void addCourse(Course course, OnSuccessListener<Void> successListener, 
                         OnFailureListener failureListener) {
        // Generate unique key for this course
        String key = databaseReference.push().getKey();
        if (key != null) {
            course.setId(key);
            // Save course to Firebase
            databaseReference.child(key).setValue(course)
                    .addOnSuccessListener(successListener)
                    .addOnFailureListener(failureListener);
        }
    }

    // ═══════════════════════════════════════════════════════════
    // DELETE - Remove course from database
    // ═══════════════════════════════════════════════════════════
    public void deleteCourse(String courseId, OnSuccessListener<Void> successListener, 
                            OnFailureListener failureListener) {
        databaseReference.child(courseId).removeValue()
                .addOnSuccessListener(successListener)
                .addOnFailureListener(failureListener);
    }

    // ═══════════════════════════════════════════════════════════
    // Get database reference for READ operations
    // ═══════════════════════════════════════════════════════════
    public DatabaseReference getDatabaseReference() {
        return databaseReference;
    }
}
```

**How it works:**
```
┌─────────────────────────────────────────────────────────────┐
│                    FIREBASE OPERATIONS                       │
├─────────────────────────────────────────────────────────────┤
│                                                              │
│  CREATE (addCourse):                                         │
│  ┌─────────────┐    ┌──────────────┐    ┌────────────────┐  │
│  │ Course      │ →  │ push().      │ →  │ setValue()     │  │
│  │ Object      │    │ getKey()     │    │ saves to       │  │
│  │             │    │ generates ID │    │ Firebase       │  │
│  └─────────────┘    └──────────────┘    └────────────────┘  │
│                                                              │
│  DELETE (deleteCourse):                                      │
│  ┌─────────────┐    ┌──────────────────────────────────┐    │
│  │ Course ID   │ →  │ child(id).removeValue()          │    │
│  │ "-ABC123"   │    │ removes from Firebase            │    │
│  └─────────────┘    └──────────────────────────────────┘    │
│                                                              │
│  READ (getDatabaseReference):                                │
│  ┌─────────────────────────────────────────────────────┐    │
│  │ Returns reference for ValueEventListener            │    │
│  │ Used in CoursesFragment to listen for changes       │    │
│  └─────────────────────────────────────────────────────┘    │
│                                                              │
└─────────────────────────────────────────────────────────────┘
```

---

## 3️⃣ Adapter Class - CourseAdapter.java

**Purpose:** Takes list of courses and creates card view for each one in RecyclerView.

```java
package com.example.coursemanager.adapters;

import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;
import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import java.util.List;

public class CourseAdapter extends RecyclerView.Adapter<CourseAdapter.CourseViewHolder> {
    private List<Course> courseList;
    private Context context;
    private FirebaseHelper firebaseHelper;

    // Constructor - receives list and context
    public CourseAdapter(List<Course> courseList, Context context) {
        this.courseList = courseList;
        this.context = context;
        this.firebaseHelper = new FirebaseHelper();
    }

    // ═══════════════════════════════════════════════════════════
    // Creates new card view for each course
    // ═══════════════════════════════════════════════════════════
    @NonNull
    @Override
    public CourseViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(context)
                .inflate(R.layout.item_course_card, parent, false);
        return new CourseViewHolder(view);
    }

    // ═══════════════════════════════════════════════════════════
    // Fills card with course data
    // ═══════════════════════════════════════════════════════════
    @Override
    public void onBindViewHolder(@NonNull CourseViewHolder holder, int position) {
        Course course = courseList.get(position);

        // Set text on card
        holder.txtCourseName.setText(course.getCourseName());
        holder.txtCourseCode.setText("Code: " + course.getCourseCode());
        holder.txtCreditHours.setText("Credits: " + course.getCreditHours());

        // Delete button click
        holder.btnDelete.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                int currentPosition = holder.getAdapterPosition();
                
                firebaseHelper.deleteCourse(
                    course.getId(),
                    unused -> {
                        // Success - remove from list and update UI
                        courseList.remove(currentPosition);
                        notifyItemRemoved(currentPosition);
                        Toast.makeText(context, "Course deleted!", Toast.LENGTH_SHORT).show();
                    },
                    e -> {
                        // Failed
                        Toast.makeText(context, "Delete failed: " + e.getMessage(), 
                                Toast.LENGTH_SHORT).show();
                    }
                );
            }
        });
    }

    // Returns total number of courses
    @Override
    public int getItemCount() {
        return courseList.size();
    }

    // ═══════════════════════════════════════════════════════════
    // ViewHolder - holds references to card views
    // ═══════════════════════════════════════════════════════════
    public static class CourseViewHolder extends RecyclerView.ViewHolder {
        TextView txtCourseName, txtCourseCode, txtCreditHours;
        Button btnDelete;

        public CourseViewHolder(@NonNull View itemView) {
            super(itemView);
            txtCourseName = itemView.findViewById(R.id.txtCourseName);
            txtCourseCode = itemView.findViewById(R.id.txtCourseCode);
            txtCreditHours = itemView.findViewById(R.id.txtCreditHours);
            btnDelete = itemView.findViewById(R.id.btnDelete);
        }
    }
}
```

**How RecyclerView Adapter works:**
```
┌─────────────────────────────────────────────────────────────────┐
│                    RECYCLERVIEW ADAPTER FLOW                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Step 1: onCreateViewHolder()                                    │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Inflates item_course_card.xml → Creates empty card view │   │
│  │  Returns ViewHolder with references to TextViews/Buttons │   │
│  └──────────────────────────────────────────────────────────┘   │
│                         │                                        │
│                         ▼                                        │
│  Step 2: onBindViewHolder()                                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Gets Course from list at position                        │   │
│  │  Sets: txtCourseName = "Mobile App Development"          │   │
│  │  Sets: txtCourseCode = "Code: CS401"                     │   │
│  │  Sets: txtCreditHours = "Credits: 3"                     │   │
│  │  Sets: Delete button click listener                       │   │
│  └──────────────────────────────────────────────────────────┘   │
│                         │                                        │
│                         ▼                                        │
│  Step 3: getItemCount()                                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  Returns courseList.size() → Tells RecyclerView how      │   │
│  │  many cards to create                                     │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4️⃣ Fragment Class - CoursesFragment.java

**Purpose:** Main screen showing all courses. Listens to Firebase for real-time updates.

```java
package com.example.coursemanager.fragments;

import android.content.Intent;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import androidx.annotation.NonNull;
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

public class CoursesFragment extends Fragment {
    private RecyclerView recyclerView;
    private CourseAdapter courseAdapter;
    private List<Course> courseList;
    private FirebaseHelper firebaseHelper;
    private FloatingActionButton fabAddCourse;

    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_courses, container, false);

        // Initialize
        recyclerView = view.findViewById(R.id.recyclerViewCourses);
        fabAddCourse = view.findViewById(R.id.fabAddCourse);
        courseList = new ArrayList<>();
        firebaseHelper = new FirebaseHelper();

        // Setup RecyclerView
        recyclerView.setLayoutManager(new LinearLayoutManager(getContext()));
        courseAdapter = new CourseAdapter(courseList, getContext());
        recyclerView.setAdapter(courseAdapter);

        // FAB click → Open Add Course screen
        fabAddCourse.setOnClickListener(v -> {
            Intent intent = new Intent(getContext(), AddCourseActivity.class);
            startActivity(intent);
        });

        // Load courses from Firebase
        loadCourses();

        return view;
    }

    // ═══════════════════════════════════════════════════════════
    // READ - Listen to Firebase for course data
    // ═══════════════════════════════════════════════════════════
    private void loadCourses() {
        firebaseHelper.getDatabaseReference().addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot snapshot) {
                courseList.clear();
                
                // Loop through all courses in Firebase
                for (DataSnapshot dataSnapshot : snapshot.getChildren()) {
                    Course course = dataSnapshot.getValue(Course.class);
                    if (course != null) {
                        courseList.add(course);
                    }
                }
                
                // Update RecyclerView
                courseAdapter.notifyDataSetChanged();
            }

            @Override
            public void onCancelled(@NonNull DatabaseError error) {
                // Handle error
            }
        });
    }
}
```

**How ValueEventListener works:**
```
┌─────────────────────────────────────────────────────────────────┐
│                 FIREBASE REAL-TIME LISTENING                     │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  addValueEventListener() - Listens CONTINUOUSLY                  │
│                                                                  │
│  ┌──────────────┐         ┌──────────────┐                      │
│  │   FIREBASE   │ ──────► │   APP        │                      │
│  │   DATABASE   │ changes │   LISTENER   │                      │
│  └──────────────┘         └──────┬───────┘                      │
│                                  │                               │
│                                  ▼                               │
│  When data changes (add/delete/update):                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │  onDataChange() is called automatically                   │   │
│  │                                                           │   │
│  │  1. courseList.clear() - Empty old list                   │   │
│  │  2. for loop - Read each course from snapshot             │   │
│  │  3. courseList.add() - Add to list                        │   │
│  │  4. notifyDataSetChanged() - Refresh RecyclerView         │   │
│  └──────────────────────────────────────────────────────────┘   │
│                                                                  │
│  Result: Screen updates AUTOMATICALLY when data changes!        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 5️⃣ Activity Class - AddCourseActivity.java

**Purpose:** Form screen where user enters course details and saves to Firebase.

```java
package com.example.coursemanager.activities;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;
import com.example.coursemanager.R;
import com.example.coursemanager.models.Course;
import com.example.coursemanager.utils.FirebaseHelper;
import com.google.android.material.textfield.TextInputEditText;

public class AddCourseActivity extends AppCompatActivity {
    private TextInputEditText etCourseName, etCourseCode, etCreditHours;
    private Button btnAddCourse;
    private ProgressBar progressBar;
    private FirebaseHelper firebaseHelper;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_add_course);

        // Initialize views
        etCourseName = findViewById(R.id.etCourseName);
        etCourseCode = findViewById(R.id.etCourseCode);
        etCreditHours = findViewById(R.id.etCreditHours);
        btnAddCourse = findViewById(R.id.btnAddCourse);
        progressBar = findViewById(R.id.progressBar);
        
        firebaseHelper = new FirebaseHelper();

        // Add button click
        btnAddCourse.setOnClickListener(v -> addCourse());
    }

    private void addCourse() {
        // Get user input
        String name = etCourseName.getText().toString().trim();
        String code = etCourseCode.getText().toString().trim();
        String creditsStr = etCreditHours.getText().toString().trim();

        // Validate input
        if (name.isEmpty() || code.isEmpty() || creditsStr.isEmpty()) {
            Toast.makeText(this, "Please fill all fields", Toast.LENGTH_SHORT).show();
            return;
        }

        int credits = Integer.parseInt(creditsStr);

        // Show loading
        progressBar.setVisibility(View.VISIBLE);
        btnAddCourse.setEnabled(false);

        // Create course object
        Course course = new Course(null, name, code, credits);

        // Save to Firebase
        firebaseHelper.addCourse(course,
            unused -> {
                // Success
                progressBar.setVisibility(View.GONE);
                Toast.makeText(this, "Course added successfully!", Toast.LENGTH_SHORT).show();
                finish(); // Go back to previous screen
            },
            e -> {
                // Failed
                progressBar.setVisibility(View.GONE);
                btnAddCourse.setEnabled(true);
                Toast.makeText(this, "Failed: " + e.getMessage(), Toast.LENGTH_SHORT).show();
            }
        );
    }
}
```

---

## 6️⃣ Layout Files

### fragment_courses.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp">

    <!-- List of courses -->
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerViewCourses"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

    <!-- Floating button to add course -->
    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fabAddCourse"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_alignParentEnd="true"
        android:layout_alignParentBottom="true"
        android:layout_margin="16dp"
        android:src="@android:drawable/ic_input_add" />

</RelativeLayout>
```

### activity_add_course.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="24dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Add New Course"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="24dp" />

    <!-- Course Name Input -->
    <com.google.android.material.textfield.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Course Name">

        <com.google.android.material.textfield.TextInputEditText
            android:id="@+id/etCourseName"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" />
    </com.google.android.material.textfield.TextInputLayout>

    <!-- Course Code Input -->
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

    <!-- Credit Hours Input -->
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

    <!-- Loading indicator -->
    <ProgressBar
        android:id="@+id/progressBar"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_marginTop="16dp"
        android:visibility="gone" />

    <!-- Add Button -->
    <Button
        android:id="@+id/btnAddCourse"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="24dp"
        android:text="Add Course"
        android:padding="16dp" />

</LinearLayout>
```

### item_course_card.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.cardview.widget.CardView 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/cardView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_margin="8dp"
    app:cardCornerRadius="12dp"
    app:cardElevation="4dp">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="16dp">

        <!-- Course Name -->
        <TextView
            android:id="@+id/txtCourseName"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Course Name"
            android:textSize="18sp"
            android:textStyle="bold" />

        <!-- Course Code -->
        <TextView
            android:id="@+id/txtCourseCode"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Code: CS101"
            android:layout_marginTop="4dp" />

        <!-- Credit Hours -->
        <TextView
            android:id="@+id/txtCreditHours"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Credits: 3"
            android:layout_marginTop="4dp" />

        <!-- Delete Button -->
        <Button
            android:id="@+id/btnDelete"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:text="Delete"
            android:backgroundTint="#F44336" />

    </LinearLayout>
</androidx.cardview.widget.CardView>
```

---

## 🔄 Complete User Action Flow

### Action 1: View All Courses
```
┌─────────────────────────────────────────────────────────────────┐
│                    VIEW COURSES FLOW                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Step 1: User opens app                                          │
│     │                                                            │
│     ▼                                                            │
│  Step 2: CoursesFragment loads                                   │
│     │    - onCreateView() runs                                   │
│     │    - RecyclerView setup                                    │
│     │    - loadCourses() called                                  │
│     │                                                            │
│     ▼                                                            │
│  Step 3: ValueEventListener connects to Firebase                 │
│     │    - addValueEventListener()                               │
│     │                                                            │
│     ▼                                                            │
│  Step 4: onDataChange() receives data                            │
│     │    - Loops through all courses                             │
│     │    - Adds each to courseList                               │
│     │                                                            │
│     ▼                                                            │
│  Step 5: notifyDataSetChanged() updates screen                   │
│     │    - RecyclerView creates cards                            │
│     │                                                            │
│     ▼                                                            │
│  Step 6: User sees all courses in card format                    │
│                                                                  │
│  CONCEPTS: Fragment, RecyclerView, Adapter, Firebase READ,       │
│            ValueEventListener, CardView                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Action 2: Add New Course
```
┌─────────────────────────────────────────────────────────────────┐
│                    ADD COURSE FLOW                               │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Step 1: User clicks [+] FAB button                              │
│     │    - fabAddCourse.setOnClickListener()                     │
│     │                                                            │
│     ▼                                                            │
│  Step 2: Intent opens AddCourseActivity                          │
│     │    - startActivity(intent)                                 │
│     │                                                            │
│     ▼                                                            │
│  Step 3: User sees form with 3 fields                            │
│     │    - Course Name (TextInputEditText)                       │
│     │    - Course Code (TextInputEditText)                       │
│     │    - Credit Hours (TextInputEditText, number)              │
│     │                                                            │
│     ▼                                                            │
│  Step 4: User fills form and clicks "Add Course"                 │
│     │    - btnAddCourse.setOnClickListener()                     │
│     │                                                            │
│     ▼                                                            │
│  Step 5: Validation checks                                       │
│     │    - If empty → Show error Toast                           │
│     │    - If valid → Continue                                   │
│     │                                                            │
│     ▼                                                            │
│  Step 6: ProgressBar shows loading                               │
│     │    - progressBar.setVisibility(VISIBLE)                    │
│     │                                                            │
│     ▼                                                            │
│  Step 7: Course object created                                   │
│     │    - new Course(null, name, code, credits)                 │
│     │                                                            │
│     ▼                                                            │
│  Step 8: FirebaseHelper.addCourse() called                       │
│     │    - push().getKey() generates ID                          │
│     │    - setValue() saves to Firebase                          │
│     │                                                            │
│     ▼                                                            │
│  Step 9: Success callback                                        │
│     │    - Hide ProgressBar                                      │
│     │    - Show success Toast                                    │
│     │    - finish() returns to previous screen                   │
│     │                                                            │
│     ▼                                                            │
│  Step 10: CoursesFragment auto-updates                           │
│           - ValueEventListener detects new data                  │
│           - New course appears in list                           │
│                                                                  │
│  CONCEPTS: Intent, TextInputLayout, Firebase CREATE,             │
│            ProgressBar, Toast, finish()                          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Action 3: Delete Course
```
┌─────────────────────────────────────────────────────────────────┐
│                    DELETE COURSE FLOW                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  Step 1: User sees course card with Delete button                │
│     │                                                            │
│     ▼                                                            │
│  Step 2: User clicks "Delete" button                             │
│     │    - btnDelete.setOnClickListener() in adapter             │
│     │                                                            │
│     ▼                                                            │
│  Step 3: Get course ID from clicked item                         │
│     │    - course.getId()                                        │
│     │                                                            │
│     ▼                                                            │
│  Step 4: FirebaseHelper.deleteCourse() called                    │
│     │    - child(courseId).removeValue()                         │
│     │                                                            │
│     ▼                                                            │
│  Step 5: Firebase removes data                                   │
│     │    - Data deleted from cloud                               │
│     │                                                            │
│     ▼                                                            │
│  Step 6: Success callback                                        │
│     │    - courseList.remove(position)                           │
│     │    - notifyItemRemoved(position)                           │
│     │    - Show Toast "Course deleted!"                          │
│     │                                                            │
│     ▼                                                            │
│  Step 7: Card disappears from screen                             │
│           - RecyclerView animates removal                        │
│                                                                  │
│  CONCEPTS: Firebase DELETE, RecyclerView animation,              │
│            notifyItemRemoved(), Toast                            │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📦 Required Dependencies (build.gradle)

```gradle
dependencies {
    // Firebase
    implementation platform('com.google.firebase:firebase-bom:32.7.0')
    implementation 'com.google.firebase:firebase-database'
    
    // RecyclerView
    implementation 'androidx.recyclerview:recyclerview:1.3.2'
    
    // CardView
    implementation 'androidx.cardview:cardview:1.0.0'
    
    // Material Design (for TextInputLayout, FAB)
    implementation 'com.google.android.material:material:1.11.0'
}
```

---

## ✅ Concepts Covered Summary

| Concept | Where Used | What It Does |
|---------|------------|--------------|
| **Model Class** | Course.java | Holds course data structure |
| **Firebase CREATE** | FirebaseHelper.addCourse() | Saves new course |
| **Firebase READ** | CoursesFragment.loadCourses() | Gets all courses |
| **Firebase DELETE** | FirebaseHelper.deleteCourse() | Removes course |
| **ValueEventListener** | CoursesFragment | Real-time data sync |
| **RecyclerView** | CoursesFragment | Displays scrollable list |
| **RecyclerView.Adapter** | CourseAdapter | Binds data to cards |
| **ViewHolder** | CourseViewHolder | Holds card view references |
| **CardView** | item_course_card.xml | Material card UI |
| **FloatingActionButton** | fragment_courses.xml | Add button |
| **TextInputLayout** | activity_add_course.xml | Material input fields |
| **ProgressBar** | AddCourseActivity | Loading indicator |
| **Intent** | CoursesFragment | Navigate to add screen |
| **Fragment** | CoursesFragment | Reusable UI component |
| **LinearLayout** | Layouts | Vertical arrangement |
| **RelativeLayout** | fragment_courses.xml | FAB positioning |
