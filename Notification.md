Activity_main.xml
```xml
 <EditText
        android:id="@+id/etName"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your name" />

    <Button
        android:id="@+id/btnGreet"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Greet Me"
        android:layout_marginTop="16dp" />
```

MainActivity.java

inside class
```java
private static final String CHANNEL_ID = "100";
private static final int NOTIFICATION_ID = 1;
```

inside onCreate
```
btn = findViewById(R.id.btnGreet);
        txt = findViewById(R.id.etName);

        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
            NotificationChannel channel = new NotificationChannel(
                    CHANNEL_ID, "Greet Channel", NotificationManager.IMPORTANCE_DEFAULT);
            channel.enableVibration(true);
            channel.setVibrationPattern(new long[]{0, 10000, 200, 500});
            NotificationManager notificationManager = getSystemService(NotificationManager.class);
            notificationManager.createNotificationChannel(channel);
        }

        btn.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                NotificationCompat.Builder builder = new NotificationCompat.Builder(MainActivity.this, CHANNEL_ID);
                builder.setSmallIcon(R.drawable.ic_launcher_foreground);
                builder.setContentTitle("Greeting");
                builder.setLargeIcon(Icon.createWithResource(MainActivity.this, R.drawable.ic_launcher_foreground));
                builder.setContentText("Hello " + txt.getText().toString());
                builder.setPriority(NotificationCompat.PRIORITY_HIGH);
                NotificationManagerCompat notificationManager = NotificationManagerCompat.from(MainActivity.this);
                if (ActivityCompat.checkSelfPermission(MainActivity.this, Manifest.permission.POST_NOTIFICATIONS) != PackageManager.PERMISSION_GRANTED) {
                    Toast.makeText(MainActivity.this, "Permission not granted", Toast.LENGTH_SHORT).show();
                    return;
                }
                notificationManager.notify(NOTIFICATION_ID, builder.build());
            }
        });
```

AndroidManifest
```
    <uses-permission android:name="android.permission.POST_NOTIFICATIONS" />
    <uses-permission android:name="android.permission.VIBRATE" />
```
