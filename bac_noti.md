

1️⃣ activity_main.xml (Simple)

```<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <ProgressBar
        android:id="@+id/progressBar"
        style="?android:attr/progressBarStyleHorizontal"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:max="100"/>

    <Button
        android:id="@+id/btnStart"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Start"
        android:layout_marginTop="20dp"/>
</LinearLayout>
```

---

2️⃣ MainActivity.java (VERY SIMPLE)

```java
package com.example.simpleprogress;

import android.app.NotificationChannel;
import android.app.NotificationManager;
import android.os.Build;
import android.os.Bundle;
import android.os.Handler;
import android.widget.Button;
import android.widget.ProgressBar;

import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.NotificationCompat;

public class MainActivity extends AppCompatActivity {

    ProgressBar progressBar;
    int progress = 0;
    Handler handler = new Handler();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        progressBar = findViewById(R.id.progressBar);
        Button btnStart = findViewById(R.id.btnStart);

        btnStart.setOnClickListener(v -> {
            progress = 0;
            progressBar.setProgress(0);
            handler.postDelayed(runnable, 100);
        });
    }

    Runnable runnable = new Runnable() {
        @Override
        public void run() {
            if (progress < 100) {
                progress++;
                progressBar.setProgress(progress);
                handler.postDelayed(this, 100); // 10 seconds total
            } else {
                showNotification();
            }
        }
    };

    private void showNotification() {
        String channelId = "simple_channel";

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(
                    channelId,
                    "Simple Notification",
                    NotificationManager.IMPORTANCE_DEFAULT);
            getSystemService(NotificationManager.class)
                    .createNotificationChannel(channel);
        }

        NotificationCompat.Builder builder =
                new NotificationCompat.Builder(this, channelId)
                        .setSmallIcon(android.R.drawable.ic_dialog_info)
                        .setContentTitle("Done")
                        .setContentText("Progress completed!");

        NotificationManager manager =
                (NotificationManager) getSystemService(NOTIFICATION_SERVICE);

        manager.notify(1, builder.build());
    }
}
````

---

3️⃣ AndroidManifest.xml (Only if Android 13+)

<uses-permission android:name="android.permission.POST_NOTIFICATIONS"/>


---