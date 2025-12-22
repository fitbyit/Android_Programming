Below is a **simple Android (Java) example** that fulfills the requirement:

✔ Screen with **Start** and **Stop** buttons
✔ A **Timer** that counts seconds
✔ **Start** → timer starts
✔ **Stop** → timer stops
✔ Time displayed in **seconds**

---

## 📁 Files Used

* `activity_main.xml`
* `MainActivity.java`

---

## 1️⃣ Layout File — `activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="20dp">

    <TextView
        android:id="@+id/tvTimer"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="0 seconds"
        android:textSize="24sp"
        android:layout_marginBottom="20dp" />

    <Button
        android:id="@+id/btnStart"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Start" />

    <Button
        android:id="@+id/btnStop"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Stop"
        android:layout_marginTop="10dp" />

</LinearLayout>
```

---

## 2️⃣ Java File — `MainActivity.java`

```java
package com.example.timerapp;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {

    TextView tvTimer;
    Button btnStart, btnStop;

    Handler handler = new Handler();
    int seconds = 0;
    boolean isRunning = false;

    Runnable timerRunnable = new Runnable() {
        @Override
        public void run() {
            if (isRunning) {
                seconds++;
                tvTimer.setText(seconds + " seconds");
                handler.postDelayed(this, 1000); // 1 second
            }
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tvTimer = findViewById(R.id.tvTimer);
        btnStart = findViewById(R.id.btnStart);
        btnStop = findViewById(R.id.btnStop);

        btnStart.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                if (!isRunning) {
                    isRunning = true;
                    handler.post(timerRunnable);
                }
            }
        });

        btnStop.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                isRunning = false;
            }
        });
    }
}
```

---

## 🧠 How It Works (Simple Explanation)

* `Handler + Runnable` runs code every **1 second**
* `seconds` increments each second
* **Start button** → sets `isRunning = true`
* **Stop button** → sets `isRunning = false`
* Time shown in `TextView`

---

## ✅ Output

* App opens → **0 seconds**
* Click **Start** → timer starts counting
* Click **Stop** → timer stops

Just tell me 👍
