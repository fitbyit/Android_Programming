✔ Username
✔ Password
✔ Confirm Password
✔ Gender (RadioButton)
✔ Terms & Conditions (CheckBox)
✔ Validation
✔ Display details on **second page**

---

# 📁 Project Structure

```
app
 └── java
     └── com.example.registrationapp
         ├── MainActivity.java
         └── DisplayActivity.java

 └── res
     └── layout
         ├── activity_main.xml
         └── activity_display.xml
```

---

# 1️⃣ `activity_main.xml` (Registration Page)

```xml
<?xml version="1.0" encoding="utf-8"?>
<ScrollView xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        android:padding="20dp">

        <EditText
            android:id="@+id/etUsername"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Username" />

        <EditText
            android:id="@+id/etPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Password"
            android:inputType="textPassword" />

        <EditText
            android:id="@+id/etConfirmPassword"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="Confirm Password"
            android:inputType="textPassword" />

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Gender"
            android:layout_marginTop="10dp"/>

        <RadioGroup
            android:id="@+id/radioGroupGender"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">

            <RadioButton
                android:id="@+id/rbMale"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Male"/>

            <RadioButton
                android:id="@+id/rbFemale"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Female"/>
        </RadioGroup>

        <CheckBox
            android:id="@+id/cbTerms"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="I agree to Terms & Conditions"/>

        <Button
            android:id="@+id/btnRegister"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="Register"
            android:layout_marginTop="15dp"/>

    </LinearLayout>
</ScrollView>
```

---

# 2️⃣ `MainActivity.java`

```java
package com.example.registrationapp;

import androidx.appcompat.app.AppCompatActivity;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.*;

public class MainActivity extends AppCompatActivity {

    EditText etUsername, etPassword, etConfirmPassword;
    RadioGroup radioGroupGender;
    CheckBox cbTerms;
    Button btnRegister;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        etUsername = findViewById(R.id.etUsername);
        etPassword = findViewById(R.id.etPassword);
        etConfirmPassword = findViewById(R.id.etConfirmPassword);
        radioGroupGender = findViewById(R.id.radioGroupGender);
        cbTerms = findViewById(R.id.cbTerms);
        btnRegister = findViewById(R.id.btnRegister);

        btnRegister.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                validateAndRegister();
            }
        });
    }

    private void validateAndRegister() {
        String username = etUsername.getText().toString().trim();
        String password = etPassword.getText().toString().trim();
        String confirmPassword = etConfirmPassword.getText().toString().trim();

        if (username.isEmpty()) {
            etUsername.setError("Username required");
            return;
        }

        if (password.isEmpty()) {
            etPassword.setError("Password required");
            return;
        }

        if (password.length() < 6) {
            etPassword.setError("Password must be at least 6 characters");
            return;
        }

        if (!password.equals(confirmPassword)) {
            etConfirmPassword.setError("Passwords do not match");
            return;
        }

        if (radioGroupGender.getCheckedRadioButtonId() == -1) {
            Toast.makeText(this, "Please select gender", Toast.LENGTH_SHORT).show();
            return;
        }

        if (!cbTerms.isChecked()) {
            Toast.makeText(this, "Please accept Terms & Conditions", Toast.LENGTH_SHORT).show();
            return;
        }

        // Get gender
        int selectedId = radioGroupGender.getCheckedRadioButtonId();
        RadioButton selectedGender = findViewById(selectedId);
        String gender = selectedGender.getText().toString();

        // Go to next activity
        Intent intent = new Intent(MainActivity.this, DisplayActivity.class);
        intent.putExtra("username", username);
        intent.putExtra("gender", gender);
        startActivity(intent);
    }
}
```

---

# 3️⃣ `activity_display.xml` (Second Page)

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="20dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="User Details"
        android:textSize="22sp"
        android:textStyle="bold"
        android:layout_marginBottom="20dp"/>

    <TextView
        android:id="@+id/tvUsername"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="18sp"/>

    <TextView
        android:id="@+id/tvGender"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="18sp"
        android:layout_marginTop="10dp"/>

</LinearLayout>
```

---

# 4️⃣ `DisplayActivity.java`

```java
package com.example.registrationapp;

import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.widget.TextView;

public class DisplayActivity extends AppCompatActivity {

    TextView tvUsername, tvGender;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_display);

        tvUsername = findViewById(R.id.tvUsername);
        tvGender = findViewById(R.id.tvGender);

        String username = getIntent().getStringExtra("username");
        String gender = getIntent().getStringExtra("gender");

        tvUsername.setText("Username: " + username);
        tvGender.setText("Gender: " + gender);
    }
}
```

---

# 5️⃣ `AndroidManifest.xml` (Important)

```xml
<application
    ...
    >
    <activity android:name=".DisplayActivity" />
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
</application>
```

---

## ✅ RESULT

✔ User registers
✔ Validation applied
✔ Details shown on next page
