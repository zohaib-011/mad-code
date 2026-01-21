# Unbound Service - From final_code.txt

## 🎯 Purpose
Play background music independently. Start it, music plays. Stop it, music stops. Service runs even when app is closed.

---

## 📁 Folder Structure

```
app/src/main/java/com/example/f257_a/
    └── MusicService.java           ← Unbound Service

app/src/main/res/layout/
    └── activity_main6.xml          ← Layout with buttons

AndroidManifest.xml                  ← Declare service
```

---

## 💻 Complete Code

### MusicService.java

```java
package com.example.f257_a;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.IBinder;
import android.provider.Settings;

public class MusicService extends Service {
    MediaPlayer mp;
    
    public MusicService() {
    }
    
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) {
        mp = MediaPlayer.create(this, Settings.System.DEFAULT_ALARM_ALERT_URI);
        mp.setLooping(true);
        if(mp != null) {
        }
        mp.start();
        return super.onStartCommand(intent, flags, startId);
    }
    
    @Override
    public void onDestroy() {
        if(mp.isPlaying()) {
            mp.stop();
            mp.release();
        }
        super.onDestroy();
    }
    
    @Override
    public IBinder onBind(Intent intent) {
        throw new UnsupportedOperationException("Not yet implemented");
    }
}
```

### MainActivity6.java (Unbound buttons only)

```java
Button btn1, btn2;

btn1.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        startService(new Intent(MainActivity6.this, MusicService.class));
    }
});

btn2.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        stopService(new Intent(MainActivity6.this, MusicService.class));
    }
});
```

### AndroidManifest.xml

```xml
<service
    android:name=".MusicService"
    android:enabled="true"
    android:exported="false" />
```

---

## ✅ How It Works

```
User clicks "Play" → startService() → MusicService.onStartCommand()
→ Music plays → User closes app → Music STILL plays
→ User reopens → Clicks "Stop" → stopService() → onDestroy() → Music stops
```
