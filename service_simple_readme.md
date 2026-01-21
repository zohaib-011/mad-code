# Service - Simple Guide

## 🎯 Purpose

**What is a Service?**
A Service is a component that runs in the background, even when you close the app.

**Why do we need it?**
- Some tasks need to continue even when app is closed
- Example: Playing music, downloading files, syncing data
- Thread stops when Activity closes, but Service continues!

**Simple Example:**
Music player app - you want music to play while using other apps.

```
❌ WITHOUT Service:
User plays music → Exits app → Music STOPS

✅ WITH Service:
User plays music → Exits app → Music CONTINUES
User can use WhatsApp, Chrome, etc. while music plays!
```

---

## 📊 Service vs Thread

| Aspect | Thread | Service |
|--------|--------|---------|
| **Runs when app closed?** | ❌ NO | ✅ YES |
| **Use for** | Short tasks (seconds) | Long tasks (minutes/hours) |
| **Example** | Countdown 10→0 | Music playback |
| **Stops when** | Activity destroyed | You stop it manually |

---

## 📁 Project Folder Structure

```
app/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── f257_a/
│       │               ├── MainActivity6.java       ← Control Activity (buttons)
│       │               └── MusicService.java        ← Unbound Service
│       │
│       ├── res/
│       │   └── layout/
│       │       └── activity_main6.xml              ← Layout with Play/Stop buttons
│       │
│       └── AndroidManifest.xml                     ← Declare activity & service
│
└── build.gradle                                     ← Dependencies
```

**Files you need to create:**
1. `MusicService.java` - Service that plays music
2. `MainActivity6.java` - Activity with Play/Stop buttons
3. `activity_main6.xml` - Layout with 2 buttons
4. Update `AndroidManifest.xml` - **MUST** declare service + activity

---

## 🎵 Two Types of Services

### 1. Unbound Service (Simple - Fire & Forget)
```
Start → Runs independently → Stop

Example: Start music, forget about it, stop later
```

### 2. Bound Service (Advanced - Control)
```
Bind → Get reference → Call methods → Unbind

Example: Start music, pause, change volume, stop
```

**We'll focus on UNBOUND Service (simpler!)**

---

## 🔄 Simple Flow

```
User clicks "Play Music" button
    ↓
Activity calls: startService(MusicService)
    ↓
MusicService starts playing music
    ↓
User closes app (exits Activity)
    ↓
Music STILL playing! (Service alive)
    ↓
User re-opens app
    ↓
User clicks "Stop Music" button
    ↓
Activity calls: stopService(MusicService)
    ↓
Music stops
```

---

## 💻 Complete Simple Example

### Purpose: Play background music that continues when app closes

**MusicService.java**

```java
package com.example.f257_a;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.IBinder;
import android.provider.Settings;
import android.widget.Toast;

/**
 * SIMPLE UNBOUND SERVICE
 * Plays music in background
 */
public class MusicService extends Service {
    MediaPlayer mp;

    @Override
    public void onCreate() {
        super.onCreate();
        Toast.makeText(this, "Music Service Created", Toast.LENGTH_SHORT).show();
    }

    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        // ═══════════════════════════════════════════════
        // CALLED WHEN: startService() is invoked
        // ═══════════════════════════════════════════════
        
        // Create MediaPlayer with system alarm sound
        mp = MediaPlayer.create(this, Settings.System.DEFAULT_ALARM_ALERT_URI);
        
        // Loop the music
        mp.setLooping(true);
        
        if(mp != null) {
            mp.start();  // Start playing
            Toast.makeText(this, "Music Started", Toast.LENGTH_SHORT).show();
        }
        
        // START_STICKY = Restart if system kills it
        return START_STICKY;
    }

    @Override
    public void onDestroy() {
        // ═══════════════════════════════════════════════
        // CALLED WHEN: stopService() is invoked
        // ═══════════════════════════════════════════════
        
        if(mp != null && mp.isPlaying()) {
            mp.stop();      // Stop music
            mp.release();   // Free memory
        }
        
        Toast.makeText(this, "Music Stopped", Toast.LENGTH_SHORT).show();
        super.onDestroy();
    }

    @Override
    public IBinder onBind(Intent intent) {
        // This is UNBOUND service, return null
        return null;
    }
}
```

