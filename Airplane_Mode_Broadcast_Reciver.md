## Airplane_Mode_Broadcast_Reciver
---

**activity_main.xml**
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity" >


    <TextView
        android:layout_margin="20dp"
        android:id="@+id/textView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Airplne Mode"
        android:textAlignment="center"
        android:textSize="34sp"
        android:textStyle="bold" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:gravity="center"
        android:orientation="vertical">

        <ImageView
            android:id="@+id/img"
            android:layout_width="140dp"
            android:layout_height="211dp"
            app:srcCompat="@drawable/mode_off" />

        <TextView
            android:id="@+id/status"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Mode : Off"
            android:textAlignment="center"
            android:textColor="#F44336"
            android:textSize="30dp"
            android:textStyle="bold" />
    </LinearLayout>
</LinearLayout>
```


**Main_Activity.java**
```java
package com.example.airplanemode;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.content.IntentFilter;
import android.os.Bundle;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;
public class MainActivity extends AppCompatActivity {
    TextView status;
    ImageView img;
    private BroadcastReceiver airplane = new BroadcastReceiver() {
        @Override
        public void onReceive(Context context, Intent intent) {
            boolean isAirplaneModeEnabled = intent.getBooleanExtra("state", false);
            if (isAirplaneModeEnabled) {
                status.setText("Airplane Mode Enabled");
                img.setImageResource(R.drawable.mode_on);
                Toast.makeText(context, "Airplane Mode Enabled", Toast.LENGTH_LONG).show();
            }
            else{
                status.setText("Airplane Mode Disabled");
                img.setImageResource(R.drawable.mode_off);
                Toast.makeText(context, "Airplane Mode Disabled", Toast.LENGTH_LONG).show();
            }
        }
    } ;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });
        status = findViewById(R.id.status);
        img = findViewById(R.id.img);
        registerReceiver(airplane, new IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED));
    }

    @Override
    protected void onDestroy() {
        super.onDestroy();
        unregisterReceiver(airplane);
    }
}
```
