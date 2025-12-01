**Predictive Back Gesture (Android 13+)** and works on **all Android versions**.

```java
package com.example.predictiveback;

import android.os.Build;
import android.os.Bundle;
import android.window.OnBackInvokedCallback;

import androidx.activity.OnBackPressedCallback;
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private final OnBackInvokedCallback backCallback = this::showExitDialog;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Android 13+ (Predictive Back)
        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.TIRAMISU) {
            getOnBackInvokedDispatcher().registerOnBackInvokedCallback(
                    OnBackInvokedCallback.PRIORITY_DEFAULT,
                    backCallback
            );
        }
        // Android 12 and below
        else {
            getOnBackPressedDispatcher().addCallback(
                    this,
                    new OnBackPressedCallback(true) {
                        @Override
                        public void handleOnBackPressed() {
                            showExitDialog();
                        }
                    }
            );
        }
    }

    private void showExitDialog() {
        new AlertDialog.Builder(this)
                .setTitle("Exit App")
                .setMessage("Do you want to exit?")
                .setPositiveButton("Yes", (d, w) -> finish())
                .setNegativeButton("No", (d, w) -> d.dismiss())
                .show();
    }
}
```

---

# ✅ **Add This in AndroidManifest (Required!)**

```xml
<application
    android:enableOnBackInvokedCallback="true"
    ... >
```