**MainActivity6.java (Control Activity)**

```java
package com.example.f257_a;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

public class MainActivity6 extends AppCompatActivity {
    Button btnPlay, btnStop;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main6);

        btnPlay = findViewById(R.id.btnPlay);
        btnStop = findViewById(R.id.btnStop);

        // ═══════════════════════════════════════════════
        // START SERVICE (Play Music)
        // ═══════════════════════════════════════════════
        btnPlay.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent serviceIntent = new Intent(MainActivity6.this, MusicService.class);
                startService(serviceIntent);
            }
        });

        // ═══════════════════════════════════════════════
        // STOP SERVICE (Stop Music)
        // ═══════════════════════════════════════════════
        btnStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent serviceIntent = new Intent(MainActivity6.this, MusicService.class);
                stopService(serviceIntent);
            }
        });
    }
}
```

**activity_main6.xml**

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Music Service Demo"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="30dp" />

    <Button
        android:id="@+id/btnPlay"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Play Music (Start Service)"
        android:textSize="18sp"
        android:padding="16dp" />

    <Button
        android:id="@+id/btnStop"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Stop Music (Stop Service)"
        android:textSize="18sp"
        android:padding="16dp"
        android:layout_marginTop="16dp" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Try this:\n1. Click Play\n2. Press Home button\n3. Music still plays!\n4. Open app again\n5. Click Stop"
        android:textSize="16sp"
        android:layout_marginTop="40dp"
        android:gravity="center" />

</LinearLayout>
```

---

## 📝 Code Breakdown (Line by Line)

### Service Lifecycle Methods

#### 1. onCreate()
```java
@Override
public void onCreate() {
    super.onCreate();
    // Called ONCE when service is first created
}
```
**When:** First time service starts  
**Purpose:** Initialize resources

#### 2. onStartCommand()
```java
@Override
public int onStartCommand(Intent intent, int flags, int startId) {
    // Start your work here
    return START_STICKY;
}
```
**When:** Every time `startService()` is called  
**Purpose:** Do the actual work (play music, download, etc.)  
**Return values:**
- `START_STICKY` - Restart if killed
- `START_NOT_STICKY` - Don't restart

#### 3. onDestroy()
```java
@Override
public void onDestroy() {
    // Clean up resources
    super.onDestroy();
}
```
**When:** `stopService()` is called  
**Purpose:** Stop work and free memory

#### 4. onBind()
```java
@Override
public IBinder onBind(Intent intent) {
    return null;  // For unbound service
}
```
**Purpose:** Return null for simple unbound service

### Starting/Stopping Service

#### Start Service
```java
Intent serviceIntent = new Intent(this, MusicService.class);
startService(serviceIntent);
```
**What happens:**
1. Android creates service (if not exists)
2. Calls `onCreate()` (first time only)
3. Calls `onStartCommand()`
4. Service runs in background

#### Stop Service
```java
Intent serviceIntent = new Intent(this, MusicService.class);
stopService(serviceIntent);
```
**What happens:**
1. Calls `onDestroy()`
2. Service stops

---

## 🔧 AndroidManifest.xml (REQUIRED!)

**You MUST declare service in manifest:**

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.f257_a">

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/Theme.AppCompat">

        <!-- Your Activity -->
        <activity android:name=".MainActivity6" />

        <!-- ════════════════════════════════════════ -->
        <!-- DECLARE SERVICE HERE (IMPORTANT!)        -->
        <!-- ════════════════════════════════════════ -->
        <service
            android:name=".MusicService"
            android:enabled="true"
            android:exported="false" />

    </application>

</manifest>
```

**Attributes:**
- `android:name=".MusicService"` - Your service class
- `android:enabled="true"` - Service can run
- `android:exported="false"` - Only your app can use it

---

## 🎯 When to Use Service?

| Use Service When | Example |
|------------------|---------|
| Task continues when app closed | Music player |
| Long download | Download large file |
| Background sync | Sync with server |
| Periodic task | Upload logs every hour |

| DON'T Use Service For | Use Instead |
|----------------------|-------------|
| Short task (< 5 seconds) | Thread |
| UI update | Handler |
| One-time download | DownloadManager |

