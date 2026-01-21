# Bound Service - From final_code.txt

## 🎯 Purpose
Control background music with direct method calls (play, pause, stop). Two-way communication between Activity and Service.

---

## 📁 Folder Structure

```
app/src/main/java/com/example/f257_a/
    └── MybindService.java          ← Bound Service

app/src/main/res/layout/
    └── activity_main6.xml          ← Layout with buttons

AndroidManifest.xml                  ← Declare service
```

---

## 💻 Complete Code

### MybindService.java

```java
package com.example.f257_a;

import android.app.Service;
import android.content.Intent;
import android.media.MediaPlayer;
import android.os.Binder;
import android.os.IBinder;
import android.provider.Settings;

public class MybindService extends Service {
    MediaPlayer mp;
    private final IBinder binder = (IBinder) new LocalBinder();
    
    public class LocalBinder extends Binder {
        public MybindService getservices() {
            return MybindService.this;
        }
    }
    
    @Override
    public void onCreate() {
        super.onCreate();
        mp = MediaPlayer.create(this, Settings.System.DEFAULT_RINGTONE_URI);
        mp.setLooping(true);
    }
    
    public void startMusic() {
        if (!mp.isPlaying()) {
            mp.start();
        }
    }
    
    public void stopMusic() {
        if (mp.isPlaying()) {
            mp.stop();
            mp.prepareAsync();
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
        return binder;
    }
}
```

### MainActivity6.java (Bound buttons only)

```java
package com.example.f257_a;

import androidx.appcompat.app.AppCompatActivity;
import android.content.ComponentName;
import android.content.Intent;
import android.content.ServiceConnection;
import android.os.Bundle;
import android.os.IBinder;
import android.view.View;
import android.widget.Button;

public class MainActivity6 extends AppCompatActivity {
    Button btn3, btn4;
    MybindService MBS;
    Boolean isbound;
    
    ServiceConnection connection = new ServiceConnection() {
        @Override
        public void onServiceConnected(ComponentName componentName, IBinder iBinder) {
            MybindService.LocalBinder binder = (MybindService.LocalBinder) iBinder;
            MBS = binder.getservices();
            isbound = true;
        }
        
        @Override
        public void onServiceDisconnected(ComponentName componentName) {
            isbound = false;
        }
    };
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main6);
        
        btn3 = findViewById(R.id.boundPlay);
        btn4 = findViewById(R.id.boundStop);
        
        // Bind to service
        bindService(new Intent(MainActivity6.this, MybindService.class), 
                   connection, BIND_AUTO_CREATE);
        
        btn3.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if(isbound) {
                    MBS.startMusic();
                }
            }
        });
        
        btn4.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if(isbound) {
                    MBS.stopMusic();
                }
            }
        });
    }
}
```

### AndroidManifest.xml

```xml
<service
    android:name=".MybindService"
    android:enabled="true"
    android:exported="false" />
```

---

## ✅ How It Works

```
onCreate() → bindService() → ServiceConnection.onServiceConnected()
→ Get service reference (MBS) → isbound = true
→ Click "Play" → MBS.startMusic() (direct method call)
→ Click "Stop" → MBS.stopMusic() (direct method call)
→ onDestroy() → unbindService()
```

**Key Difference:** Direct method calls instead of just start/stop!