---

## ✅ Testing Steps

### 1. Setup
- Create MusicService.java
- Create MainActivity6.java
- Create activity_main6.xml
- Add service to AndroidManifest.xml

### 2. Test Service Runs
1. Open MainActivity6
2. Click "Play Music" button
3. **Listen:** Should hear alarm sound
4. **See Toast:** "Music Started"

### 3. Test Service Continues When App Closed
1. While music playing, press **Home button**
2. **Important:** Music should STILL play!
3. Open other apps (WhatsApp, Chrome)
4. **Music still playing?** ✅ Service works!

### 4. Test Stop Service
1. Re-open your app
2. Click "Stop Music" button
3. **Music stops?** ✅ Service destroyed!

---

## 🐛 Common Errors

### Error 1: "Service not declared in manifest"
**Error message:**
```
java.lang.IllegalArgumentException: Service Intent must be explicit
```

**Solution:**
Add to AndroidManifest.xml:
```xml
<service
    android:name=".MusicService"
    android:enabled="true"
    android:exported="false" />
```

---

### Error 2: Music doesn't play
**Possible reasons:**
1. Volume is muted → Turn up volume
2. MediaPlayer not created → Check if null
3. Not calling `mp.start()` → Add start() call

**Solution:**
```java
if(mp != null) {
    mp.start();  // Make sure this is called
}
```

---

### Error 3: Service stops when app closes
**Problem:** Using Thread instead of Service

**Solution:**
Use Service, not Thread:
```java
// ✅ CORRECT - Service continues
startService(new Intent(this, MusicService.class));

// ❌ WRONG - Thread stops when Activity destroyed
new Thread(() -> {
    // This stops when app closes
}).start();
```

---

### Error 4: Music won't stop
**Problem:** Not calling `mp.stop()` in onDestroy()

**Solution:**
```java
@Override
public void onDestroy() {
    if(mp != null && mp.isPlaying()) {
        mp.stop();      // Add this
        mp.release();   // Add this
    }
    super.onDestroy();
}
```

---

### Error 5: "Service already running" or onCreate() not called again
**This is NORMAL!**

When you call `startService()` multiple times:
- **First call:** `onCreate()` → `onStartCommand()`
- **Second call:** `onStartCommand()` only (no onCreate)
- **Third call:** `onStartCommand()` only

This is expected behavior!

---

## 🔄 Service Lifecycle Diagram

```
┌─────────────────────────────────────────────────┐
│               SERVICE LIFECYCLE                 │
├─────────────────────────────────────────────────┤
│                                                 │
│  startService() called                          │
│      ↓                                          │
│  onCreate() [ONCE - First time only]            │
│      ↓                                          │
│  onStartCommand() [EVERY TIME]                  │
│      ↓                                          │
│  [SERVICE RUNNING]                              │
│      │                                          │
│      │  App closed → Service STILL runs         │
│      │  Phone locked → Service STILL runs       │
│      │                                          │
│      ↓                                          │
│  stopService() called                           │
│      ↓                                          │
│  onDestroy()                                    │
│      ↓                                          │
│  [SERVICE STOPPED]                              │
│                                                 │
└─────────────────────────────────────────────────┘
```

---

## 📚 Summary

**Service = Background component**
- Runs independently of Activity
- Continues when app is closed
- Must be declared in AndroidManifest.xml

**Unbound Service:**
- Simple start/stop pattern
- Fire and forget
- No communication back to Activity

**Pattern:**
```java
// In Activity
Intent intent = new Intent(this, MusicService.class);
startService(intent);  // Start
stopService(intent);   // Stop

// In Service
public int onStartCommand(...) {
    // Do your work
    return START_STICKY;
}
```

**Simple purpose:** Run tasks in background, even when app is closed! 🎉

---

## 🎓 Next Steps

**Want more control over your service?**
→ Learn **Bound Service** (can pause, resume, change volume)

**Need periodic tasks?**
→ Use **Handler + Runnable** inside Service

**Want to keep service alive?**
→ Use **Foreground Service** (shows notification)

But for simple background music, this Unbound Service is perfect! ✅
